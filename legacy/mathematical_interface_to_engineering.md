# 수학의 공통 인터페이스에서 공학 모델까지

이 문서는 서로 다른 수학/물리/공학 도메인에서 반복해서 나타나는 구조를 하나의 공통 인터페이스로 통폐합한 문서다.

핵심 관점은 특정 공식이나 분야별 용어를 먼저 외우는 것이 아니라,

> **무엇을 상태로 잡는가 → 어떤 법칙으로 허용되는 상태/운동을 정하는가 → 그 해집합은 어떤 공간구조를 갖는가 → 국소구조가 어떤 동역학을 만드는가 → 대칭과 분해로 어떤 독립 성분을 찾는가 → 스케일을 바꾸면 어떤 유효이론이 남는가 → 실제 공학 모델에서는 무엇을 추가해야 닫히는가**

를 하나의 흐름으로 보는 것이다.

---

# 0. 전체 구조

가장 압축하면 다음과 같다.

$$
\boxed{
\text{대상/관측}
\to
\text{상태공간}
\to
\text{연산자 방정식/변분적 생성/제약}
\to
\text{해집합}
\to
\text{기하/국소구조}
\to
\text{생성자/동역학}
\to
\text{대칭/분해}
\to
\text{축약/스케일링}
\to
\text{폐쇄/경계조건/수치화}
\to
\text{공학 모델}
}
$$

이 흐름은 반드시 일방향은 아니다.

실제 문제에서는

- 관측 데이터에서 상태공간을 추정하기도 하고,
- 방정식에서 변분구조를 역으로 찾기도 하며,
- 동역학에서 보존량을 찾은 뒤 다시 기하를 복원하기도 하고,
- 미시모델에서 거시 유효이론을 만들기도 한다.

따라서 이 문서는 **계층 구조**라기보다 반복해서 왕복할 수 있는 **공통 인터페이스**로 읽는 것이 좋다.

---

# 1. 대상과 관측: 무엇을 기술할 것인가

가장 먼저 정해야 하는 것은 실제 세계나 추상적 문제에서 무엇을 하나의 상태로 볼 것인지다.

상태공간을 바로 정하기 전에 보통 다음 두 종류의 객체가 먼저 등장한다.

$$
X
$$

는 가능한 미시적 대상 또는 configuration들의 집합이다.

그리고 관측량은

$$
A:X\to Y
$$

형태의 map이다.

여기서

- $X$는 상태 후보들의 집합,
- $Y$는 관측값 공간,
- $A$는 상태를 실제 측정 가능한 값으로 보내는 관측 map이다.

같은 시스템이라도 무엇을 관측하느냐에 따라 이후의 모델링이 달라질 수 있다.

## 도메인별 용어

| 도메인 | 대상 | 관측량의 예 |
|---|---|---|
| 고전역학 | 입자의 위치/운동량 | 위치, 속도, 에너지 |
| 장론 | 공간 전체의 장 | 장값, 밀도, flux |
| 회로 | 전기적 상태 | 전압, 전류 |
| 제어 | plant의 내부 상태 | sensor output |
| 확률론 | 확률변수 또는 확률과정 | 기대값, 분산, event |
| 통계역학 | 미시상태 또는 분포 | 에너지, 입자수, 평균 |
| 머신러닝 | parameter/representation/data state | loss, prediction, feature |

여기서부터 이미 중요한 구분이 생긴다.

$$
\text{state}
\neq
\text{observable}
$$

상태는 시스템을 기술하기 위한 내부 변수이고, 관측량은 그 상태에서 읽어내는 함수다.

---

# 2. 상태공간: 가능한 상태들을 어디에 모을 것인가

이제 상태들을 하나의 공간에 모은다.

일반적으로

$$
\mathcal X
$$

를 상태공간이라고 하자.

단순한 경우에는

$$
\mathcal X=\mathbb R^n
$$

일 수 있지만, 실제 수학에서는 다음처럼 훨씬 다양한 구조가 나온다.

- vector space
- manifold
- function space
- measure space
- probability simplex
- Hilbert/Banach space
- phase space
- configuration space
- quotient space

## 2.1 입자와 장의 차이

질점계에서는 상태가 유한차원이다.

$$
q\in Q
$$

여기서 $Q$는 configuration space다.

반면 장에서는 상태 자체가 함수다.

$$
u:\Omega\to V
$$

따라서 상태공간은 함수들의 집합이 된다.

$$
\mathcal X
=
\{u:\Omega\to V\}
$$

즉

$$
\text{finite-dimensional state}
\to
\text{function-valued state}
$$

로 올라간다.

## 2.2 확률론에서는 상태가 분포가 될 수도 있다

확률측도들의 공간을

$$
\mathcal P(X)
=
\{
\mu\mid
\mu\text{ is a probability measure on }X
\}
$$

라고 하자.

통계역학, 확률론, optimal transport, information geometry에서는 개별 점 $x\in X$보다

$$
\mu\in\mathcal P(X)
$$

를 상태로 잡는 경우가 많다.

즉 같은 "상태"라는 말도 도메인마다 층위가 다르다.

| 층위 | 상태 |
|---|---|
| 미시상태 | $x\in X$ |
| 유한차원 상태 | $z\in M$ |
| 장 | $u:\Omega\to V$ |
| 경로 | $\gamma:[0,T]\to X$ |
| 분포 | $\mu\in\mathcal P(X)$ |
| 분포의 경로 | $\mu_\bullet:[0,T]\to\mathcal P(X)$ |

---

# 3. 법칙을 만드는 구조: 어떤 상태가 허용되는가

상태공간만 정하면 가능한 상태가 너무 많다.

따라서 다음 질문이 필요하다.

> **상태공간의 원소들 중 어떤 상태 또는 운동이 실제 법칙을 만족하는가?**

가장 넓은 공통 형식은 연산자 방정식

$$
L_\theta u=f
$$

이다.

정확히는

$$
L_\theta:
D(L_\theta)\subseteq\mathcal X
\to
\mathcal Y
$$

이고

$$
u\in D(L_\theta),
\qquad
f\in\mathcal Y
$$

이다.

여기서

- $\mathcal X$는 상태공간,
- $\mathcal Y$는 방정식의 결과가 사는 공간,
- $D(L_\theta)$는 operator가 정의되는 admissible domain,
- $\theta\in\Theta$는 물성/모델/소자/환경 파라미터,
- $f$는 source, forcing, load, input

이다.

즉 이 문서의 가장 넓은 법칙 인터페이스는

$$
\boxed{
\text{state space}
\to
L_\theta u=f
}
$$

이다.

## 3.1 흔히 보는 방정식은 어떻게 $Lu=f$로 읽는가

겉으로 모양이 다른 식도 미지 상태를 묶고 왼쪽 전체를 하나의 operator로 보면 같은 형식으로 읽힌다.

