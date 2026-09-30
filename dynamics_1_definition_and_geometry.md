# 1. 동역학을 정의하는 수학적 구조

이 글의 질문은 하나다.

> 시간이 지나면서 변하는 계를 수학적으로 쓰려면 무엇을 먼저 정해야 하는가?

처음에는 익숙한 유클리드 공간에서 시작한다. 이후 필요한 경우에만 다양체, 함수공간, 확률측도 공간으로 확장한다.

$$
\boxed{
\text{state}
\longrightarrow
\text{state space}
\longrightarrow
\text{vector field or variational principle}
\longrightarrow
\text{integral curve}
\longrightarrow
\text{flow}
}
$$

이 글에서 한 번 수학 용어를 도입한 뒤에는 같은 개념을 다른 표현으로 바꾸지 않는다.

## 1. state와 state space

가장 먼저 정할 것은 한 시각의 계를 완전히 기술하는 값이다. 이 값을 **state**라고 한다.

유한차원에서는 state를

$$
x(t)\in M
$$

으로 쓴다.

- $I\subseteq\mathbb R$: 시간 구간인 집합
- $M$: state space
- $x:I\to M$: 시간 $t$에 state $x(t)$를 대응시키는 map

가장 익숙한 경우에는 $M=\mathbb R^n$이다.

예를 들어 질량–스프링에서 위치 $q(t)\in\mathbb R$만으로는 다음 운동을 결정할 수 없으므로 속도까지 포함하여

$$
x(t)=
\begin{pmatrix}
q(t)\\
v(t)
\end{pmatrix}
\in\mathbb R^2,
\qquad
v(t)=\dot q(t)
$$

를 state로 잡는다.

이 선택의 목적은 현재 state를 알면 동역학 법칙이 다음 순간의 변화를 정할 수 있게 하는 것이다.

### configuration manifold와 phase space

고전역학에서는 위치와 자세를 모은 공간을 **configuration manifold** $Q$라고 한다.

- $Q$: configuration manifold
- $TQ$: tangent bundle
- $T^*Q$: cotangent bundle

라그랑주역학에서는 $(q,\dot q)\in TQ$를 사용하고, 해밀턴역학에서는 $(q,p)\in T^*Q$를 사용한다.

$T^*Q$는 해밀턴역학의 **phase space**이다.

## 2. tangent vector와 vector field

state $x\in M$에서 가능한 순간 변화는 **tangent vector**

$$
v\in T_xM
$$

로 쓴다.

- $T_xM$: $x$에서의 tangent space
- $v$: $T_xM$의 원소인 tangent vector

$M=\mathbb R^n$이면 $T_xM$을 $\mathbb R^n$과 동일시할 수 있으므로 그냥 속도 벡터라고 생각해도 된다.

모든 state $x$에 tangent vector를 하나씩 지정하는 것을 **vector field**라고 한다.

$$
X:M\to TM,
\qquad
X(x)\in T_xM.
$$

유클리드 공간에서는

$$
X:\mathbb R^n\to\mathbb R^n
$$

이다.

vector field가 주어지면 autonomous ODE

$$
\dot x(t)=X(x(t))
$$

를 얻는다.

- $X$: vector field
- $x:I\to M$: 미지의 curve
- $\dot x(t)\in T_{x(t)}M$: curve의 tangent vector

이 식의 목적은 각 state에서 가능한 tangent vector 중 실제 시간 변화에 사용할 tangent vector를 지정하는 것이다.

## 3. integral curve와 flow

vector field $X$가 주어졌을 때

$$
\dot\gamma(t)=X(\gamma(t))
$$

를 만족하는 curve

$$
\gamma:I\to M
$$

를 $X$의 **integral curve**라고 한다.

초기조건 $\gamma(0)=x_0$을 함께 주면

$$
\dot\gamma(t)=X(\gamma(t)),
\qquad
\gamma(0)=x_0
$$

라는 initial value problem이 된다.

초기조건마다 integral curve가 유일하게 존재한다고 하자. 그러면

$$
\Phi_t(x_0)=\gamma_{x_0}(t)
$$

