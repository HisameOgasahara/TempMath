# 2. 같은 동역학을 다른 수학적 객체에서 표현하기

이 글의 출발점은 이미 동역학이 정해져 있다는 것이다.

state space $M$ 위에 flow

$$
\Phi_t:M\to M
$$

가 주어졌다고 하자.

이 글의 질문은 다음이다.

> 같은 flow를 state 자체가 아니라 observable, probability measure, Hamilton--Jacobi function, value function으로 쓰면 무엇이 달라지는가?

## 1. state의 evolution

초기 state $x_0\in M$에 대해

$$
x_t
=
\Phi_t(x_0)
$$

가 state의 evolution이다.

- $M$: state space
- $\Phi_t:M\to M$: flow
- $x_0\in M$: initial state
- $x_t\in M$: time $t$의 state

이것이 기준이다. 이후의 모든 식은 이 state evolution과 연결된다.

## 2. observable과 Koopman operator

**observable**은 state에서 값을 읽는 함수

$$
A:M\to\mathbb R
$$

이다.

state가 $x_0$에서 $\Phi_t(x_0)$로 이동하면 observable의 값은

$$
A(\Phi_t(x_0))
$$

가 된다.

이를 함수 자체의 evolution으로 옮기기 위해 **Koopman operator**

$$
U_t:\mathcal F(M)\to\mathcal F(M)
$$

를

$$
(U_tA)(x)
=
A(\Phi_t(x))
$$

로 정의한다.

- $\mathcal F(M)$: 필요한 regularity를 가진 real-valued observables의 함수공간
- $U_t$: Koopman operator

flow가 vector field $X$에서 만들어졌다면 smooth observable $A$에 대한 Koopman generator $\mathcal L$은

$$
\mathcal LA
=
X[A]
=
dA[X]
$$

이다.

유클리드 공간 $M=\mathbb R^n$에서는

$$
\mathcal LA(x)
=
\nabla A(x)\cdot X(x).
$$

Hamiltonian system에서는

$$
\mathcal LA
=
\{A,H\}
$$

로 쓸 수 있다.

## 3. probability measure와 pushforward measure

initial probability measure

$$
\mu_0\in\mathcal P(M)
$$

를 생각한다.

flow $\Phi_t$가 measure를 옮긴 결과를 **pushforward measure**

$$
\mu_t
=
(\Phi_t)_\#\mu_0
$$

로 정의한다.

measurable set $B\subseteq M$에 대해