| 흔한 식 | 미지 상태 | operator $L$ | $Lu=f$ 해석 |
|---|---|---|---|
| $Au=b$ | $u$ | $L=A$ | $Lu=b$ |
| $\dot x=F(x)+g$ | $x$ | $Lx=\dot x-F(x)$ | $Lx=g$ |
| $\partial_tu-\kappa\Delta u=s$ | $u$ | $L=\partial_t-\kappa\Delta$ | $Lu=s$ |
| $\partial_t\rho+\nabla\cdot j=s$ | $(\rho,j)$ | $L(\rho,j)=\partial_t\rho+\nabla\cdot j$ | $L(\rho,j)=s$ |
| $Av=\lambda v$ | $v$ | $L_\lambda=A-\lambda I$ | $L_\lambda v=0$ |
| $\partial_t\rho=L^*\rho$ | $\rho$ | $\widetilde L\rho=\partial_t\rho-L^*\rho$ | $\widetilde L\rho=0$ |

특히 continuity/balance equation

$$
\partial_t\rho+\nabla\cdot j=s
$$

은

$$
L(\rho,j)
=
\partial_t\rho+\nabla\cdot j
$$

라는 operator를 정의한 뒤

$$
L(\rho,j)=s
$$

라고 읽는 것이다.

즉 목적은 서로 다른 미분/대수 관계를 하나의 map $L$의 작용으로 묶어 해집합/스펙트럼/변분/축약을 같은 언어로 다루는 것이다.

## 3.2 제약조건: $Lu=f$의 admissible domain을 줄인다

그런데

$$
Lu=f
$$

만으로는 해가 여러 개 남거나 물리적으로 허용되지 않는 상태까지 포함할 수 있다.

따라서 별도의 constraint operator

$$
C:\mathcal X\to Z
$$

를 두고

$$
C(u)=d
$$

를 요구한다.

전체 문제는

$$
\begin{cases}
Lu=f,\\
C(u)=d.
\end{cases}
$$

가 된다.

그러면 admissible domain은

$$
D_{\rm adm}
=
\{
u\in D(L)
\mid
C(u)=d
\}
$$

이고 실제 해집합은

$$
\mathcal S_{f,d}
=
\{
u\in D(L)
\mid
Lu=f,\ C(u)=d
\}
$$

가 된다.

이 구조는 initial condition, boundary condition, normalization, gauge condition, incompressibility, circuit topology, feasible constraint 등으로 나타난다.

즉

$$
\boxed{
Lu=f
\to
\text{남아 있는 자유도}
\to
C(u)=d
\to
\text{admissible solution set}
}
$$

이다.

## 3.3 변분구조: 특정 $L$을 생성하는 구조

많은 물리계에서는 $L$을 처음부터 주지 않고 functional

$$
\mathcal F:\mathcal A\to\mathbb R
$$

을 먼저 둔다.

핵심 조건은 단순한 minimum이 아니라 **stationarity**다.

$$
D\mathcal F(u)=0
$$

또는

$$
\delta\mathcal F[u]=0
$$

을 요구한다.

그 이유는 변분문제에는 minimum뿐 아니라 maximum과 saddle도 포함되기 때문이다.

변분구조의 공통 흐름은

$$
\boxed{
\mathcal F
\to
D\mathcal F
\to
L_{\mathcal F}
\to
L_{\mathcal F}u=0
}
$$

이다.

| 변분 대상 | 상태공간의 원소 | functional의 예 | stationarity가 주는 것 |
|---|---|---|---|
| 점 | $x\in M$ | $F:M\to\mathbb R$ | $dF_x=0$, critical point |
| 경로 | $\gamma:[t_0,t_1]\to Q$ | action $S[\gamma]$ | Euler--Lagrange ODE |
| 장 | $u:\Omega\times I\to V$ | field action / energy | Euler--Lagrange PDE |
| 분포 | $\mu\in\mathcal P(X)$ | entropy / free energy | equilibrium condition 또는 분포 flow의 구동 functional |

따라서 경로에 대한 action만이 변분구조가 아니다.

점 자체의 최적화에서는

$$
F:M\to\mathbb R
$$

에 대해

$$
dF_x=0
$$

인 critical point를 찾고, 경로/장/분포에서는 같은 구조가 더 높은 차원의 상태공간으로 확장된다.

이제 다음 질문이 생긴다.

> **stationary functional에서 나온 $L$이 실제 시간운동을 만들 때, 보존/소산/확률계는 무엇이 달라지는가?**

# 4. 변분구조의 분류: 보존/소산/구동/확률

앞 절에서 functional로부터 operator equation을 만들 수 있었다.

그런데 그것만으로는 **그 operator가 어떤 종류의 운동을 만드는지** 아직 구별되지 않는다.

따라서 이제 functional과 국소 기하가 결합될 때 동역학이 어떤 유형으로 갈라지는지를 본다.

모든 동역학이 동일한 종류의 변분구조를 갖는 것은 아니다.

공학적으로 중요한 분류는 다음 네 축이다.

$$
\boxed{
\text{conservative}
\quad
\text{dissipative}
\quad
\text{driven}
\quad
\text{stochastic}
}
$$

---

## 4.1 보존계

보존계에서는 보통 Hamiltonian 또는 action 구조가 중심이 된다.

상태공간을 phase space $M$이라 하고 Hamiltonian을

$$
H:M\to\mathbb R
$$

라고 하자.

적절한 symplectic structure가 있으면 Hamiltonian vector field

$$
X_H:M\to TM
$$

가 생성되고

$$
\dot z=X_H(z)
$$

라는 운동을 만든다.

대표 특징은

$$
\frac{d}{dt}H(z_t)=0
$$

같은 보존량이다.

---

## 4.2 소산계

소산계에서는 어떤 functional이 감소한다.

$$
\mathcal F:\mathcal M\to\mathbb R
$$

와 metric $g$가 주어지면 gradient flow는

$$
\dot x_t
=
-\operatorname{grad}_g\mathcal F(x_t)
$$

이다.

따라서 보통

$$
\frac{d}{dt}\mathcal F(x_t)\le 0
$$

가 된다.

이 구조는

- diffusion,
- heat flow,
- optimization,
- dissipative mechanics,
- Wasserstein gradient flow

등에서 반복된다.

---

## 4.3 외부 구동계

실제 공학계는 보존계나 순수 소산계만으로 끝나지 않는다.

일반적으로

$$
\mathcal E(\mathcal L)[u]
=
Q[u,t]
$$

처럼 쓸 수 있다.

왼쪽은 variational/conservative part이고, 오른쪽은

- forcing,
- control input,
- damping,
- source,
- actuator

같은 외부 항이다.

질량--스프링--댐퍼 계에서는

$$
m\ddot q+kq
=
-c\dot q+f(t)
$$

처럼 나타난다.

---

## 4.4 확률계

확률계에서도 상태를 분포로 올리면 앞의 gradient-flow 구조와 연결되는 경우가 있다.

확률분포 공간을

$$
\mathcal P_2(E)
$$

라고 하고 free energy를

$$
\mathcal F:
\mathcal P_2(E)
\to
\mathbb R
$$

라고 하자.

여기에 Wasserstein metric을 주면 적절한 경우

$$
\partial_t\mu_t
=
-\operatorname{grad}_{W_2}\mathcal F(\mu_t)
$$

라는 gradient flow가 Fokker--Planck equation으로 나타난다.

대표적으로 밀도 $\rho_t$에 대해