로 **flow**

$$
\Phi_t:M\to M
$$

를 정의할 수 있다.

따라서

$$
\boxed{
X
\longrightarrow
\dot x=X(x)
\longrightarrow
\gamma_{x_0}
\longrightarrow
\Phi_t
}
$$

이다.

vector field와 flow는 같은 것이 아니다. $X$는 순간 변화율을 정하고, $\Phi_t$는 유한한 시간 $t$ 뒤의 state를 정한다.

## 4. Riemannian metric과 gradient flow

함수

$$
F:M\to\mathbb R
$$

가 있다고 하자.

- $F$: 실숫값 smooth function
- $dF_x\in T_x^*M$: $x$에서의 differential
- $T_x^*M$: cotangent space

$dF_x$는 tangent vector가 아니라 covector이다.

따라서 $dF_x$만으로는 곧바로 $\dot x$를 정할 수 없다.

**Riemannian metric**

$$
g_x:T_xM\times T_xM\to\mathbb R
$$

을 주면 gradient $\operatorname{grad}_gF(x)\in T_xM$를

$$
g_x\left(\operatorname{grad}_gF(x),v\right)
=
dF_x[v]
\qquad
\text{for every }v\in T_xM
$$

로 정의한다.

그 뒤 **gradient flow**를

$$
\dot x(t)
=
-\operatorname{grad}_gF(x(t))
$$

로 정의할 수 있다.

이 식을 사용하는 목적은 $F$가 감소하는 동역학을 만드는 것이다.

실제로

$$
\frac{d}{dt}F(x(t))
=
dF_{x(t)}[\dot x(t)]
=
-g_{x(t)}
\left(
\operatorname{grad}_gF,
\operatorname{grad}_gF
\right)
\le 0.
$$

### 유클리드 공간의 경우

$M=\mathbb R^n$이고 표준 내적을 metric으로 쓰면

$$
\operatorname{grad}_gF=\nabla F
$$

이므로

$$
\dot x=-\nabla F(x)
$$

가 된다.

## 5. 정보기하: Fisher metric과 natural gradient flow

정보기하에서는 parameter $\theta$로 표시되는 확률분포족

$$
\mathcal S
=
\left\{
p_\theta
\mid
\theta\in\Theta
\right\}
$$

을 생각한다.

- $\Theta\subseteq\mathbb R^d$: parameter space
- $p_\theta$: probability density 또는 probability mass function
- $\mathcal S$: statistical model

regular statistical model에서는 **Fisher information matrix**

$$
g_{ij}(\theta)
=
\mathbb E_{p_\theta}
\left[
\partial_i\log p_\theta(X)\,
\partial_j\log p_\theta(X)
\right]
$$

를 Riemannian metric으로 사용한다.

목적함수

$$
F:\Theta\to\mathbb R
$$

가 있을 때 natural gradient는

$$
\operatorname{grad}_{g_{\mathrm F}}F
=
g_{\mathrm F}^{-1}\nabla_\theta F
$$

이고 natural gradient flow는

$$
\dot\theta
=
-
g_{\mathrm F}(\theta)^{-1}
\nabla_\theta F(\theta)
$$

이다.

여기서도 구조는 앞 절과 같다.

$$
\boxed{
\text{statistical manifold}
+
\text{Fisher metric}
+
F
\longrightarrow
\text{gradient flow}
}
$$

### exponential family 예시

$$
p_\theta(x)
=
h(x)
\exp
\left(
\langle\theta,T(x)\rangle-\psi(\theta)
\right)
$$

인 regular exponential family에서는

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

## 6. 수송기하: Wasserstein distance와 gradient flow

이번에는 state가 하나의 점이 아니라 probability measure라고 하자.

유클리드 공간 $\mathbb R^d$ 위의 2차 moment가 유한한 probability measure들의 집합을

$$
\mathcal P_2(\mathbb R^d)
$$

라고 한다.

두 probability measure $\mu,\nu\in\mathcal P_2(\mathbb R^d)$ 사이의 **2-Wasserstein distance**는

