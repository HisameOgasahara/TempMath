# 같은 동역학은 다른 수학적 객체에서 어떻게 나타나는가

앞 글에서 state space $M$과 flow

$$
\Phi_t:M\to M
$$

를 얻었다.

이 글에서는 새로운 동역학을 만드는 것이 아니라, 같은 flow가 다른 수학적 객체에 어떻게 작용하는지 본다.

핵심은 다음 세 가지다.

$$
\boxed{
\text{state}
\qquad
\text{observable}
\qquad
\text{probability measure}
}
$$

Hamilton--Jacobi function과 value function은 이 공통 흐름에 자동으로 붙는 것이 아니라, 각각 Hamiltonian system과 optimal control problem에서 추가로 생긴다.

## 1. 기준: state의 evolution

initial state $x_0\in M$에 대해

$$
x_t
=
\Phi_t(x_0)
$$

가 state의 evolution이다.

이 식이 기준이고 이후의 object들은 모두 이 flow와 연결된다.

## 2. state에서 observable로

**observable**은 state에서 값을 읽는 function

$$
A:M\to\mathbb R
$$

이다.

state가 $\Phi_t(x)$로 이동했을 때 observable 값은

$$
A(\Phi_t(x))
$$

이다.

이를 function 자체의 변화로 쓰기 위해 **Koopman operator**

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

따라서 같은 flow를

$$
x\mapsto\Phi_t(x)
$$

로 보거나

$$
A\mapsto A\circ\Phi_t
$$

로 볼 수 있다.

flow가 vector field $X$에서 만들어지고 $A$가 smooth하면 Koopman generator $\mathcal L$은

$$
\mathcal LA
=
X[A]
=
dA[X]
$$

이다.

유클리드 공간에서는

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

가 된다.

## 3. state에서 probability measure로

initial state가 하나가 아니라 probability measure

$$
\mu_0\in\mathcal P(M)
$$

로 주어졌다고 하자.

flow가 measure를 옮긴 결과는 **pushforward measure**

$$
\mu_t
=
(\Phi_t)_\#\mu_0
$$

이다.

measurable set $B\subseteq M$에 대해