$$
\partial_t\rho_t
=
\nabla\cdot
\left(
\rho_t\nabla V
\right)
+
\beta^{-1}\Delta\rho_t
$$

가 있고, 이에 대응하는 trajectory 수준의 diffusion SDE는

$$
dX_t
=
-\nabla V(X_t)\,dt
+
\sqrt{2\beta^{-1}}\,dW_t
$$

이다.

따라서 이 계열에서는

$$
\boxed{
\text{free energy}
+
\text{Wasserstein geometry}
\to
\text{Fokker--Planck gradient flow}
\leftrightarrow
\text{diffusion SDE}
}
$$

라는 연쇄가 성립한다.

즉 확률적 동역학은

- trajectory 수준의 random process,
- distribution 수준의 Fokker--Planck/Kolmogorov equation

으로 나뉘지만, reversible diffusion이나 overdamped Langevin 계열에서는 그 distribution dynamics가 다시 변분/gradient-flow 구조에서 나온다.

모든 SDE가 gradient flow에서 나오는 것은 아니므로 이 연결은 해당 구조를 갖는 확률계에 적용한다.

---

# 5. 해집합: 방정식을 만족하는 것들의 공간

연산자 식

$$
F(x)=0
$$

이 주어지면 자연스럽게 해집합을

$$
\mathcal S
=
\{
x\in\mathcal X
\mid
F(x)=0
\}
$$

으로 정의한다.

이 단계부터 중요한 변화가 일어난다.

문제는 더 이상 단순히 "해 하나를 구한다"가 아니라

> **해 전체가 어떤 공간을 이루는가**

로 바뀐다.

---

## 5.1 선형문제

선형사상

$$
A:V\to W
$$

에 대해

$$
\ker A
=
\{
v\in V
\mid
Av=0
\}
$$

는 vector subspace다.

즉 해집합 자체가 선형구조를 가진다.

---

## 5.2 비선형문제

비선형 map

$$
F:M\to N
$$

에 대해

$$
F^{-1}(0)
$$

은 조건이 좋으면 submanifold가 된다.

이 경우 해집합에는

- tangent space,
- local coordinates,
- dimension,
- curvature

같은 기하적 구조가 생긴다.

---

## 5.3 대수적 문제

다항식들의 집합

$$
f_1,\dots,f_k
$$

에 대해

$$
V
=
\{
x
\mid
f_i(x)=0
\}
$$

을 생각하면 algebraic variety가 된다.

여기서는 metric보다

- ideal,
- prime ideal,
- localization,
- local ring,
- spectrum

같은 대수적 국소구조가 중심이 된다.

즉 "해집합의 기하"는 도메인에 따라 다른 방식으로 구현된다.

---

## 5.4 도메인별 해집합과 심화 구조

해집합을 공간으로 보는 것이 실제로 핵심이 되는 대표적인 경우만 정리하면 다음과 같다.

| 분야 | 방정식 | 해집합 | 이어지는 구조 |
|---|---|---|---|
| 선형대수 | $Au=b$ | affine solution space | kernel, image, quotient |
| 고유치/스펙트럼 | $Av=\lambda v$ | eigenspace | spectrum, spectral decomposition |
| ODE/PDE | $Lu=f$ | trajectory 또는 function-space solution set | invariant manifold, weak solution, semigroup |
| 변분법 | $D\mathcal F(u)=0$ | critical set | Hessian, stability, bifurcation |
| 대수기하 | $f_1=\cdots=f_k=0$ | algebraic set | variety, local ring, scheme |
| 확률/통계역학 | $L^*\mu=0$ 또는 equilibrium condition | invariant/equilibrium measures | ergodic decomposition, Gibbs family |
| 정보기하 | parametric model constraints | statistical manifold | Fisher metric, dual affine structure |

다음 단계에서 중요한 것은 해집합에 구조를 많이 얹는 것이 아니라, **그 국소구조가 어떤 생성자/관측량/동역학을 만들어내는가**를 보는 것이다.

# 6. 기하와 국소구조: 국소 데이터가 무엇을 만들어내는가

해집합이나 상태공간에 국소구조를 넣는 목적은 구조 자체를 나열하는 데 있지 않다.

다음 단계의 동역학을 생각하면 핵심 질문은 하나다.

> **점 근처에서 얻은 미분/기하/교환 구조가 어떤 infinitesimal generator나 물리량을 만들어내는가?**

이 절에서는 **국소 데이터 → 생성되는 infinitesimal object**까지만 다룬다.  
그 infinitesimal object를 실제 시간운동, flow, semigroup, group으로 적분하는 일은 7절에서 다룬다.

---

## 6.1 좌표, tangent, cotangent: 변화율을 국소 데이터로 만든다

local chart를

$$
\varphi:
U\subseteq M
\to
\mathbb R^n
$$

라고 하자.

좌표를 잡으면 상태의 작은 변화를 미분할 수 있고, 점

$$
p\in M
$$

에서 tangent space

$$
T_pM
$$

와 cotangent space

$$
T_p^*M
$$

를 얻는다.

함수

$$
F:M\to\mathbb R
$$

의 differential은

$$
dF_p\in T_p^*M
$$

이다.

즉 첫 단계는

$$
\boxed{
\text{local coordinate}
\to
\text{derivative}
\to
dF_p
}
$$

이다.

하지만 $dF_p$는 아직 covector이므로 이것만으로는 실제 운동 방향이 정해지지 않는다.  
다음의 metric, symplectic structure 같은 추가 구조가 covector를 generator로 바꾼다.

---

## 6.2 metric: $dF$를 gradient generator로 바꾼다

Riemannian metric은

$$
g_p:
T_pM\times T_pM
\to
\mathbb R
$$

이다.

metric은

$$
dF_p\in T_p^*M
$$

에 대응하는 vector

$$
\operatorname{grad}_gF(p)\in T_pM
$$

를 정한다.

따라서

$$
\boxed{
dF
+
g
\to
\operatorname{grad}_gF
}
$$

이다.

여기까지가 국소구조의 역할이고, 실제 gradient flow

$$
\dot x=-\operatorname{grad}_gF(x)
$$

는 다음 절에서 이 generator를 시간방정식으로 읽은 것이다.

---

## 6.3 symplectic form과 Poisson bracket: $dH$를 Hamiltonian generator로 바꾼다

symplectic form은 closed nondegenerate $2$-form

$$
\omega\in\Omega^2(M)
$$

이다.

Hamiltonian

$$
H:M\to\mathbb R
$$

가 주어지면

$$
\iota_{X_H}\omega=dH
$$

로 Hamiltonian vector field

$$
X_H:M\to TM
$$

가 정해진다.

즉

$$
\boxed{
dH
+
\omega
\to
X_H
}
$$

이다.

같은 infinitesimal action을 observable 쪽에서 읽으면 Poisson bracket이 나온다.

$$
\{f,H\}
$$

는 observable

$$
f:M\to\mathbb R
$$

에 Hamiltonian generator가 작용한 결과다.

따라서 state-side와 observable-side는

$$
\boxed{
H
\to
X_H
\qquad\Longleftrightarrow\qquad
f
\to
\{f,H\}
}
$$

