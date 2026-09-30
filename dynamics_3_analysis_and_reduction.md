# 동역학에서 무엇을 읽고 무엇을 줄이는가

앞의 두 글에서 동역학과 그 여러 표현을 얻었다.

이제 질문은 두 단계로 바뀐다.

> 정해진 동역학에서 어떤 mode와 time scale을 읽을 수 있는가?

> 그 정보를 이용해 어떤 자유도를 남기고 어떤 자유도를 제거할 수 있는가?

따라서 이 글은

$$
\boxed{
\text{analysis}
\longrightarrow
\text{reduction}
}
$$

의 순서로 간다.

# 1. analysis: operator에서 mode를 읽기

가장 단순한 linear system

$$
\dot x=Ax
$$

에서 시작한다.

- $A:\mathbb R^n\to\mathbb R^n$: linear operator
- $x(t)\in\mathbb R^n$: state

solution은

$$
x(t)=e^{tA}x_0
$$

이다.

따라서 finite-time evolution operator를

$$
T_t=e^{tA}
$$

라고 쓰면

$$
T_{t+s}=T_tT_s,
\qquad
T_0=I
$$

를 만족한다.

함수공간에서도 같은 관계를 가지는 $\{T_t\}_{t\ge0}$를 **semigroup**으로 사용한다.

그 infinitesimal generator $A$는

$$
Au
=
\lim_{t\downarrow0}
\frac{T_tu-u}{t}
$$

로 정의한다.

즉

$$
\boxed{
\text{generator }A
\longrightarrow
\text{semigroup }T_t
}
$$

가 순간 변화와 유한시간 변화를 연결한다.

## 2. eigenvalue와 spectrum이 time scale을 드러낸다

eigenvalue $\lambda$와 eigenvector $v\neq0$가

$$
Av=\lambda v
$$

를 만족하면

$$
T_tv=e^{\lambda t}v.
$$

따라서 $\operatorname{Re}\lambda$는 해당 mode의 성장 또는 감쇠 속도와 연결된다.

finite dimension을 넘으면 eigenvalue만으로 충분하지 않으므로 **spectrum**

$$
\sigma(A)
$$

을 사용한다.

resolvent set은

$$
\rho(A)
=
\left\{
\lambda\in\mathbb C:
\lambda I-A
\text{ is bijective and has bounded inverse}
\right\}
$$

이고

$$
\sigma(A)
=
\mathbb C\setminus\rho(A)
$$

이다.

resolvent operator는

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

이므로 Laplace transform이 semigroup과 resolvent를 연결한다.

## 3. Fourier와 Laplace는 같은 동역학을 mode별로 읽게 한다

constant-coefficient differential operator를 생각하자.

함수

$$
u:\mathbb R^d\to\mathbb C
$$

의 Fourier transform을

$$
\widehat u(\xi)
=
\int_{\mathbb R^d}
e^{-ix\cdot\xi}u(x)\,dx
$$

로 두면

$$
\widehat{\partial_j u}(\xi)
=
i\xi_j\widehat u(\xi).
$$

따라서

$$
\widehat{P(\partial)u}(\xi)
=
P(i\xi)\widehat u(\xi)
$$

가 된다.

즉 differential operator가 frequency별 multiplication으로 바뀐다.

time direction에서도

$$
P(D)u=0,
\qquad
D=\frac{d}{dt}
$$

에 대해

$$
P(D)e^{st}=P(s)e^{st}
$$

이므로 polynomial root가 exponential mode를 정한다.

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

가 나타난다.

## 4. module은 같은 generalized eigenstructure를 대수적으로 기록한다

finite-dimensional complex vector space $E$와 linear operator

$$
A:E\to E
$$

가 있을 때

$$
p(\zeta)\cdot v
=
p(A)v
$$

로 $\mathbb C[\zeta]$가 $E$에 작용하게 하면 $E$는 $\mathbb C[\zeta]$-module이 된다.

annihilator는

$$
\operatorname{Ann}_{\mathbb C[\zeta]}(E)
=
\left\{
p\in\mathbb C[\zeta]:
p(A)=0
\right\}
$$

이고 finite-dimensional case에서는 minimal polynomial $m_A$에 대해

$$
\operatorname{Ann}(E)=(m_A)
$$

이다.

한 generalized eigenspace에서

$$
A=\lambda I+N,
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

따라서 eigenvalue, minimal polynomial, Jordan structure, resolvent pole이 같은 linear structure를 서로 다른 방식으로 기록한다.

여기까지가 첫 번째 analysis이다.

$$
\boxed{
A
\longrightarrow
T_t
\longrightarrow
\sigma(A)
\longrightarrow
\text{modes and time scales}
}
$$

# 5. nonlinear dynamics에서는 stability와 invariant set을 본다

nonlinear system

$$
\dot x=X(x)
$$

에서 equilibrium $x_*$는

