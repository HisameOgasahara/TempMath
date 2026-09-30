# 동역학은 어떻게 정해지는가

처음 질문은 단순하다.

> 시간이 지나면서 무엇이 변하고, 그 변화는 무엇이 정하는가?

이 질문을 수학적으로 쓰면 먼저 **state**와 **state space**를 정하고, state의 순간 변화인 **tangent vector**를 정하는 법칙을 준다. 그 법칙으로부터 **integral curve**와 **flow**가 나온다.

$$
\boxed{
\text{state}
\longrightarrow
\text{state space}
\longrightarrow
\text{tangent vector}
\longrightarrow
\text{vector field or variational equation}
\longrightarrow
\text{integral curve}
\longrightarrow
\text{flow}
}
$$

## 1. 무엇이 변하는가: state와 state space

한 시각의 계를 기술하는 값을 **state**라고 하고, 가능한 state 전체의 집합을 **state space**라고 한다.

시간 구간을 $I\subseteq\mathbb R$, state space를 $M$이라 하면 시간에 따른 state는 map

$$
x:I\to M
$$

으로 쓴다.

가장 익숙한 경우는 $M=\mathbb R^n$이다. 예를 들어 질량–스프링에서는 위치 $q$만으로 다음 운동이 정해지지 않으므로

$$
x(t)
=
\begin{pmatrix}
q(t)\\
\dot q(t)
\end{pmatrix}
\in\mathbb R^2
$$

를 state로 잡는다.

고전역학에서는 configuration을 모은 manifold를 $Q$라고 한다. 라그랑주역학은 주로

$$
(q,\dot q)\in TQ
$$

를, 해밀턴역학은

$$
(q,p)\in T^*Q
$$

를 사용한다.

함수 전체가 state일 수도 있다. 예를 들어 heat equation에서는

$$
u(t,\cdot)\in\mathcal X
$$

가 한 시각의 state이고 $\mathcal X$는 함수공간이다.

확률분포 전체가 state일 수도 있다. 수송기하에서는

$$
\mu_t\in\mathcal P_2(\mathbb R^d)
$$

를 시간에 따라 변하는 state로 본다.

따라서 첫 단계는 항상 같다.

$$
\boxed{
\text{무엇을 state로 선택할 것인가}
}
$$

## 2. state는 어느 방향으로 변할 수 있는가: tangent space

smooth manifold $M$의 state $x\in M$에서 가능한 순간 변화는 **tangent vector**

$$
v\in T_xM
$$

로 쓴다.

$T_xM$은 $x$에서의 **tangent space**이다. $M=\mathbb R^n$이면 $T_xM$을 $\mathbb R^n$과 동일시할 수 있다.

모든 $x\in M$에 tangent vector를 하나씩 지정하는 smooth section을 **vector field**

$$
X:M\to TM,
\qquad
X(x)\in T_xM
$$

라고 한다.

그러면 state equation은

$$
\dot x(t)=X(x(t))
$$

가 된다.

여기까지는 어떤 vector field를 써야 하는지 아직 정하지 않았다. 다음 단계에서 geometry, energy, action, control input이 그 vector field 또는 equation을 정한다.

## 3. 무엇이 실제 동역학을 정하는가

### Riemannian metric을 사용하는 경우

smooth function

$$
F:M\to\mathbb R
$$

의 differential은

$$
dF_x\in T_x^*M
$$

이다. 이것은 cotangent vector이므로 직접 $\dot x$로 사용할 수 없다.

Riemannian metric

$$
g_x:T_xM\times T_xM\to\mathbb R
$$

을 주면 gradient $\operatorname{grad}_gF(x)\in T_xM$를

$$
g_x\!\left(\operatorname{grad}_gF(x),v\right)
=
dF_x[v]
\qquad
(v\in T_xM)
$$

로 정의할 수 있다.

따라서 gradient flow

$$
\dot x
=
-\operatorname{grad}_gF(x)
$$

를 얻는다.

유클리드 공간에서는 $g$가 표준 inner product이므로

$$
\dot x=-\nabla F(x)
$$

가 된다.

### symplectic form을 사용하는 경우

해밀턴역학에서는 phase space $T^*Q$에 symplectic form

$$
\omega\in\Omega^2(T^*Q)
$$

가 있고 Hamiltonian

$$
H:T^*Q\to\mathbb R
$$

가 주어진다.

Hamiltonian vector field $X_H$는

$$
\iota_{X_H}\omega=dH
$$

로 정의한다.

canonical coordinates에서는

$$
\dot q^i
=
\frac{\partial H}{\partial p_i},
\qquad
\dot p_i
=
-\frac{\partial H}{\partial q^i}.
$$

즉

$$
(T^*Q,\omega,H)
\longrightarrow
X_H
\longrightarrow
\dot z=X_H(z)
$$

이다.

### action functional을 사용하는 경우

라그랑주역학에서는 먼저 Lagrangian

$$
L:TQ\to\mathbb R
$$

을 정하고 curve $q:[t_0,t_1]\to Q$에 대해 action functional

$$
\mathcal S[q]
=
\int_{t_0}^{t_1}
L(q(t),\dot q(t))\,dt
$$

을 만든다.

끝점을 고정한 variation $\delta q$에 대해

$$
D\mathcal S[q](\delta q)=0
$$

을 요구하면 Euler--Lagrange equation

$$
\frac{d}{dt}
\frac{\partial L}{\partial\dot q^i}
-
\frac{\partial L}{\partial q^i}
=
0
$$

을 얻는다.

여기서는 vector field를 먼저 주는 대신, action functional의 stationary curve를 구해 equation을 얻는다.

### control input을 사용하는 경우

control system은