로 대응한다.

---

## 6.4 vector field의 교환관계: Lie bracket이 새로운 infinitesimal direction을 만든다

두 vector field

$$
X,Y:M\to TM
$$

가 있을 때 Lie bracket

$$
[X,Y]
$$

은 두 infinitesimal transformations의 비가환성을 측정하는 또 하나의 vector field다.

즉

$$
\boxed{
X,Y
\to
[X,Y]
}
$$

로 새로운 infinitesimal direction이 생성된다.

이 구조 때문에 vector field들의 공간은 Lie algebra를 이루며, 제어이론에서는

$$
X_i,
\qquad
[X_i,X_j],
\qquad
[X_i,[X_j,X_k]],
\ldots
$$

를 통해 직접 입력하지 않은 방향까지 생성 가능한지를 본다.

여기서는 **어떤 새로운 infinitesimal generator가 생기는가**까지만 본다.  
이 generator들이 finite transformation이나 reachable flow를 어떻게 만드는지는 7절에서 이어진다.

---

## 6.5 differential form: local differential relation에서 flux와 conservation quantity를 만든다

$k$-form을

$$
\alpha\in\Omega^k(M)
$$

라고 하고 exterior derivative를

$$
d:
\Omega^k(M)
\to
\Omega^{k+1}(M)
$$

라고 하자.

전자기학에서는 potential $1$-form

$$
A
$$

에서 field strength $2$-form

$$
F=dA
$$

를 만들고

$$
dF=d^2A=0
$$

을 얻는다.

여기에 Stokes-type relation을 적용하면 local differential relation이 line/surface/volume integral과 연결된다.

즉 differential form의 핵심 역할은

$$
\boxed{
\text{local differential data}
\to
\text{integrated flux / conserved quantity}
}
$$

이다.

---

## 6.6 정보기하: divergence와 potential의 국소 전개가 1차/2차/3차 구조를 만든다

exponential family를

$$
p_\theta(x)
=
h(x)
\exp
\left(
\langle\theta,T(x)\rangle
-
\psi(\theta)
\right)
$$

라고 하자.

natural coordinate는

$$
\theta\in\Theta
$$

이고 expectation coordinate는

$$
\eta
=
\nabla\psi(\theta)
$$

이다.

또

$$
\eta_i
=
\mathbb E_\theta[T_i(X)]
$$

이며

$$
\nabla^2\psi(\theta)
=
\operatorname{Cov}_{p_\theta}[T(X)]
$$

이다.

따라서 같은 Hessian이

- 정보기하에서는 Fisher metric,
- 통계에서는 covariance,
- 통계역학에서는 fluctuation,
- response theory에서는 susceptibility

로 해석된다.

이 관계를 국소 전개의 차수별로 보면 더 구조적으로 정리된다.

| 국소 차수 | 생성되는 구조 | 통계/물리 해석 |
|---|---|---|
| 0차 | potential / divergence의 값 | free energy, entropy, KL value |
| 1차 | differential, score, gradient, response direction | generalized force, linear response direction |
| 2차 | Hessian, Fisher metric, covariance | fluctuation, susceptibility, local distinguishability |
| 3차 이상 | cubic/higher tensor, connection correction, higher cumulant | skewness, nonlinear response, higher-order fluctuation |

특히 KL divergence의 local expansion은

$$
D_{\rm KL}
(
p_\theta
\Vert
p_{\theta+d\theta}
)
=
\frac12
g_{ij}(\theta)
d\theta^i d\theta^j
+
O(\|d\theta\|^3)
$$

이므로 2차항에서 Fisher metric이 나온다.

반면 3차 이상을 버리지 않으면 단순한 metric geometry를 넘어 connection, asymmetry, higher cumulant, nonlinear response를 구별할 정보가 남는다.

따라서 정보기하의 국소구조는

$$
\boxed{
\psi\ \text{or}\ D
\to
\text{1st-order response}
\to
\text{2nd-order Fisher/covariance}
\to
\text{3rd+-order connection/higher response}
}
$$

라는 계층으로 읽는 것이 좋다.

---

## 6.7 Lie derivative: 이미 얻은 generator가 무엇을 보존하는지 검사한다

vector field

$$
X:M\to TM
$$

가 이미 주어졌다면 tensor field나 differential form이 그 infinitesimal motion 아래 어떻게 변하는지를 Lie derivative

$$
\mathcal L_X
$$

로 측정한다.

$$
\mathcal L_XT=0
$$

이면 $T$는 $X$가 만드는 infinitesimal motion에 대해 invariant하다.

즉

$$
\boxed{
X
\to
\mathcal L_X
\to
\text{infinitesimal invariance test}
}
$$

이다.

이 조건은 7절에서 finite flow로 적분되고, 8절에서 symmetry와 conservation law로 이어진다.

---

## 6.8 국소구조가 만드는 infinitesimal object 요약

| 국소 데이터 | 만들어지는 infinitesimal object | 다음 절에서 전개되는 것 |
|---|---|---|
| $dF+g$ | $\operatorname{grad}_gF$ | gradient ODE/flow |
| $dH+\omega$ | $X_H$ | Hamiltonian flow |
| $X,Y$ | $[X,Y]$ | Lie algebra, group/reachable flow |
| $H$ + Poisson structure | $\{\,\cdot\,,H\}$ | observable evolution |
| differential operator $A$ | infinitesimal generator $A$ | semigroup |
| Markov generator $L$ | infinitesimal stochastic generator | Markov semigroup/FPE |
| $X$ acting on tensor $T$ | $\mathcal L_XT$ | symmetry/invariance |

이 표가 6절과 7절의 역할을 나눈다.

- **6절:** 무엇이 infinitesimal generator를 만드는가.
- **7절:** 그 generator가 어떤 미분방정식, flow, semigroup, group으로 전개되는가.

# 7. 국소 생성자에서 동역학으로: 미분방정식, flow, 군과 반군

6절에서 metric, symplectic form, Lie bracket, differential operator 등으로부터 여러 infinitesimal generator를 얻었다.

이제 이 절의 질문은 다르다.

> **그 infinitesimal generator를 시간에 따라 전개하면 어떤 미분방정식, flow, semigroup, group structure가 생기는가?**

전체 구조는 다음과 같다.

$$
\boxed{
\text{local generator}
\to
\text{differential equation}
\to
\text{finite-time evolution}
}
$$

그리고 finite-time evolution의 합성법칙에 따라 group 또는 semigroup 구조가 나타난다.

---

## 7.1 vector field와 ODE

vector field

$$
X:M\to TM
$$

가 주어지면 trajectory

$$
x:I\to M
$$

는

$$
\dot x(t)=X(x(t))
$$

를 만족한다.

즉

$$
\boxed{
X
\leftrightarrow
\dot x=X(x)
}
$$

로 vector field와 1계 ODE는 같은 local dynamics를 두 방식으로 표현한다.

---

## 7.2 ODE에서 flow와 one-parameter group으로

ODE의 해를 초기값마다 모으면

$$
\Phi_t:M\to M
$$

라는 flow를 얻는다.

$$
\frac{d}{dt}\Phi_t(x)
=
X(\Phi_t(x))
$$