$$
X(x_*)=0
$$

을 만족한다.

equilibrium 근처에서 function

$$
V:M\to\mathbb R
$$

가

$$
V(x_*)=0,
\qquad
V(x)>0
\quad
(x\neq x_*)
$$

이고

$$
\dot V(x)
=
dV_x[X(x)]
\le0
$$

이면 $V$를 **Lyapunov function**으로 사용한다.

### 질량–스프링–댐퍼

$$
m\ddot q+c\dot q+kq=0,
\qquad
m,c,k>0
$$

에서

$$
V(q,\dot q)
=
\frac12m\dot q^2
+
\frac12kq^2
$$

로 두면

$$
\dot V=-c\dot q^2\le0.
$$

이 example에서는 energy 감소가 equilibrium으로 향하는 dynamics를 분석하는 데 쓰인다.

flow $\Phi_t$에 대해 set $S\subseteq M$이

$$
\Phi_t(S)=S
$$

를 만족하면 **invariant set**이다.

equilibrium $x_*$로 수렴하는 initial states의 집합은

$$
\mathcal B(x_*)
=
\left\{
x_0\in M:
\Phi_t(x_0)\to x_*
\text{ as }t\to\infty
\right\}
$$

이고 이를 **basin of attraction**이라고 한다.

따라서 linear spectrum과 nonlinear stability analysis는 모두 어떤 성분이 빨리 사라지고 무엇이 오래 남는지 알려준다.

이제 reduction으로 넘어갈 수 있다.

# 6. reduction의 질문은 closure이다

전체 state를

$$
z=(x,y)
$$

로 나누자.

- $x$: 남길 variables
- $y$: 제거할 variables

전체 system이

$$
\dot x=f(x,y),
\qquad
\dot y=g(x,y)
$$

일 때 $x$만으로

$$
\dot x=\bar f(x)
$$

를 만들고 싶다.

하지만 같은 $x$에서도 $y$가 다르면 $\dot x$가 달라질 수 있다. 따라서 reduction의 핵심은 **closure**가 가능한지 보는 것이다.

## 7. exact하게 닫히는 경우: quotient와 invariant manifold

Lie group $G$가 manifold $M$에 작용하고 dynamics가 그 action과 compatible하면 quotient

$$
M/G
$$

에 reduced dynamics를 내릴 수 있다.

또 submanifold $N\subseteq M$이

$$
X(x)\in T_xN
\qquad
(x\in N)
$$

을 만족하면 $N$은 **invariant manifold**이다.

$N$에서 시작한 integral curve는 $N$에 남기 때문에 $\dim N<\dim M$이면 더 작은 state space에서 dynamics를 기술할 수 있다.

equilibrium 근처의 **center manifold**와 time-scale separation이 있는 system의 **slow manifold**가 이 방향의 대표적인 예다.

## 8. mode를 선택해서 줄이는 경우: modal truncation

analysis에서 mode를 찾았다면 일부만 남길 수 있다.

$$
u(t)
=
\sum_{j=1}^{\infty}
c_j(t)\phi_j
$$

에서

$$
u(t)
\approx
\sum_{j=1}^{k}
c_j(t)\phi_j
$$

로 두는 것이 **modal truncation**이다.

Fourier modes, eigenmodes, POD modes 등을 사용할 수 있다.

linear invariant subspace를 남기면 exact할 수 있지만 nonlinear coupling이 있으면 일반적으로 approximation과 closure가 필요하다.

Koopman generator에서도

$$
\mathcal V
=
\operatorname{span}
\{\phi_1,\dots,\phi_k\}
$$

가 invariant하고

$$
\mathcal L\phi_i
=
\sum_{j=1}^{k}
B_{ij}\phi_j
$$

이면 finite-dimensional observable dynamics가 닫힌다.

## 9. probability measure를 줄이는 경우: moment closure와 finite-dimensional family

probability measure $\mu_t$에서 moments

$$
m_i(t)
=
\int_M
\phi_i(x)\,d\mu_t(x)
$$

를 남기면

$$
\dot m_i(t)
=
\int_M
\mathcal L\phi_i(x)\,d\mu_t(x).
$$

오른쪽이 retained moments만으로 표현되지 않으면 higher moments를 retained moments의 함수로 근사한다. 이것이 **moment closure**이다.

또 probability measure 전체 대신

$$
\{\mu_\theta:\theta\in\Theta\subseteq\mathbb R^k\}
$$

만 남겨

$$
\mu_t\approx\mu_{\theta(t)}
$$

로 둘 수 있다.

이때 projection을 정할 때 Fisher metric이나 Wasserstein metric을 사용할 수 있다. 따라서 정보기하와 수송기하는 여기서는 distribution reduction의 geometry로 다시 등장한다.

## 10. function을 줄이는 경우: HJ/HJB approximation

Hamilton--Jacobi function과 value function도 function space의 원소이므로 finite basis로 줄일 수 있다.

