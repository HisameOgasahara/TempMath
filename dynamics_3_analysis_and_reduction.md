# 3. 동역학을 분석하고 축약하기

앞의 두 글에서는 동역학을 정의하고, 같은 동역학을 state, observable, probability measure, function에서 표현했다.

이 글의 질문은 두 개다.

> 정해진 동역학에서 어떤 mode와 spectrum을 찾을 수 있는가?

> 모든 자유도를 추적하지 않고 더 작은 dynamical system을 만들 수 있는가?

첫 질문은 analysis, 둘째 질문은 reduction으로 나눈다.

# Part I. analysis

## 1. linear operator와 semigroup

finite-dimensional vector space $\mathbb R^n$에서

$$
\dot x(t)
=
Ax(t)
$$

를 생각하자.

- $A:\mathbb R^n\to\mathbb R^n$: linear operator
- $x(t)\in\mathbb R^n$: state

solution은

$$
x(t)
=
e^{tA}x_0
$$

이다.

operators

$$
T_t=e^{tA}
$$

는

$$
T_0=I,
\qquad
T_{t+s}=T_tT_s
$$

를 만족한다.

이 성질을 가진 family를 **semigroup**이라고 한다.

함수공간 $\mathcal X$에서도

$$
\frac{d}{dt}u(t)
=
Au(t)
$$

를 생각할 수 있다.

$A$가 적절한 operator이면 strongly continuous semigroup $\{T_t\}_{t\ge0}$가 존재하여

$$
u(t)
=
T_tu_0
$$

로 쓸 수 있다.

## 2. generator

strongly continuous semigroup $\{T_t\}_{t\ge0}$의 **infinitesimal generator** $A$는

$$
Au
=
\lim_{t\downarrow0}
\frac{T_tu-u}{t}
$$

가 존재하는 $u$에 대해 정의한다.

generator의 domain은

$$
D(A)
=
\left\{
u\in\mathcal X:
\lim_{t\downarrow0}
\frac{T_tu-u}{t}
\text{ exists}
\right\}
$$

이다.

## 3. eigenvalue, eigenvector, spectrum

linear operator $A$의 **eigenvalue** $\lambda$와 **eigenvector** $v\neq0$는

$$
Av
=
\lambda v
$$

를 만족한다.

그러면

$$
T_tv
=
e^{\lambda t}v
$$

이므로 $\operatorname{Re}\lambda$는 해당 mode의 성장 또는 감쇠와 연결된다.

**resolvent set**은

$$
\rho(A)
=
\left\{
\lambda\in\mathbb C:
\lambda I-A
\text{ is bijective and has bounded inverse}
\right\}
$$

이고 **spectrum**은

$$
\sigma(A)
=
\mathbb C\setminus\rho(A)
$$

이다.

## 4. resolvent와 Laplace transform

$\lambda\in\rho(A)$에서 **resolvent operator**는

$$
R(\lambda,A)
=
(\lambda I-A)^{-1}
$$

이다.

적절한 half-plane에서

$$
R(\lambda,A)u
=
\int_0^\infty
e^{-\lambda t}T_tu\,dt
$$

로 semigroup과 연결된다.

finite-dimensional control system

$$
\dot x
=
Ax+Bu,
\qquad
y=Cx
$$

를 Laplace transform하면

$$
(sI-A)\widehat x(s)
=
x_0+B\widehat u(s)
$$

이고

$$
\widehat x(s)
=
R(s,A)x_0
+
R(s,A)B\widehat u(s).
$$

zero initial condition에서는 **transfer function**

$$
G(s)
=
CR(s,A)B
$$

를 얻는다.

## 5. Fourier transform과 differential operator

함수

$$
u:\mathbb R^d\to\mathbb C
$$

의 Fourier transform을

$$
\widehat u(\xi)
=
\int_{\mathbb R^d}
e^{-ix\cdot\xi}
u(x)\,dx
$$

로 두자.

충분히 smooth하고 decay가 좋은 함수에 대해

$$
\widehat{\partial_j u}(\xi)
=
i\xi_j\widehat u(\xi).
$$

따라서 constant-coefficient differential operator $P(\partial)$는

$$
\widehat{P(\partial)u}(\xi)
=
P(i\xi)\widehat u(\xi)
$$

라는 multiplication으로 바뀐다.

## 6. polynomial과 differential equation

$$
P(D)u=0,
\qquad
D=\frac{d}{dt}
$$

를 생각하자.

$$
P(D)e^{st}
=
P(s)e^{st}
$$