이며, 양/음의 시간으로 모두 전개 가능하면

$$
\Phi_{t+s}
=
\Phi_t\circ\Phi_s,
\qquad
\Phi_0=\operatorname{id}_M
$$

이므로 one-parameter group 구조를 가진다.

따라서

$$
\boxed{
X
\to
\dot x=X(x)
\to
\Phi_t
\to
\text{one-parameter flow/group}
}
$$

이다.

---

## 7.3 Lie algebra에서 Lie group으로

6절의 Lie bracket으로 조직된 infinitesimal generators는 Lie algebra

$$
\mathfrak g
$$

를 이룬다.

Lie group $G$의 identity $e$에서

$$
\mathfrak g=T_eG
$$

이고 exponential map은 schematic하게

$$
\exp:
\mathfrak g
\to
G
$$

로 infinitesimal generator를 finite transformation에 연결한다.

즉

$$
\boxed{
\text{Lie algebra}
\to
\text{exponential/integration}
\to
\text{Lie group action}
}
$$

이다.

이제 8절에서는 이 group action이 원래 법칙이나 functional을 보존하는지를 물어 symmetry를 정의한다.

---

## 7.4 Lie bracket과 제어 trajectory

control-affine system을 schematic하게

$$
\dot x
=
X_0(x)
+
\sum_{i=1}^m
u_i(t)X_i(x)
$$

라고 하자.

6절에서 얻은

$$
X_i,
\quad
[X_i,X_j],
\quad
[X_i,[X_j,X_k]],
\ldots
$$

는 infinitesimal reachable directions다.

7절에서는 이 방향들을 실제 입력 sequence로 합성하여 finite trajectory와 reachable set을 만든다.

즉

$$
\boxed{
\text{Lie-generated directions}
\to
\text{control composition}
\to
\text{reachable motion}
}
$$

이다.

---

## 7.5 Hamiltonian generator에서 Hamiltonian flow로

6절에서

$$
dH+\omega
\to
X_H
$$

를 얻었다.

이제 실제 dynamics는

$$
\dot z=X_H(z)
$$

이고 그 해들이 Hamiltonian flow

$$
\Phi_t^H
$$

를 만든다.

observable 쪽에서는 같은 evolution이

$$
\frac{d}{dt}f
=
\{f,H\}
$$

로 나타난다.

따라서 state evolution과 observable evolution이 같은 generator의 두 표현이다.

---

## 7.6 differential operator에서 evolution PDE와 semigroup으로

함수공간 $X$에서 operator

$$
A:
D(A)\subseteq X
\to
X
$$

가 주어지면 evolution equation은

$$
\frac{d}{dt}u_t
=
Au_t
$$

이다.

적절한 조건 아래에서

$$
T_t:X\to X
$$

라는 semigroup이 생기고

$$
u_t=T_tu_0
$$

로 쓸 수 있다.

시간을 역으로 항상 돌릴 수 없는 dissipative PDE에서는 group이 아니라

$$
T_{t+s}
=
T_tT_s,
\qquad
t,s\ge0
$$

인 semigroup이 자연스럽다.

즉

$$
\boxed{
A
\to
\partial_tu=Au
\to
T_t
\to
\text{semigroup}
}
$$

이다.

---

## 7.7 Markov generator에서 Markov semigroup과 Fokker--Planck로

Markov generator를

$$
L
$$

이라 하면 observable 쪽에는 Markov semigroup

$$
P_t
$$

가 작용한다.

형식적으로

$$
\frac{d}{dt}P_tf
=
LP_tf
$$

이다.

distribution 쪽에는 adjoint operator와 adjoint semigroup이 작용한다.

$$
\partial_t\mu_t
=
L^*\mu_t
$$

$$
\mu_t
=
P_t^*\mu_0
$$

밀도가 존재하면 이것이 Fokker--Planck/Kolmogorov forward equation이 된다.

따라서

$$
\boxed{
L
\to
P_t
\qquad\text{and}\qquad
L^*
\to
P_t^*
\to
\text{distribution evolution}
}
$$

이다.

---

## 7.8 6절에서 8절까지의 연결

전체 관계를 한 번에 쓰면 다음과 같다.

$$
\boxed{
\text{local structure}
\to
\text{infinitesimal generator}
\to
\text{ODE/PDE}
\to
\text{flow/group/semigroup}
\to
\text{symmetry and invariants}
}
$$

예를 들면

$$
dH+\omega
\to
X_H
\to
\dot z=X_H(z)
\to
\Phi_t^H
\to
\text{Hamiltonian symmetry/conservation},
$$

$$
dF+g
\to
-\operatorname{grad}_gF
\to
\dot x=-\operatorname{grad}_gF
\to
\Phi_t
\to
\text{dissipative invariance/Lyapunov structure},
$$

$$
A
\to
\partial_tu=Au
\to
T_t
\to
\text{semigroup symmetry/spectral structure}
$$

처럼 같은 골격이 반복된다.

# 8. 대칭과 불변량: 운동에서 변하지 않는 것은 무엇인가

동역학이 정해지면 다음 질문은

> 어떤 변환을 해도 법칙이 같고, 어떤 양이 운동을 따라 보존되는가?

이다.

group $G$가 상태공간 $M$에 작용한다고 하자.

$$
\alpha:G\times M\to M
$$

이 작용이 동역학과 compatible하면 symmetry가 된다.

---

## 8.1 Noether 구조

action

$$
S
$$

가 연속 대칭을 가지면 conserved quantity

$$
J:M\to\mathbb R
$$

가 생긴다.

동역학 vector field를 $X$라 하면

$$
X[J]=0
$$

이다.

따라서 trajectory는 level set

$$
J^{-1}(c)
$$

안에 갇힌다.

---

## 8.2 장론의 local conservation law

장론에서는 global conserved quantity보다 local density와 flux가 더 자연스럽다.

밀도를

$$
\rho:\Omega\times\mathbb R\to\mathbb R
$$

flux를

$$
j:\Omega\times\mathbb R\to\mathbb R^d
$$

source를

$$
s:\Omega\times\mathbb R\to\mathbb R
$$

라고 하면 balance law는

$$
\partial_t\rho
+
\nabla\cdot j
=
s
$$

이다.

특히

$$
s=0
$$

이면 conservation law다.

---

# 9. 분해: 복잡한 운동을 독립적인 성분으로 쪼개기

대칭과 동역학을 그대로 보면 여러 자유도가 서로 섞여 있어서 계산하기 어렵다.

그래서 다음 질문이 필요하다.

> **operator나 symmetry가 서로 섞지 않는 최소 단위의 mode는 무엇인가?**

이 목적은 유한차원에서는 고유치분해로 시작하고, 무한차원에서는 spectral theory, 대칭군 전체를 보면 representation theory, translation symmetry까지 가면 harmonic analysis로 확장된다.

$$
\boxed{
\text{eigenvalue decomposition}
\to
\text{spectral theory}
\to
\text{representation theory}
\to
\text{harmonic analysis}
}
$$

---

## 9.1 고유값 분해

선형 operator

$$
A:V\to V
$$

에 대해 eigenvector $v$는