$$
S(t,q)
\approx
\sum_{j=1}^{k}
a_j(t)\phi_j(q)
$$

및

$$
V(t,x)
\approx
\sum_{j=1}^{k}
b_j(t)\psi_j(x).
$$

여기서 줄이는 것은 state dimension이 아니라 function space의 degrees of freedom이다.

## 11. 제거한 variables의 영향이 남는 경우: Mori--Zwanzig

closure가 exact하지 않으면 제거한 $y$의 영향이 사라지지 않는다.

Mori--Zwanzig formalism에서는 projection을 사용하여 그 영향을 memory term과 orthogonal dynamics term으로 남긴다.

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
- $K:[0,\infty)\to\mathbb R^{d\times d}$: memory kernel
- $\eta(t)\in\mathbb R^d$: fluctuating force

memory가 짧고 그 시간 동안 velocity가 거의 변하지 않는다고 가정하면

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

라고 두면

$$
-\int_0^tK(t-s)\dot q(s)\,ds
\approx
-\gamma\dot q(t)
$$

가 된다.

thermal equilibrium에서는 적절한 조건 아래 memory kernel과 fluctuating force의 covariance가 **fluctuation--dissipation relation**으로 연결된다.

## 12. mass--spring과 RLC는 effective model의 익숙한 예다

ideal mass--spring system은

$$
m\ddot q+kq=0
$$

이고 energy는

$$
E_{\mathrm{mech}}
=
\frac12m\dot q^2
+
\frac12kq^2.
$$

damping과 forcing을 넣으면

$$
m\ddot q+c\dot q+kq=f(t)
$$

이고

$$
\frac{dE_{\mathrm{mech}}}{dt}
=
-c\dot q^2+f(t)\dot q.
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

RLC와 external voltage를 포함하면

$$
L\ddot Q+R\dot Q+\frac{1}{C}Q
=
V_{\mathrm{ext}}(t)
$$

및

$$
\frac{dE_{\mathrm{LC}}}{dt}
=
-R\dot Q^2
+
V_{\mathrm{ext}}(t)\dot Q.
$$

$damping$이나 $resistance$를 phenomenological term으로 직접 넣은 model과, 더 큰 system에서 variables를 제거하여 얻은 effective term은 같은 유도과정이 아니다.

## 13. scale 자체를 바꾸는 reduction: coarse graining과 RG

field $u$를

$$
u=u_{\mathrm{coarse}}+u_{\mathrm{fine}}
$$

로 나누고 fine-scale degrees of freedom을 제거하여 coarse variables의 effective dynamics를 만드는 것이 **coarse graining**이다.

Littlewood--Paley decomposition에서는

$$
u
=
\sum_{j\in\mathbb Z}
\Delta_j u
$$

처럼 frequency scale별로 나눌 수 있다.

**renormalization group**에서는 degrees of freedom을 제거한 뒤 scale transformation까지 수행하고 coupling constants가 scale에 따라 어떻게 변하는지 추적한다.

따라서 RG flow는 physical time에 대한 flow와 같은 것이 아니다.

# 14. 전체 연결

이 글의 흐름은 다음 하나로 정리된다.

$$
\boxed{
\begin{array}{c}
\text{generator or vector field}\\
\downarrow\\
\text{spectrum, modes, stability, invariant sets}\\
\downarrow\\
\text{retained variables or retained modes}\\
\downarrow\\
\text{closure}\\
\downarrow\\
\text{reduced dynamics}
\end{array}
}
$$

spectrum과 stability analysis는 무엇을 남길지 판단하는 정보를 주고, reduction에서는 실제로 variables, modes, moments, probability family, function basis를 줄인다. exact closure가 되지 않으면 memory나 effective terms가 필요하다.

---

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
\|T_tu-u\|_{\mathcal X}=0
$$

이면 $C_0$-semigroup이라고 한다.

## invariant manifold

submanifold $N\subseteq M$이 flow $\Phi_t$에 대해 정의되는 시간 동안

$$
\Phi_t(N)\subseteq N
$$

을 만족하면 positively invariant이다. vector field 수준에서는

$$
X(x)\in T_xN
$$

이 local invariance를 주는 표준 조건이다.

## attractor

여기서는 continuous semiflow $\Phi_t$에 대해 compact invariant set $\mathcal A$가 어떤 neighborhood $U$를 attract하는 경우를 사용한다.

$$
d(\Phi_t(U),\mathcal A)\to0
\qquad
(t\to\infty).
$$

## quotient manifold

Lie group action이 free이고 proper이면 quotient $M/G$가 smooth manifold가 되는 표준적인 충분조건을 얻는다.

## center manifold

equilibrium의 linearization에서 stable, center, unstable spectral subspaces가 분리되고 필요한 smoothness 조건이 성립하면 center eigenspace에 tangent한 local invariant center manifold가 존재한다.