$$
((\Phi_t)_\#\mu_0)(B)
=
\mu_0(\Phi_t^{-1}(B))
$$

로 정의한다.

observable과 probability measure는

$$
\int_M A\,d\mu_t
=
\int_M U_tA\,d\mu_0
$$

로 연결된다.

즉 state에 작용하는 같은 flow가 observable에는 composition으로, probability measure에는 pushforward로 나타난다.

## 4. density가 존재하면 continuity equation이 된다

$M=\mathbb R^n$이고 $\mu_t$가 smooth density $\rho(t,x)$를 가진다고 하자.

state equation이

$$
\dot x=X(x)
$$

이면 density는

$$
\partial_t\rho
+
\nabla\cdot(\rho X)
=
0
$$

을 만족한다.

이 식이 **continuity equation**이다.

Hamiltonian system에서는 Hamiltonian vector field의 구조 때문에 canonical coordinates에서

$$
\partial_t\rho
+
\{\rho,H\}
=
0
$$

이라는 **Liouville equation**을 얻는다.

여기까지의 연결은 하나다.

$$
\boxed{
\Phi_t
\longrightarrow
U_tA=A\circ\Phi_t
\qquad\text{and}\qquad
\mu_t=(\Phi_t)_\#\mu_0
}
$$

## 5. stochastic dynamics에서는 Markov semigroup이 같은 역할을 한다

확률적 동역학에서는 deterministic flow $\Phi_t$ 대신 transition law를 사용한다.

Markov process $(X_t)_{t\ge0}$에 대해

$$
(P_tA)(x)
=
\mathbb E
\left[
A(X_t)\mid X_0=x
\right]
$$

로 **Markov semigroup**을 정의한다.

observable은 $P_t$로 변하고 probability measure는 dual operator $P_t^*$로

$$
\mu_t=P_t^*\mu_0
$$

처럼 변한다.

generator를 $\mathcal L$이라고 하면

$$
\partial_t A_t
=
\mathcal L A_t
$$

와

$$
\partial_t\rho_t
=
\mathcal L^*\rho_t
$$

가 서로 대응한다.

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

generator는

$$
\mathcal LA
=
-\nabla U\cdot\nabla A
+
\beta^{-1}\Delta A
$$

이고 density는

$$
\partial_t\rho
=
\nabla\cdot(\rho\nabla U)
+
\beta^{-1}\Delta\rho
$$

를 만족한다.

앞 글에서는 이 Fokker--Planck equation이 Wasserstein gradient flow로 나왔다. 여기서는 같은 equation을 Langevin SDE의 probability density evolution으로 얻었다.

즉 같은 PDE가 서로 다른 출발점에서 연결된다.

## 6. Hamiltonian system에서는 Hamilton--Jacobi function이 생긴다

Hamiltonian system의 state는

$$
(q,p)\in T^*Q
$$

이다.

smooth function

$$
S:I\times Q\to\mathbb R
$$

가

$$
\partial_tS(t,q)
+
H(q,d_qS(t,q),t)
=
0
$$

을 만족하면 이것이 **Hamilton--Jacobi equation**이다.

유클리드 좌표에서는

$$
\partial_tS(t,q)
+
H(q,\nabla_qS(t,q),t)
=
0.
$$

또

$$
p=d_qS(t,q)
$$

를 통해 $S$의 differential이 momentum을 정한다.

따라서 Hamilton--Jacobi function은 Hamiltonian integral curves의 family를 function 하나로 기술하는 데 사용된다.

## 7. optimal control에서는 value function이 생긴다

control system

$$
\dot x=f(x,u,t)
$$

에 running cost $\ell$과 terminal cost $\varphi$를 준다.

cost functional은

$$
J_{t,x}[u]
=
\int_t^T
\ell(x_s,u_s,s)\,ds
+
\varphi(x_T)
$$

이다.

**value function**

$$
V:[0,T]\times M\to\mathbb R
$$

은

$$
V(t,x)
=
\inf_u J_{t,x}[u]
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

최소값을 달성하는 control이 있으면

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

로 optimal feedback을 얻는다.

Hamilton--Jacobi function $S$와 value function $V$는 둘 다 function이지만 같은 수학적 object가 아니다.

## 8. 전체 연결

deterministic dynamics에서는

$$
\boxed{
\begin{array}{c}
x_t=\Phi_t(x_0)\\
\downarrow\\
(U_tA)(x)=A(\Phi_t(x))\\
\downarrow\\
\mu_t=(\Phi_t)_\#\mu_0\\
\downarrow\\
\partial_t\rho+\nabla\cdot(\rho X)=0
\end{array}
}
$$

로 연결된다.

확률적 dynamics에서는 $\Phi_t$ 대신 Markov semigroup $P_t$가 observable과 probability measure를 연결한다.

Hamilton--Jacobi function과 value function은 각각 Hamiltonian system과 optimal control problem에서 추가로 정의된다.

다음 글에서는 이렇게 얻은 operator, generator, observable, probability measure를 이용해 spectrum과 mode를 분석하고, 그 분석을 바탕으로 dynamical system을 축약한다.

---

# 정확한 정의와 조건

## Koopman operator

measurable map $\Phi_t:M\to M$에 대해 composition이 정의되는 function space $\mathcal F(M)$ 위에서

$$
U_tA=A\circ\Phi_t
$$

로 정의한다.

## pushforward measure

measurable map $F:M\to N$와 measure $\mu$에 대해

$$
(F_\#\mu)(B)
=
\mu(F^{-1}(B))
$$

로 정의한다.

## Markov semigroup

operators $\{P_t\}_{t\ge0}$가

$$
P_0=I,
\qquad
P_{t+s}=P_tP_s
$$

를 만족하고 positivity와 constant preservation을 만족할 때 Markov semigroup이라고 한다.

## HJB equation

본문에서는 value function이 differentiable한 경우만 썼다. 일반적인 optimal control에서는 viscosity solution을 사용한다.