$$
Av=\lambda v
$$

를 만족한다.

이 경우 $A$의 작용은 $v$ 방향에서는 scalar multiplication으로 단순화된다.

즉 eigenvector는 operator가 더 이상 성분을 섞지 않는 기본 mode다.

---

## 9.2 spectral theory

고유치분해를 무한차원 operator까지 확장하면 spectral theory가 필요하다.

self-adjoint operator의 경우 형식적으로

$$
A
=
\int_{\sigma(A)}
\lambda\,dE(\lambda)
$$

처럼 볼 수 있다.

여기서

$$
\sigma(A)
$$

는 spectrum이고 $E$는 spectral measure다.

이 단계가 필요한 이유는 무한차원에서는 discrete eigenvalue만으로 operator 전체를 분해할 수 없는 경우가 있기 때문이다.

즉

$$
\boxed{
\text{finite eigenmodes}
\to
\text{discrete + continuous spectrum}
}
$$

으로 확장된다.

---

## 9.3 representation theory

이제 operator 하나가 아니라 symmetry group 전체가 상태공간에 작용한다고 하자.

representation을

$$
\rho:
G
\to
GL(V)
$$

라고 한다.

그러면 $V$를 $G$가 보존하는 invariant subspace, 더 나아가 irreducible representation으로 분해한다.

즉

> operator 하나의 eigenmode decomposition

을

> symmetry group 전체의 simultaneous decomposition

으로 일반화한 것이다.

---

## 9.4 harmonic analysis와 Fourier decomposition

translation group처럼 연속적인 대칭이 있으면 그 irreducible mode가 exponential/Fourier mode로 나타난다.

Fourier transform

$$
\mathcal F:
f
\mapsto
\widehat f
$$

은 translation-invariant differential operator를 frequency별 multiplication으로 바꾼다.

예를 들어

$$
D
=
\frac{d}{dt}
$$

에 대해

$$
De^{st}
=
s e^{st}
$$

이므로 exponential mode에서는 미분연산자가 scalar $s$로 바뀐다.

즉

$$
\boxed{
\text{differential operator}
\to
\text{eigenmode}
\to
\text{frequency-wise multiplication}
}
$$

이다.

---

## 9.5 Laplace transform: 미분방정식에서 대수적 해집합으로

제어이론과 회로에서는 이 구조를 Laplace transform으로 적극적으로 사용한다.

polynomial differential operator를

$$
P(D)
=
a_nD^n+\cdots+a_1D+a_0I
$$

라고 하자.

exponential mode $e^{st}$에 작용시키면

$$
P(D)e^{st}
=
P(s)e^{st}
$$

가 된다.

따라서 homogeneous differential equation

$$
P(D)u=0
$$

의 mode를 찾는 문제는

$$
P(s)=0
$$

이라는 polynomial equation으로 바뀐다.

root set은

$$
V(P)
=
\{
s\in\mathbb C
\mid
P(s)=0
\}
$$

이다.

즉 time-domain에서는 함수공간의 미분연산자 문제였던 것이 transform domain에서는 polynomial의 영점 문제로 내려간다.

여러 변수 PDE에서는 symbol $P(\xi)$를 사용하여

$$
V(P)
=
\{
\xi
\mid
P(\xi)=0
\}
$$

같은 characteristic set을 본다.

이 때문에

- 원래 공간에서는 differential/function-space geometry,
- transform domain에서는 spectral/polynomial zero-set geometry

라는 두 표현을 연결해서 볼 수 있다.

엄밀히 모든 pole set을 곧바로 scheme으로 취급해야 한다는 뜻은 아니지만, polynomial symbol과 그 공통 영점집합은 자연스럽게 대수기하적 언어로 확장될 수 있다.

LTI system에서

$$
P(D)y
=
Q(D)u
$$

에 Laplace transform을 적용하면 초기조건을 별도로 처리한 뒤

$$
P(s)Y(s)
=
Q(s)U(s)
$$

를 얻고 transfer function은

$$
G(s)
=
\frac{Y(s)}{U(s)}
=
\frac{Q(s)}{P(s)}
$$

가 된다.

따라서

- $P(s)=0$: pole/mode,
- $Q(s)=0$: zero,
- $G(s)$: rational input-output operator

가 된다.

그래서 제어와 system theory에서 state-space와 Laplace-domain은 같은 LTI dynamics의 두 표현이다.

$$
\boxed{
\text{state-space dynamics}
\leftrightarrow
\text{Laplace / pole / transfer-function algebra}
}
$$

impulse response, pole, mode, transfer function도 이 변환 아래에서 같은 operator structure의 서로 다른 표현으로 연결된다.

# 10. 스케일과 유효이론: 어떤 mode를 남길 것인가

앞 절에서 복잡한 상태나 operator를 mode로 분해했다.

그러면 다음 질문이 자연스럽다.

> **관심 있는 스케일에서 모든 mode를 유지해야 하는가?**

실제 거시현상에서는 short-scale/high-frequency mode를 하나하나 추적하지 않고도 long-scale/low-frequency dynamics를 기술할 수 있는 경우가 많다.

따라서 목표는 원래 dynamics 전체를 그대로 계산하는 것이 아니라 **관심 스케일에서 닫힌 effective dynamics를 얻는 것**이다.

## 10.1 effective dynamics

원래 dynamics를 schematic하게

$$
\partial_tu
=
\mathcal L u
$$

라고 하자.

multiscale decomposition을 통해

$$
u
=
u_{\rm coarse}
+
u_{\rm fine}
$$

로 나눈 뒤 coarse component가

$$
\partial_tu_{\rm coarse}
=
\mathcal L_{\rm eff}u_{\rm coarse}
+
\text{effective correction}
$$

처럼 자체적인 유효 방정식을 따르도록 만드는 것이 목표다.

즉

$$
\boxed{
\text{full dynamics}
\to
\text{scale separation}
\to
\text{effective dynamics}
}
$$

이다.

## 10.2 Littlewood--Paley / multiscale decomposition 관점

조화해석에서는 함수를 dyadic frequency band로 분해할 수 있다.

schematic하게

$$
u
=
\sum_{j\in\mathbb Z}\Delta_j u
$$

라고 쓰자.

여기서 $\Delta_j$는 대략

$$
|\xi|\sim 2^j
$$

의 mode를 남기는 frequency-localization operator다.

따라서

- 작은 $j$: low-frequency / large-scale component,
- 큰 $j$: high-frequency / small-scale component

로 읽을 수 있다.

이 구조의 목적은 단순한 Fourier decomposition보다 한 단계 더 나아가

> **어느 scale의 mode가 어느 scale의 mode와 상호작용하는가**

를 추적하는 것이다.

따라서 nonlinear PDE, turbulence, RG, multiscale modeling에서

$$
\boxed{
\text{frequency decomposition}
\to
\text{scale-by-scale interaction}
\to
\text{relevant scale selection}
}
$$

이라는 관점이 생긴다.

## 10.3 RG: high-frequency mode의 효과를 낮은 스케일 이론에 흡수한다

field를 cutoff $\Lambda$를 기준으로