$$
W_2(\mu,\nu)^2
=
\inf_{\pi\in\Pi(\mu,\nu)}
\int_{\mathbb R^d\times\mathbb R^d}
\|x-y\|^2
\,d\pi(x,y)
$$

로 정의한다.

- $\Pi(\mu,\nu)$: marginals가 $\mu,\nu$인 coupling들의 집합
- $\pi$: coupling
- $W_2$: 2-Wasserstein distance

매끄러운 density $\rho(t,x)$를 쓰는 경우 mass conservation은 **continuity equation**

$$
\partial_t\rho
+
\nabla\cdot(\rho v)
=
0
$$

으로 쓴다.

functional

$$
\mathcal F:
\mathcal P_2(\mathbb R^d)
\to
\mathbb R
$$

의 Wasserstein gradient flow는 매끄러운 경우 형식적으로

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

정보기하와 수송기하의 공통점은 둘 다 확률분포를 다루지만 metric이 다르다는 것이다.

- Fisher metric: statistical model 안에서 parameter 변화의 크기를 정한다.
- Wasserstein distance: probability mass를 옮기는 비용으로 measure 사이의 거리를 정한다.

## 7. symplectic form과 Hamiltonian vector field

해밀턴역학에서는 phase space $M=T^*Q$ 위에 **symplectic form**

$$
\omega\in\Omega^2(M)
$$

을 둔다.

symplectic form은 closed이고 nondegenerate인 differential $2$-form이다.

Hamiltonian

$$
H:M\to\mathbb R
$$

가 주어지면 **Hamiltonian vector field** $X_H$를

$$
\iota_{X_H}\omega
=
dH
$$

로 정의한다.

canonical coordinates $(q^i,p_i)$에서는

$$
\omega
=
\sum_i dq^i\wedge dp_i
$$

이고 Hamilton's equations는

$$
\dot q^i
=
\frac{\partial H}{\partial p_i},
\qquad
\dot p_i
=
-
\frac{\partial H}{\partial q^i}.
$$

따라서

$$
\boxed{
(T^*Q,\omega)
+
H
\longrightarrow
X_H
\longrightarrow
\text{integral curves}
}
$$

이다.

Riemannian metric으로 만든 gradient flow에서는 $F$가 감소하지만, Hamiltonian vector field에서는

$$
\frac{d}{dt}H
=
dH[X_H]
=
\omega(X_H,X_H)
=
0
$$

이므로 autonomous Hamiltonian system의 $H$가 보존된다.

## 8. Lagrangian과 action functional

라그랑주역학에서는 curve 자체를 먼저 비교한다.

**Lagrangian**

$$
L:TQ\to\mathbb R
$$

에서 **action functional**

$$
\mathcal S[q]
=
\int_{t_0}^{t_1}
L(q(t),\dot q(t))
\,dt
$$

를 정의한다.

- $q:[t_0,t_1]\to Q$: curve
- $\mathcal S$: curve를 실수에 대응시키는 functional

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

정칙한 경우에는 Legendre transform을 사용하여 해밀턴역학과 연결된다.

$$
p_i
=
\frac{\partial L}{\partial\dot q^i},
\qquad
H(q,p)
=
p\cdot\dot q-L(q,\dot q).
$$

## 9. control system

제어이론에서는 입력을 포함한 state equation을

$$
\dot x
=
f(x,u,t)
$$

로 둔다.

- $M$: state space
- $\mathcal U$: admissible control values의 집합
- $u:I\to\mathcal U$: control input
- $f:M\times\mathcal U\times I\to TM$: 각 $(x,u,t)$에서 $T_xM$의 vector를 주는 map

유클리드 공간에서는

$$
f:
\mathbb R^n\times\mathbb R^m\times I
\to
\mathbb R^n
$$

으로 생각하면 된다.

control-affine system은

$$
\dot x
=
X_0(x)
+
\sum_{i=1}^{m}
u_i(t)X_i(x)
$$

이다.

여기서는 control input $u$를 정하면 vector field가 정해지고, 그 뒤 integral curve를 구한다.

## 10. 함수가 state인 경우: PDE