$$
((\Phi_t)_\#\mu_0)(B)
=
\mu_0(\Phi_t^{-1}(B))
$$

이다.

observable과 probability measure는

$$
\int_M A\,d\mu_t
=
\int_M U_tA\,d\mu_0
$$

로 연결된다.

## 4. continuity equation과 Liouville equation

$M=\mathbb R^n$이고 $\mu_t$가 smooth density $\rho(t,x)$를 가진다고 하자.

state equation이

$$
\dot x
=
X(x)
$$

이면 density는 **continuity equation**

$$
\partial_t\rho
+
\nabla\cdot(\rho X)
=
0
$$

을 만족한다.

Hamiltonian system의 canonical coordinates $(q,p)$에서는 **Liouville equation**

$$
\partial_t\rho
+
\{\rho,H\}
=
0
$$

으로 쓸 수 있다.

## 5. stochastic process와 Markov semigroup

Markov process $(X_t)_{t\ge0}$에 대해 observable $A$의 evolution을

$$
(P_tA)(x)
=
\mathbb E
\left[
A(X_t)\mid X_0=x
\right]
$$

로 정의한다.

조건이 맞으면 $\{P_t\}_{t\ge0}$는 **Markov semigroup**이다.

probability measure는 dual action으로

$$
\mu_t
=
P_t^*\mu_0
$$

로 evolution한다.

generator를 $\mathcal L$이라 하면 observable은

$$
\partial_t A_t
=
\mathcal L A_t
$$

형태로, density는

$$
\partial_t\rho_t
=
\mathcal L^*\rho_t
$$

형태로 쓴다.

### Langevin SDE와 Fokker--Planck equation

$\mathbb R^d$에서

$$
dX_t
=
-\nabla U(X_t)\,dt
+
\sqrt{2\beta^{-1}}\,dW_t
$$

를 생각하자.

- $U:\mathbb R^d\to\mathbb R$: potential
- $\beta>0$: parameter
- $W_t$: $d$-dimensional Brownian motion

generator는 smooth function $A$에 대해

$$
\mathcal LA
=
-\nabla U\cdot\nabla A
+
\beta^{-1}\Delta A
$$

이다.

density는

$$
\partial_t\rho
=
\nabla\cdot(\rho\nabla U)
+
\beta^{-1}\Delta\rho
$$

를 만족한다.

이것이 Fokker--Planck equation이다.

1번 글에서 같은 PDE가 Wasserstein gradient flow로도 나타났다. 여기서는 그 PDE를 SDE의 probability density evolution으로 읽는다.

## 6. Hamilton--Jacobi equation

Hamiltonian system의 state는

$$
(q,p)\in T^*Q
$$

이다.

**Hamilton--Jacobi function**

$$
S:I\times Q\to\mathbb R
$$

가 smooth하다고 하자.

각 time $t$에서

$$
p
=
d_qS(t,q)
$$

를 사용한다.

Hamilton--Jacobi equation은

$$
\partial_tS(t,q)
+
H(q,d_qS(t,q),t)
=
0
$$

이다.

유클리드 좌표에서는

$$
\partial_tS(t,q)
+
H(q,\nabla_qS(t,q),t)
=
0.
$$

smooth solution이 존재하고 graph 표현이 유지되는 영역에서 characteristic curve는 Hamilton's equations와 연결된다.

## 7. control problem과 value function

control system

$$
\dot x
=
f(x,u,t)
$$

가 있다고 하자.

- $x(t)\in M$: state
- $u(t)\in\mathcal U$: control
- $\ell(x,u,t)$: running cost
- $\varphi(x)$: terminal cost

cost functional을

$$
J_{t,x}[u]
=
\int_t^T
\ell(x_s,u_s,s)\,ds
+
\varphi(x_T)
$$

로 정의한다.

**value function**

$$
V:[0,T]\times M\to\mathbb R
$$

은

$$
V(t,x)
=
\inf_{u}
J_{t,x}[u]
$$

로 정의한다.

smooth한 경우 **Hamilton--Jacobi--Bellman equation**

$$
\partial_tV(t,x)
+
\inf_{u\in\mathcal U}
\left\{
\ell(x,u,t)
+
d_xV(t,x)[f(x,u,t)]
\right\}
=
0
$$

을 만족한다.

terminal condition은

$$
V(T,x)=\varphi(x)
$$

이다.

최소값을 달성하는 control $u^*(t,x)$가 존재하면

$$
u^*(t,x)
\in
\operatorname*{arg\,min}_{u\in\mathcal U}
\left\{
\ell(x,u,t)
+
d_xV[f(x,u,t)]
\right\}
$$

으로 optimal feedback을 얻고

$$
\dot x
=
f(x,u^*(t,x),t)
$$

에서 optimal state trajectory를 얻는다.

Hamilton--Jacobi function $S$와 value function $V$는 같은 object가 아니다.

## 8. 한 연결로 정리

deterministic ODE

$$
\dot x=X(x)
$$

에서 시작하면

$$
x_t=\Phi_t(x_0)
$$

이고 observable은

$$
(U_tA)(x)=A(\Phi_t(x))
$$

이며 probability measure는

$$
\mu_t=(\Phi_t)_\#\mu_0
$$

이다.

smooth density가 존재하면

$$
\partial_t\rho+\nabla\cdot(\rho X)=0.
$$

따라서 중심 연결은

$$
\boxed{
\text{state}
\longrightarrow
\text{observable}
\longrightarrow
\text{probability measure}
\longrightarrow
\text{density}
}
$$

이다.

Hamilton--Jacobi function과 value function은 모든 dynamical system에 자동으로 붙는 object가 아니라 각각 Hamiltonian mechanics와 optimal control problem이라는 추가 구조가 있을 때 도입된다.

## 9. 다음 글로의 연결

다음 글에서는 Fourier transform, Laplace transform, spectrum, resolvent, semigroup, Lyapunov function, attractor, invariant manifold, moment closure, Mori--Zwanzig, coarse graining, renormalization group을 다룬다.

# 정확한 정의와 조건

### Koopman operator

measurable map $\Phi_t:M\to M$와 observable space $\mathcal F(M)$이 composition에 대해 닫혀 있으면

$$
U_tA=A\circ\Phi_t
$$

로 Koopman operator를 정의한다.

### pushforward measure

measurable map $F:M\to N$와 measure $\mu$에 대해

$$
(F_\#\mu)(B)
=
\mu(F^{-1}(B))
$$

로 정의한다.

### Markov semigroup

operators $\{P_t\}_{t\ge0}$가

$$
P_0=I,
\qquad
P_{t+s}=P_tP_s
$$

를 만족하고 positivity와 constant preservation을 만족할 때 Markov semigroup이라 한다.

### HJB equation

본문에서는 classical differentiability를 가정했다. 일반적인 optimal control에서는 value function이 differentiable하지 않을 수 있으므로 viscosity solution을 사용한다.

### Hamilton--Jacobi equation

본문에서는 $Q=\mathbb R^n$ 또는 smooth manifold의 한 coordinate chart에서 $S$가 충분히 smooth하고 $d_qS$의 graph가 Hamiltonian flow 아래에서 적절히 유지되는 경우를 사용했다.