$$
u
=
u_{<\Lambda}
+
u_{>\Lambda}
$$

로 나누자.

여기서

- $u_{<\Lambda}$는 low-frequency / long-wavelength mode,
- $u_{>\Lambda}$는 high-frequency / short-wavelength mode

다.

RG에서는 $u_{>\Lambda}$를 제거하거나 적분하되 그 효과를 그냥 버리지 않고, 남아 있는 coupling이나 coefficient를 바꾸는 방식으로 흡수한다.

즉

$$
\boxed{
\text{mode decomposition}
\to
\text{high-frequency elimination}
\to
\text{coupling renormalization}
\to
\text{low-frequency effective theory}
}
$$

이다.

theory/model들의 공간을

$$
\mathcal T
$$

라고 하고 scale transformation을

$$
R_\ell:
\mathcal T\to\mathcal T
$$

라고 하면 RG는 상태 하나의 시간운동이 아니라

$$
T
\mapsto
R_\ell(T)
$$

라는 이론 자체의 scale-flow를 본다.

fixed point

$$
R_\ell(T_*)=T_*
$$

는 scale change에도 같은 form을 유지하는 effective theory를 나타낸다.

# 11. 공학으로 내려갈 때 추가되는 구조

앞 단계까지는 법칙의 구조, 해집합의 기하, 동역학, 대칭, mode, scaling을 얻었다.

그런데 실제 공학에서는 이것만으로 계산 가능한 모델이 완성되지 않는 경우가 많다.

왜냐하면 실제 물질의 응답, 장치의 기하, 입력과 경계, 남길 mode, 계산 방법을 아직 정하지 않았기 때문이다.

따라서 공학으로 내려가는 목적과 필요의 연쇄는

$$
\boxed{
\text{field/operator law}
\to
\text{balance}
\to
\text{constitutive closure}
\to
\text{geometry/constraints}
\to
\text{mode reduction}
\to
\text{IC/BC}
\to
\text{discretization}
\to
\text{engineering model}
}
$$

로 보는 것이 자연스럽다.

순수수학이나 이론물리의 구조만으로 실제 공학모델이 완성되는 경우는 드물다.

보통 다음 네 요소가 추가된다.

$$
\boxed{
\text{closure}
+
\text{geometry/constraints}
+
\text{IC/BC}
+
\text{discretization}
}
$$

---

## 11.1 constitutive closure

balance law만으로는 새로운 미지량이 생겨 방정식 수가 부족할 수 있다.

예를 들어

$$
\partial_t\rho
+
\nabla\cdot j
=
s
$$

에서 $j$가 아직 미지라면

$$
j
=
\mathcal C(\rho,\nabla\rho,\ldots)
$$

라는 constitutive relation을 추가해야 한다.

이것이 물질/매질의 구체적인 성질을 넣는 단계다.

예:

- Newtonian fluid의 stress law
- Fourier heat conduction
- Ohm's law
- material constitutive model

---

## 11.2 geometry와 kinematic constraint

실제 공학계에서는 공간 영역

$$
\Omega\subseteq\mathbb R^d
$$

자체가 문제의 일부다.

또한

- rigid constraint,
- incompressibility,
- contact,
- joint,
- circuit topology

같은 구조가 들어간다.

---

## 11.3 initial/boundary condition

differential equation만으로 해가 하나로 결정되지 않는다.

ODE에서는 initial state

$$
x(0)=x_0
$$

를 주고,

PDE에서는 boundary condition

$$
B(u)|_{\partial\Omega}=g
$$

를 추가한다.

이 단계에서 동일한 differential operator라도 서로 다른 실제 공학문제가 된다.

---

## 11.4 discretization과 계산

연속 operator를 실제 컴퓨터에서 계산하기 위해 finite-dimensional approximation으로 내린다.

예를 들어

$$
\mathcal L u=f
$$

를

$$
A_hu_h=f_h
$$

로 바꾼다.

여기서

- $h$는 discretization scale,
- $u_h$는 finite-dimensional state,
- $A_h$는 matrix/operator approximation이다.

이 단계부터 numerical stability, condition number, timestep, solver architecture 등이 중요해진다.

---

## 11.5 전자기장부터 회로까지: 장을 저차원 mode로 줄이는 예

전자기학에서 회로이론으로 내려가는 과정은 위 연쇄의 대표적인 예다.

전자기 상태는

$$
E,B:\Omega\to\mathbb R^3
$$

또는 potential $A$로 기술된다.

장 energy는

$$
U_{\rm EM}
=
\int_\Omega
\left[
\frac{\varepsilon}{2}|E|^2
+
\frac{1}{2\mu}|B|^2
\right]
dx
$$

이다.

아직 이 단계에서는 공간 전체의 field가 자유도이므로 무한차원 모델이다.

전압과 자속은 이 field를 기하적인 chain 위에 적분해서 얻는다.

$$
V_{ab}
=
-\int_a^bE\cdot dl
$$

$$
\Phi
=
\int_SB\cdot dS
$$

Faraday law는

$$
\oint_{\partial S}E\cdot dl
=
-
\frac{d}{dt}
\int_SB\cdot dS
$$

로 line integral과 surface integral을 연결한다.

그런데 실제 회로에서는 공간 전체의 field를 매 순간 풀고 싶지 않다.

그래서 소자 크기 $\ell$가 전자기파 파장보다 충분히 작다는 quasistatic/lumped 조건

$$
\ell\ll\lambda_{\rm EM}
$$

아래에서 field의 공간적 모양을 거의 고정하고 amplitude만 남긴다.

커패시터에서는

$$
E(x,t)
\approx
V(t)e_C(x)
$$

인덕터에서는

$$
B(x,t)
\approx
I(t)b_L(x)
$$

라고 본다.

그러면 원래 field energy가

$$
U_E
\to
\frac12CV^2
$$

$$
U_B
\to
\frac12LI^2
$$

로 내려간다.

즉

$$
\boxed{
\text{3D field}
\to
\text{dominant spatial mode}
\to
\text{time-dependent amplitude}
\to
C,L
}
$$

이다.

여기서 $C,L$은 장의 공간분포와 기하를 적분해 얻은 effective coefficient로 볼 수 있다.

한 LC loop에서 generalized coordinate를 charge

$$
q:\mathbb R\to\mathbb R
$$

라고 하고

$$
I=\dot q
$$

라고 두면

$$
L_{\rm LC}
=
\frac12L\dot q^2
-
\frac{q^2}{2C}
$$

라는 유한차원 Lagrangian을 얻는다.

Euler--Lagrange equation은

$$
L\ddot q+\frac1Cq=0
$$

이다.

따라서

$$
q\leftrightarrow x,
\qquad
I\leftrightarrow\dot x,
\qquad
L\leftrightarrow m,
\qquad
C^{-1}\leftrightarrow k
$$

라는 역학-회로 대응이 생긴다.

저항을 넣으면 dissipation이 추가되어 RLC model로 내려간다.

즉 전자기학에서 회로로 가는 과정은

$$
\boxed{
\text{field variational law}
\to
\text{Maxwell/balance}
\to
\text{geometry}
\to
\text{lumped mode reduction}
\to
\text{effective coefficients}
\to
\text{finite-dimensional circuit dynamics}
}
$$