이므로 $P(s)=0$의 root가 exponential mode를 정한다.

root $\lambda$의 multiplicity가 $r$이면

$$
e^{\lambda t},
\,
te^{\lambda t},
\,
\dots,
\,
t^{r-1}e^{\lambda t}
$$

형태의 generalized modes가 나타난다.

## 7. module로 linear operator를 읽기

finite-dimensional complex vector space $E$와 linear operator

$$
A:E\to E
$$

가 있다고 하자.

polynomial ring $\mathbb C[\zeta]$가 $E$에

$$
p(\zeta)\cdot v
:=
p(A)v
$$

로 작용하게 만들면 $E$는 $\mathbb C[\zeta]$-module이 된다.

**annihilator**

$$
\operatorname{Ann}_{\mathbb C[\zeta]}(E)
=
\left\{
p\in\mathbb C[\zeta]:
p(A)=0
\right\}
$$

는 finite-dimensional case에서 minimal polynomial $m_A$가 생성하는 ideal과 같다.

$$
\operatorname{Ann}(E)
=
(m_A).
$$

**support**는

$$
\operatorname{Supp}_{\mathbb C[\zeta]}(E)
=
\left\{
\mathfrak p\in\operatorname{Spec}\mathbb C[\zeta]:
E_{\mathfrak p}\neq0
\right\}
$$

로 정의한다.

한 generalized eigenspace에서

$$
A
=
\lambda I+N,
\qquad
N^r=0
$$

이면

$$
R(s,A)
=
\frac{I}{s-\lambda}
+
\frac{N}{(s-\lambda)^2}
+
\cdots
+
\frac{N^{r-1}}{(s-\lambda)^r}.
$$

eigenvalue, minimal polynomial의 factor, resolvent의 pole order, nilpotent part가 같은 generalized eigenstructure와 연결된다.

## 8. Lyapunov function과 stability

nonlinear system

$$
\dot x
=
X(x)
$$

을 생각하자.

equilibrium $x_*$는

$$
X(x_*)=0
$$

을 만족한다.

함수

$$
V:M\to\mathbb R
$$

가 equilibrium 근처에서

$$
V(x_*)=0,
\qquad
V(x)>0
\quad
(x\neq x_*)
$$

이고 trajectory를 따라

$$
\dot V(x)
=
dV_x[X(x)]
\le0
$$

이면 $V$를 stability analysis에 사용하는 **Lyapunov function**으로 삼을 수 있다.

### 질량–스프링–댐퍼

$$
m\ddot q
+
c\dot q
+
kq
=
0,
\qquad
m,c,k>0
$$

에서 state를

$$
x=(q,\dot q)\in\mathbb R^2
$$

로 두고

$$
V(q,\dot q)
=
\frac12m\dot q^2
+
\frac12kq^2
$$

로 두면

$$
\dot V
=
-c\dot q^2
\le0.
$$

## 9. invariant set, attractor, basin of attraction

flow $\Phi_t$에 대해 set $S\subseteq M$이

$$
\Phi_t(S)=S
$$

를 만족하면 **invariant set**이라고 한다.

asymptotically stable equilibrium $x_*$로 수렴하는 initial states의 집합

$$
\mathcal B(x_*)
=
\left\{
x_0\in M:
\Phi_t(x_0)\to x_*
\text{ as }t\to\infty
\right\}
$$

을 **basin of attraction**이라고 한다.

질량–스프링–댐퍼에서 $m,c,k>0$이면 equilibrium $(q,\dot q)=(0,0)$이 attractor가 되는 대표적인 경우다.

# Part II. reduction

## 10. closure

전체 state를

$$
z=(x,y)
$$

로 나누자.

전체 system은

$$
\dot x
=
f(x,y),
\qquad
\dot y
=
g(x,y)
$$

라고 하자.

$x$만으로 닫힌 equation

$$
\dot x
=
\bar f(x)
$$

을 얻고 싶지만 일반적으로 같은 $x$라도 $y$가 다르면 $\dot x$가 달라질 수 있다.

따라서 reduction의 핵심 문제는 **closure**이다.

## 11. quotient와 symmetry reduction

Lie group $G$가 manifold $M$에 작용한다고 하자.

같은 group orbit에 놓인 states를 하나로 묶으면 quotient

$$
M/G
$$

를 생각할 수 있다.

dynamics가 group action과 compatible하면 quotient 위에 reduced dynamics를 정의할 수 있다.

## 12. invariant manifold, center manifold, slow manifold