state는 항상 유한차원 벡터일 필요가 없다.

예를 들어 heat equation

$$
\partial_tu(t,\xi)
=
\Delta u(t,\xi)
$$

에서는 한 시각의 함수

$$
u(t,\cdot)\in\mathcal X
$$

자체를 state로 본다.

- $\Omega\subseteq\mathbb R^d$: spatial domain
- $\mathcal X$: $\Omega$ 위의 함수공간
- $A=\Delta$: 적절한 domain $D(A)\subseteq\mathcal X$를 갖는 operator

그러면

$$
\frac{d}{dt}u(t)
=
Au(t)
$$

라는 abstract evolution equation으로 쓸 수 있다.

## 11. 이 글의 결론과 다음 글

$$
\boxed{
\begin{array}{c}
\text{state }x\\
\downarrow\\
\text{state space }M\\
\downarrow\\
\text{vector field }X
\text{ or variational principle}\\
\downarrow\\
\text{integral curve}\\
\downarrow\\
\text{flow}
\end{array}
}
$$

Riemannian geometry, information geometry, optimal transport, Hamiltonian mechanics, Lagrangian mechanics, control theory는 이 순서의 서로 다른 부분에 추가 구조를 제공한다.

다음 글에서는 이미 정해진 하나의 동역학을 **observable, probability measure, Hamilton--Jacobi function, value function**에서 어떻게 다시 쓰는지 다룬다.

# 정확한 정의와 조건

본문에서는 구조를 먼저 보기 위해 강한 조건을 사용했다.

### smooth manifold

$n$-dimensional smooth manifold $M$은 locally $\mathbb R^n$과 diffeomorphic이고 smooth atlas가 주어진 Hausdorff, second-countable topological space이다.

### tangent space

$x\in M$에서 tangent space $T_xM$은 $x$에서의 derivation들의 vector space로 정의할 수 있다. 동치인 정의로 curve의 equivalence class를 사용할 수 있다.

### vector field

smooth vector field는 smooth section

$$
X:M\to TM,
\qquad
\pi\circ X=\operatorname{id}_M
$$

이다.

### integral curve

vector field $X$의 integral curve는 smooth curve $\gamma:I\to M$로서

$$
\dot\gamma(t)=X_{\gamma(t)}
$$

를 만족한다.

### flow

local flow는 열린집합 $\mathcal D\subseteq\mathbb R\times M$에서 정의된 smooth map

$$
\Phi:\mathcal D\to M
$$

으로

$$
\Phi_0=\operatorname{id}_M,
\qquad
\Phi_{t+s}(x)=\Phi_t(\Phi_s(x))
$$

가 정의되는 범위에서 성립한다.

### Riemannian metric

Riemannian metric은 각 $x\in M$에 inner product

$$
g_x:T_xM\times T_xM\to\mathbb R
$$

를 smooth하게 배정하는 것이다.

### symplectic form

symplectic form은 differential $2$-form $\omega\in\Omega^2(M)$로서

$$
d\omega=0
$$

이고 각 $x\in M$에서 bilinear form $\omega_x$가 nondegenerate이다.

### Fisher information metric

regular statistical model에서 score가 square-integrable이고 필요한 미분과 적분 교환이 가능하며 Fisher information matrix가 positive definite라고 가정하면

$$
g_{ij}(\theta)
=
\mathbb E_\theta
[
\partial_i\log p_\theta
\partial_j\log p_\theta
]
$$

가 parameter manifold의 Riemannian metric을 이룬다.

### Wasserstein space

complete separable metric space $(X,d)$에 대해

$$
\mathcal P_2(X)
=
\left\{
\mu\in\mathcal P(X):
\int_X d(x,x_0)^2\,d\mu(x)<\infty
\right\}
$$

를 정의한다. $W_2$는 couplings에 대한 quadratic transport cost의 infimum으로 정의한다.

본문의 PDE 형태의 Wasserstein gradient flow는 $X=\mathbb R^d$, density의 충분한 smoothness와 decay 또는 적절한 boundary condition을 가정한 형식적 표현이다.