로 정리할 수 있다.

---

# 12. 도메인별 번역표

## 12.1 핵심 객체

| 공통 인터페이스 | 고전역학 | 장론/유체 | 회로 | 제어 | 확률과정 | 통계역학 | 머신러닝 |
|---|---|---|---|---|---|---|---|
| 상태 | $(q,p)$ | $u(x,t)$ | capacitor voltage / inductor current | state vector | $X_t$ 또는 law | microstate / distribution | parameter / representation |
| 상태공간 | phase space | function space | state space | state space | measurable state space | phase/probability space | parameter/model space |
| 법칙 | Hamilton/EL | PDE | KCL/KVL + device law | state equation | SDE/generator | Liouville/Fokker--Planck | update rule/gradient flow |
| functional | action/Hamiltonian | action/free energy | energy | cost | entropy/rate functional | entropy/free energy | loss |
| 국소구조 | tangent/symplectic | tangent/function derivative | local linearization | Jacobian | generator | Fisher/Wasserstein geometry | Hessian/Fisher |
| 동역학 | flow | PDE flow | transient response | controlled flow | Markov semigroup | relaxation/transport | optimization trajectory |
| 대칭 | canonical symmetry | spacetime symmetry | time invariance | system symmetry | invariant measure | conservation/statistical symmetry | parameter symmetry |
| 분해 | normal mode | Fourier mode | transfer mode | controllable/observable mode | spectral decomposition | fluctuation modes | eigenspaces/features |
| 축약 | effective coordinates | reduced PDE | equivalent circuit | model reduction | coarse Markov model | coarse graining/RG | low-rank/mean-field |
| 공학 추가 | force/model | constitutive law + BC | component model | actuator/sensor constraints | calibration | equation of state | architecture/data/optimizer |

---

# 13. 상태와 functional의 이름이 도메인마다 어떻게 바뀌는가

특히 혼동이 많은 것이 상태와 변분 functional이다.

## 13.1 상태

| 공통 의미 | 도메인별 이름 |
|---|---|
| 시스템을 순간적으로 지정하는 최소 정보 | state |
| 위치만 | configuration |
| 위치+운동량 | phase-space state |
| 공간마다 값을 가지는 상태 | field |
| 확률분포 자체 | probability measure / law |
| 제어계 내부 변수 | state vector |
| 학습계 변수 | parameters / weights |

## 13.2 functional

| 역할 | 이름 |
|---|---|
| 실제 경로 선택 | action |
| 보존계의 에너지 생성자 | Hamiltonian |
| 평형/열역학 선택 | free energy |
| 무질서/정보량 평가 | entropy |
| 최적화 목표 | objective / loss / cost |
| 제어 성능 평가 | value / cost functional |
| 확률경로 희귀성 평가 | rate functional |

중요한 점은 이름이 달라도 모두

$$
\mathcal F:\mathcal A\to\mathbb R
$$

형태의 functional로 볼 수 있다는 것이다.

하지만 **모든 functional이 동일한 역할을 하는 것은 아니다.**

action은 stationary path를 고르고,

free energy는 equilibrium 또는 dissipative flow를 고르며,

loss는 optimization target을 정한다.

따라서 "functional"이라는 공통 타입과 "물리적 역할"을 구분해야 한다.

---

# 14. 전체를 한 번에 보는 최소 공통 골격

최종적으로 가장 보편적인 구조만 남기면 다음과 같다.

상태공간

$$
\mathcal X
$$

을 잡는다.

허용되는 상태 또는 운동을 가장 넓게는 operator equation으로 정의한다.

$$
F:\mathcal X\to\mathcal Y
$$

많은 물리계에서는 이 operator가 functional

$$
\mathcal F:\mathcal A\to\mathbb R
$$

의 변분에서 생성되고, constraint는 operator equation의 admissible domain을 제한한다.

그 결과 해집합

$$
\mathcal M
=
\{x\in\mathcal X:F(x)=0\}
$$

이 생긴다.

$\mathcal M$에 topology, smooth structure, metric, symplectic form, measure, local ring 등 필요한 구조를 얹는다.

한 점 근처의 local information으로 generator를 만든다.

$$
G
$$

이 generator가 global dynamics

$$
\Phi_t
$$

또는 semigroup

$$
T_t
$$

을 만든다.

대칭과 spectrum을 이용해 invariant component 또는 mode로 분해한다.

그 뒤 projection/coarse graining으로 effective model을 만든다.

마지막으로 실제 공학에서는

$$
\text{constitutive law}
+
\text{geometry}
+
\text{IC/BC}
+
\text{numerical realization}
$$

을 추가해 계산 가능한 모델로 내린다.

즉 가장 압축된 공통 인터페이스는

$$
\boxed{
\begin{aligned}
&
\text{State}
\\
&\downarrow
\\
&
\text{Operator Law / Variational Generation / Constraint}
\\
&\downarrow
\\
&
\text{Solution Space}
\\
&\downarrow
\\
&
\text{Geometry / Local Structure}
\\
&\downarrow
\\
&
\text{Generator / Dynamics}
\\
&\downarrow
\\
&
\text{Symmetry / Decomposition}
\\
&\downarrow
\\
&
\text{Reduction / Effective Scale}
\\
&\downarrow
\\
&
\text{Closure / BC / Computation}
\\
&\downarrow
\\
&
\text{Engineering Model}
\end{aligned}
}
$$

이다.

---

# 15. 이 문서를 읽을 때의 핵심 구분

마지막으로 다음 네 가지는 서로 섞지 않는 것이 중요하다.

### 1. 상태공간과 해집합

$$
\mathcal M\subseteq\mathcal X
$$

상태공간은 가능한 상태 전체이고, 해집합은 법칙을 만족하는 상태들의 부분집합이다.

### 2. 해집합의 기하와 동역학

해집합이 manifold라는 것과 그 위에 vector field가 있다는 것은 다른 구조다.

$$
\text{geometry}
\neq
\text{dynamics}
$$

### 3. generator와 flow

generator는 순간적인 infinitesimal law이고, flow/semigroup은 그것을 시간 방향으로 적분한 global evolution이다.

$$
\text{generator}
\to
\text{flow/semigroup}
$$

### 4. 공통 타입과 도메인별 역할

Hamiltonian, free energy, loss, entropy는 모두 real-valued functional일 수 있지만 물리적 역할은 서로 다르다.

따라서 통합은

> **같은 수학적 타입은 공통 인터페이스로 묶고, 서로 다른 의미와 추가구조는 도메인별 열로 남기는 방식**

으로 해야 한다.

### 5. 연산자 방정식과 변분구조

변분구조는 연산자 방정식과 별개의 최상위 법칙 유형이라기보다, 특정 operator equation을 생성하는 구조다.

$$
\text{functional}
\to
\text{variational derivative}
\to
\text{operator equation}
$$

balance law 역시 operator equation의 한 형태이고, 제약은 그 방정식의 admissible domain과 해집합을 제한한다.

이것이 수학의 공통 인터페이스에서 실제 공학 모델로 내려가는 가장 안정적인 통합 구조다.