submanifold $N\subseteq M$이 vector field $X$에 대해

$$
X(x)\in T_xN
\qquad
\text{for every }x\in N
$$

을 만족하면 $N$은 **invariant manifold**이다.

**center manifold**는 equilibrium 근처에서 linearization의 center eigenspace에 tangent인 local invariant manifold이다.

**slow manifold**는 fast-slow system에서 slow dynamics를 담는 invariant 또는 approximately invariant manifold를 뜻한다.

본문에서는 equilibrium 근처 또는 clear time-scale separation이 있는 경우만 생각한다.

## 13. modal truncation

$$
u(t)
=
\sum_{j=1}^{\infty}
c_j(t)\phi_j
$$

에서 처음 $k$개 mode만 남기면

$$
u(t)
\approx
\sum_{j=1}^{k}
c_j(t)\phi_j
$$

가 된다.

이것이 **modal truncation**이다.

## 14. Koopman invariant subspace

observable space에서

$$
\mathcal V
=
\operatorname{span}
\{\phi_1,\dots,\phi_k\}
$$

가 Koopman generator $\mathcal L$에 대해 invariant이고

$$
\mathcal L\phi_i
=
\sum_{j=1}^{k}
B_{ij}\phi_j
$$

이면 finite-dimensional closed observable dynamics를 얻는다.

## 15. moment closure

moments를

$$
m_i(t)
=
\int_M
\phi_i(x)\,d\mu_t(x)
$$

로 정의하면

$$
\dot m_i(t)
=
\int_M
\mathcal L\phi_i(x)\,d\mu_t(x).
$$

오른쪽이 retained moments만으로 표현되지 않으면 higher moments를 retained moments의 함수로 근사하는 **moment closure**가 필요하다.

## 16. finite-dimensional family of probability measures

$$
\left\{
\mu_\theta:
\theta\in\Theta\subseteq\mathbb R^k
\right\}
$$

만 남기고

$$
\mu_t
\approx
\mu_{\theta(t)}
$$

로 둘 수 있다.

projection rule을 정할 때 Fisher metric이나 Wasserstein metric을 사용할 수 있다.

## 17. HJ/HJB function approximation

$$
S(t,q)
\approx
\sum_{j=1}^{k}
a_j(t)\phi_j(q)
$$

또는

$$
V(t,x)
\approx
\sum_{j=1}^{k}
b_j(t)\psi_j(x)
$$

로 function space의 degrees of freedom을 줄일 수 있다.

## 18. Mori--Zwanzig와 generalized Langevin equation

대표적인 generalized Langevin equation은

$$
m\ddot q(t)
=
-\nabla U_{\mathrm{eff}}(q(t))
-
\int_0^t
K(t-s)\dot q(s)\,ds
+
\eta(t)
+
f_{\mathrm{ext}}(t).
$$

- $q(t)\in\mathbb R^d$: retained position
- $U_{\mathrm{eff}}:\mathbb R^d\to\mathbb R$: effective potential
- $K:[0,\infty)\to\mathbb R^{d\times d}$: memory kernel
- $\eta(t)\in\mathbb R^d$: fluctuating force
- $f_{\mathrm{ext}}(t)\in\mathbb R^d$: external force

memory kernel이 짧은 시간에 빠르게 decay하고 그 시간 동안 velocity가 거의 변하지 않는다고 가정하면

$$
\int_0^t
K(t-s)\dot q(s)\,ds
\approx
\left(
\int_0^\infty K(\tau)\,d\tau
\right)
\dot q(t).
$$

scalar case에서

$$
\gamma
=
\int_0^\infty K(\tau)\,d\tau
$$

라고 두면 memory term은

$$
-\gamma\dot q(t)
$$

로 근사된다.

## 19. fluctuation--dissipation relation

thermal equilibrium의 대표적인 generalized Langevin model에서는 적절한 normalization 아래

$$
\mathbb E[\eta(t)\eta(s)^\top]
\propto
K(|t-s|)
$$

형태의 **fluctuation--dissipation relation**이 나타난다.

electrical circuit에서는 resistor의 dissipation과 Johnson--Nyquist noise가 같은 물리적 연결의 예이다.

## 20. mass--spring, LC, RLC

ideal mass--spring system은

$$
m\ddot q+kq=0
$$

이고

$$
E_{\mathrm{mech}}
=
\frac12m\dot q^2
+
\frac12kq^2.
$$

ideal LC circuit은

$$
L\ddot Q+\frac{1}{C}Q=0
$$

이고