$$
\dot x=f(x,u,t)
$$

로 쓴다.

- $M$: state space
- $\mathcal U$: control values의 집합
- $u:I\to\mathcal U$: control input
- $f:M\times\mathcal U\times I\to TM$: 각 $(x,u,t)$에 tangent vector를 주는 map

control input $u$를 정하면 state equation이 정해진다.

## 4. 같은 구조가 정보기하와 수송기하에서는 어떻게 나타나는가

앞의 gradient flow에서 핵심은

$$
\text{state space}
+
\text{metric}
+
\text{function or functional}
\longrightarrow
\text{gradient flow}
$$

였다.

정보기하와 수송기하는 이 구조를 서로 다른 state space와 metric에서 구현한다.

### 정보기하

regular statistical model을

$$
\mathcal S
=
\{p_\theta:\theta\in\Theta\subseteq\mathbb R^d\}
$$

라고 하자.

Fisher metric은

$$
g_{ij}(\theta)
=
\mathbb E_{p_\theta}
\left[
\partial_i\log p_\theta(X)
\partial_j\log p_\theta(X)
\right]
$$

이다.

목적함수

$$
F:\Theta\to\mathbb R
$$

에 대한 natural gradient flow는

$$
\dot\theta
=
-
g_{\mathrm F}(\theta)^{-1}
\nabla_\theta F(\theta)
$$

이다.

따라서 정보기하에서는 parameter $\theta$가 state이고 Fisher metric이 gradient를 정한다.

regular exponential family

$$
p_\theta(x)
=
h(x)\exp
\left(
\langle\theta,T(x)\rangle-\psi(\theta)
\right)
$$

에서는

$$
g_{ij}(\theta)
=
\frac{\partial^2\psi}{\partial\theta^i\partial\theta^j}
=
\operatorname{Cov}_{p_\theta}
\left[
T_i(X),T_j(X)
\right].
$$

### 수송기하

state space를

$$
\mathcal P_2(\mathbb R^d)
$$

로 잡는다.

두 probability measure $\mu,\nu\in\mathcal P_2(\mathbb R^d)$ 사이의 $2$-Wasserstein distance는

$$
W_2(\mu,\nu)^2
=
\inf_{\pi\in\Pi(\mu,\nu)}
\int_{\mathbb R^d\times\mathbb R^d}
\|x-y\|^2\,d\pi(x,y)
$$

이다.

smooth density $\rho$와 충분히 좋은 boundary condition을 가정하면 functional

$$
\mathcal F:\mathcal P_2(\mathbb R^d)\to\mathbb R
$$

의 Wasserstein gradient flow는 형식적으로

$$
\partial_t\rho
=
\nabla\cdot
\left(
\rho
\nabla
\frac{\delta\mathcal F}{\delta\rho}
\right)
$$

가 된다.

예를 들어

$$
\mathcal F[\rho]
=
\int_{\mathbb R^d}
U(x)\rho(x)\,dx
+
\beta^{-1}
\int_{\mathbb R^d}
\rho(x)\log\rho(x)\,dx
$$

이면

$$
\partial_t\rho
=
\nabla\cdot(\rho\nabla U)
+
\beta^{-1}\Delta\rho.
$$

이 식은 Fokker--Planck equation이다.

정보기하와 수송기하는 둘 다 probability distribution을 다루지만 같은 metric을 쓰는 것은 아니다.

## 5. equation에서 integral curve와 flow로

vector field $X$가 정해졌다면 initial value problem

$$
\dot\gamma(t)=X(\gamma(t)),
\qquad
\gamma(0)=x_0
$$

을 푼다.

solution curve $\gamma$를 **integral curve**라고 한다.

초기조건마다 integral curve가 유일하게 존재하는 범위에서

$$
\Phi_t(x_0)
=
\gamma_{x_0}(t)
$$

로 **flow**

$$
\Phi_t:M\to M
$$

를 정의한다.

따라서 이 글 전체의 순서는

$$
\boxed{
\text{state}
\to
\text{state space}
\to
\text{tangent space}
\to
\text{dynamical law}
\to
\text{integral curve}
\to
\text{flow}
}
$$

이다.

다음 글에서는 이 flow가 이미 주어졌다고 가정하고, 같은 동역학을 observable과 probability measure에서 어떻게 나타내는지 본다.

---

# 정확한 정의와 조건

## smooth vector field

smooth vector field는 tangent bundle projection $\pi:TM\to M$에 대한 smooth section

$$
X:M\to TM,
\qquad
\pi\circ X=\operatorname{id}_M
$$

이다.

## flow

local flow는 열린집합 $\mathcal D\subseteq\mathbb R\times M$에서 정의된 smooth map

$$
\Phi:\mathcal D\to M
$$

으로, 정의되는 범위에서

$$
\Phi_0=\operatorname{id}_M,
\qquad
\Phi_{t+s}(x)=\Phi_t(\Phi_s(x))
$$

를 만족한다.

## Riemannian metric

Riemannian metric은 각 $x\in M$에 inner product

$$
g_x:T_xM\times T_xM\to\mathbb R
$$

를 smooth하게 배정한 것이다.

## symplectic form

symplectic form은 differential $2$-form $\omega\in\Omega^2(M)$로서

$$
d\omega=0
$$

이고 각 $x\in M$에서 $\omega_x$가 nondegenerate이다.

## Wasserstein space

complete separable metric space $(X,d)$에 대해

$$
\mathcal P_2(X)
=
\left\{
\mu\in\mathcal P(X):
\int_X d(x,x_0)^2\,d\mu(x)<\infty
\right\}
$$

로 정의한다. 본문의 PDE 표현은 $X=\mathbb R^d$와 smooth density를 가정한 경우이다.