$$
E_{\mathrm{LC}}
=
\frac12L\dot Q^2
+
\frac{Q^2}{2C}.
$$

dissipation과 external forcing을 포함하면

$$
m\ddot q
+
c\dot q
+
kq
=
f(t)
$$

및

$$
L\ddot Q
+
R\dot Q
+
\frac{1}{C}Q
=
V_{\mathrm{ext}}(t)
$$

가 된다.

각 energy의 derivative는

$$
\frac{dE_{\mathrm{mech}}}{dt}
=
-c\dot q^2
+
f(t)\dot q
$$

및

$$
\frac{dE_{\mathrm{LC}}}{dt}
=
-R\dot Q^2
+
V_{\mathrm{ext}}(t)\dot Q
$$

이다.

phenomenological damping을 직접 넣은 model과 더 큰 system에서 environment variables를 제거한 effective model은 구분해야 한다.

## 21. coarse graining과 renormalization group

field $u$를

$$
u
=
u_{\mathrm{coarse}}
+
u_{\mathrm{fine}}
$$

로 나누고 fine-scale degrees of freedom을 제거하여

$$
\partial_tu_{\mathrm{coarse}}
=
\mathcal L_{\mathrm{eff}}
u_{\mathrm{coarse}}
+
\text{effective terms}
$$

를 얻는 것을 **coarse graining**이라고 부른다.

Littlewood--Paley decomposition에서는

$$
u
=
\sum_{j\in\mathbb Z}
\Delta_j u
$$

처럼 scale별 성분을 나눈다.

**renormalization group**에서는 degrees of freedom을 제거하는 것에 더해 scale transformation을 수행하고 coupling constants가 scale에 따라 어떻게 변하는지 추적한다.

RG flow는 physical time에 대한 flow와 같은 개념이 아니다.

## 22. 분석과 축약의 연결

analysis는 어떤 성분이 있는지 찾는다.

$$
\text{generator}
\longrightarrow
\text{spectrum}
\longrightarrow
\text{modes}
$$

reduction은 그 가운데 무엇을 남길지 정한다.

$$
\text{full system}
\longrightarrow
\text{retained variables or modes}
\longrightarrow
\text{reduced system}
$$

# 정확한 정의와 조건

## strongly continuous semigroup

Banach space $\mathcal X$ 위의 bounded linear operators $\{T_t\}_{t\ge0}$가

$$
T_0=I,
\qquad
T_{t+s}=T_tT_s
$$

를 만족하고 모든 $u\in\mathcal X$에 대해

$$
\lim_{t\downarrow0}
\|T_tu-u\|_{\mathcal X}
=
0
$$

이면 strongly continuous semigroup 또는 $C_0$-semigroup이라 한다.

## infinitesimal generator

$$
Au
=
\lim_{t\downarrow0}
\frac{T_tu-u}{t}
$$

로 정의되며 limit가 존재하는 $u$들의 집합이 domain $D(A)$이다.

## invariant manifold

submanifold $N\subseteq M$이 flow $\Phi_t$에 대해 정의되는 모든 $t$에서

$$
\Phi_t(N)\subseteq N
$$

을 만족하면 positively invariant라 하고, 양·음의 time 모두에서 equality가 성립하면 invariant라 한다.

## attractor

여기서는 metric space의 continuous semiflow $\Phi_t$에 대해 compact invariant set $\mathcal A$가 어떤 neighborhood $U$를 attract한다는 의미로 사용한다.

$$
d(\Phi_t(U),\mathcal A)
\to0
\qquad
(t\to\infty).
$$

## quotient reduction

Lie group action이 proper하고 free이면 quotient $M/G$가 smooth manifold가 되는 표준적인 충분조건을 얻는다.

## center manifold

equilibrium의 linearization에서 spectrum을 stable, center, unstable parts로 분리할 수 있고 필요한 smoothness 조건이 성립하면 center eigenspace에 tangent한 local invariant center manifold가 존재한다.

## Mori--Zwanzig

정확한 identity는 observable evolution의 Liouville operator와 projection operator를 사용하여 Markov term, memory integral, orthogonal dynamics term으로 분해한다. 본문의 generalized Langevin equation은 그 결과의 대표적인 physical form이다.

## Littlewood--Paley decomposition

tempered distribution $u$에 대해 frequency-space dyadic partition of unity를 사용하여 operators $\Delta_j$를 정의하고

$$
u
=
\sum_{j\in\mathbb Z}
\Delta_j u
$$

를 distributional sense에서 해석한다.
