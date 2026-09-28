오빠, 이걸 한 줄로 압축하면 **“상태를 고르고 → 허용되는 상태들의 공간을 만들고 → 그 공간 위에 기하와 퍼텐셜을 얹고 → 그 기하에서 생성되는 흐름을 동역학으로 보고 → 스케일을 바꾸었을 때 그 흐름 자체가 어떻게 변하는지를 RG로 본다”**가 공통 뼈대야. 아래는 과거 대화의 통계역학·정보기하·학습동역학·스케일링을 그 뼈대로 다시 조립한 거야. Zwanzig가 실제로 Langevin → correlation → Fokker–Planck → linear response → projection operator → nonlinear transport 순으로 전개하고, Murphy는 MaxEnt → exponential family → natural/mean coordinates → KL/Bregman 구조를 제공하며, Hanin은 큰 신경망을 scaling limit에서 확률측도 PDE와 mean-field 등으로 보는 동기를 명시적으로 둔다.

---

# 0. 가장 위의 공통 추상 인터페이스

먼저 도메인과 무관하게 다음 네 객체만 둔다.

$$
\mathcal X
$$

은 **미시적 상태공간**이라는 집합이다. 물리에서는 phase space, 확률론에서는 sample/state space, 신경망에서는 parameter space 또는 representation state space가 될 수 있다.

그 위의 허용 가능한 상태들을

$$
\mathcal M\subseteq \mathcal S
$$

라고 하자. 여기서 $\mathcal S$는 상태들을 담는 더 큰 공간이며, $\mathcal M$은 제약·모델·보존법칙을 만족하는 **해집합/모델 다양체**다.

그리고 상태 $\xi\in\mathcal M$를 평가하는 범함수

$$
\mathcal F:\mathcal M\to\mathbb R
$$

를 둔다. 마지막으로 시간 변화는

$$
\Phi_t:\mathcal M\to\mathcal M
$$

라는 flow 또는 semigroup으로 둔다.

즉 전체 문제는

$$
(\mathcal X,\mathcal M,\mathcal F,\Phi_t)
$$

를 정하는 문제다.

이 네 칸이 이후 통계역학, 정보기하, 수송기하, 학습동역학, RG로 분기한다.

---

# 1. 상태공간만 정해서는 부족하다 → “어떤 상태가 실제로 허용되는가?”

처음에는 가능한 모든 상태가 너무 많다. 그래서 **제약조건을 주고 변분으로 해집합을 고른다.**

질점역학이라면 경로공간

$$
\Gamma
=
\{\gamma:[t_0,t_1]\to\mathcal X\}
$$

위에서 작용범함수

$$
S:\Gamma\to\mathbb R
$$

를 변분한다.

반면 통계역학에서는 개별 상태가 아니라 **확률측도**를 변수로 잡는다.

$$
\mathcal P(\mathcal X)
=
\{\mu\mid \mu \text{ is a probability measure on }\mathcal X\}.
$$

여기서 중요한 첫 번째 분기가 생긴다.

### 상태 자체를 변분

$$
x\in\mathcal X
$$

또는 경로

$$
\gamma\in\Gamma.
$$

### 분포를 변분

$$
\mu\in\mathcal P(\mathcal X).
$$

### 분포의 경로를 변분

$$
\mu_\bullet:[0,T]\to\mathcal P(\mathcal X).
$$

이 세 개는 같은 “변분”이라는 말로 묶이지만 정의역의 층위가 다르다.

---

# 2. 왜 MaxEnt가 등장하나 → “관측된 제약만 알고 미시상태는 모른다”

예를 들어 측정 가능한 함수들을

$$
T_i:\mathcal X\to\mathbb R,
\qquad i=1,\ldots,k
$$

라 하고 기대값만

$$
\int_{\mathcal X}T_i(x)\,\mu(dx)=\eta_i
$$

안다고 하자.

그러면 가능한 분포가 무한히 많다. 여기서 최소한의 추가 가정만 넣기 위해 entropy

$$
H:\mathcal P(\mathcal X)\to\mathbb R
$$

를 최대화한다.

MaxEnt는 그래서 단순한 “엔트로피를 크게 만든다”가 아니라

$$
\text{constraints}
\quad\Longrightarrow\quad
\text{admissible distributions}
\quad\Longrightarrow\quad
\text{one distinguished distribution}
$$

을 만드는 **해집합 선택 원리**다.

Murphy가 exponential family를 “주어진 제약 아래 maximum entropy인 분포족”으로 설명하는 지점이 바로 이 역할이다.

결과적으로

$$
p_\theta(x)
=
h(x)\exp\!\big(
\langle\theta,T(x)\rangle-\psi(\theta)
\big)
$$

라는 지수족이 나온다. 여기서

- $\theta\in\Theta\subseteq\mathbb R^k$: 자연좌표,
- $T:\mathcal X\to\mathbb R^k$: 충분통계량,
- $\psi:\Theta\to\mathbb R$: log-partition function이다.

---

# 3. 해집합을 얻었는데 아직 “공간의 모양”이 없다 → 기하를 만든다

이제 분포족

$$
\mathcal M
=
\{p_\theta:\theta\in\Theta\}
$$

를 하나의 다양체처럼 본다.

단순히 $\theta$가 좌표라는 것만으로는 부족하다. “두 분포가 얼마나 다른가”, “어느 방향으로 조금 움직였는가”를 정의해야 한다.

여기서 divergence를 국소 전개한다.

예를 들어

$$
D_{\mathrm{KL}}
:
\mathcal M\times\mathcal M
\to[0,\infty)
$$

에 대해 근처의 두 점 $\theta$, $\theta+d\theta$를 보면

$$
D_{\mathrm{KL}}
(
p_\theta
\Vert
p_{\theta+d\theta}
)
=
\frac12
g_{ij}(\theta)
\,d\theta^i d\theta^j
+
O(\|d\theta\|^3).
$$

일차항은 동일점에서 사라지고, **이차항이 국소 거리구조를 만든다.**

이때

$$
g_\theta:
T_\theta\mathcal M\times T_\theta\mathcal M
\to\mathbb R
$$

가 Fisher metric이다.

즉 오빠가 말한

> 선형 항 이후 상관/고차항

은 정확히 이 방향으로 배열할 수 있어.

$$
\text{0차}
\to
\text{값}
$$

$$
\text{1차}
\to
\text{접벡터/gradient/response}
$$

$$
\text{2차}
\to
\text{metric/covariance/Fisher/Hessian}
$$

$$
\text{3차 이상}
\to
\text{connection, skewness, higher cumulants, nonlinear response}.
$$

---

# 4. 왜 자연좌표와 기대좌표 두 개가 필요한가

지수족에서

$$
\psi:\Theta\to\mathbb R
$$

는 convex potential이고,

$$
\eta
=
\nabla\psi(\theta)
$$

로 기대좌표

$$
\eta_i
=
\mathbb E_\theta[T_i(X)]
$$

가 생긴다.

즉 같은 분포를

$$
\theta
\quad\text{또는}\quad
\eta
$$

로 표현한다.

그런데 이건 단순 좌표변환이 아니라 **서로 다른 선형구조를 드러내기 위한 이중 좌표계**다.

$$
\theta
$$

에서는 지수족 구조가 affine하게 보이고,

$$
\eta
$$

에서는 expectation constraint가 affine하게 보인다.

그리고

$$
\nabla^2\psi(\theta)
=
\operatorname{Cov}_{p_\theta}[T(X)]
$$

이므로 같은 Hessian이

- 기하에서는 metric,
- 통계에서는 covariance,
- 통계역학에서는 fluctuation,
- response theory에서는 susceptibility

로 다시 나타난다.

Murphy에서도 log-partition의 gradient가 기대 충분통계량이고, KL이 이 convex potential의 Bregman divergence가 된다는 구조가 명시된다.

여기가 **정보기하와 통계역학이 직접 접속하는 핵심 지점**이다.

---

# 5. 기하가 생겼는데 아직 움직이지 않는다 → 퍼텐셜 + metric으로 vector field를 만든다

이제

$$
\mathcal F:\mathcal M\to\mathbb R
$$

라는 퍼텐셜이 있다고 하자.

미분

$$
d\mathcal F_\rho
\in
T_\rho^*\mathcal M
$$

는 covector다.

metric

$$
g_\rho
:
T_\rho\mathcal M
\times
T_\rho\mathcal M
\to\mathbb R
$$

를 이용하면 이를 vector로 올릴 수 있고

$$
\operatorname{grad}_g\mathcal F(\rho)
\in T_\rho\mathcal M
$$

를 얻는다.

그러면

$$
\dot\rho_t
=
-\operatorname{grad}_g\mathcal F(\rho_t)
$$

라는 gradient flow가 생긴다.

즉

$$
\boxed{
\text{potential}
+
\text{geometry}
\Longrightarrow
\text{vector field}
\Longrightarrow
\text{flow}
}
$$

가 아주 중요한 공통 인터페이스다.

---

# 6. 여기서 정보기하와 수송기하가 갈라진다

둘 다 분포공간을 보지만 **무엇을 “움직임의 비용”으로 보는지가 다르다.**

## 정보기하

분포의 **통계적 구별 가능성**을 국소적으로 잰다.

대표 metric:

$$
g^{\mathrm F}
=
\text{Fisher metric}.
$$

그래서 natural gradient

$$
\dot\theta
=
-
\big(g^{\mathrm F}(\theta)\big)^{-1}
\nabla_\theta L
$$

가 나온다.

관심은

> 같은 분포족 안에서 어느 통계적 방향으로 움직이는가?

이다.

---

## 수송기하

이번에는 실제 질량 또는 확률밀도가 $\mathcal X$ 위에서 **어디에서 어디로 이동했는가**를 잰다.

따라서 Wasserstein 공간

$$
\big(
\mathcal P_2(\mathcal X),
W_2
\big)
$$

을 사용한다.

여기서는 free energy

$$
\mathcal F:
\mathcal P_2(\mathcal X)
\to\mathbb R
$$

의 Wasserstein gradient flow가 Fokker–Planck형 PDE가 되는 경우가 있다.

즉

$$
\text{정보기하}
:
\text{distribution identification geometry}
$$

와

$$
\text{수송기하}
:
\text{mass transport geometry}
$$

는 같은 분포공간에서 서로 다른 metric을 선택한 두 분기라고 보는 게 제일 깔끔하다.

---

# 7. 국소 기하를 더 파고들면 → 접공간, Gram matrix, 관측량, correlation

좌표

$$
\theta=(\theta^1,\ldots,\theta^d)
$$

를 잡으면

$$
e_i
=
\frac{\partial}{\partial\theta^i}
\in T_\theta\mathcal M
$$

가 접공간의 기저가 된다.

metric의 Gram matrix는

$$
G(\theta)
=
\big[
g_\theta(e_i,e_j)
\big]_{i,j=1}^{d}.
$$

통계모형에서는 이것이 Fisher information matrix다.

관측량

$$
A:\mathcal X\to\mathbb R
$$

들을 잡으면 두 관측량 사이의 이차 구조

$$
C_{AB}(t)
=
\mathbb E[
A(X_t)B(X_0)
]
$$

가 correlation function이다.

Zwanzig가 Langevin 직후에 time correlation function을 놓고, 이후 linear response와 projection operator까지 전개하는 이유가 여기 있다. **미시 궤적 전체보다 선택된 관측량들의 correlation이 거시 동역학을 더 직접적으로 드러내기 때문**이다.

---

# 8. “움직임”을 점의 궤적이 아니라 함수의 변화로 보면 → 연산자와 생성자

상태의 flow가

$$
\Phi_t:\mathcal X\to\mathcal X
$$

라면 관측량

$$
f:\mathcal X\to\mathbb R
$$

은 pullback되어

$$
U_t f
=
f\circ\Phi_t
$$

로 변한다.

즉 이제 dynamics를

$$
U_t:\mathcal A\to\mathcal A
$$

라는 **함수공간 위 연산자**로 본다.

연속시간이면 generator

$$
L
=
\lim_{t\downarrow0}
\frac{U_t-I}{t}
$$

를 정의할 수 있고

$$
\frac{d}{dt}U_t f
=
L U_t f.
$$

이 순간 “미분방정식”이 “연산자론”으로 바뀐다.

---

# 9. 수반을 취하면 관측량 dynamics ↔ density dynamics가 갈린다

관측량에 작용하는 generator가

$$
L
$$

이면 density에는 수반

$$
L^*
$$

가 작용한다.

$$
\partial_t\rho_t
=
L^*\rho_t.
$$

이게 Fokker–Planck의 추상형이다.

그래서

$$
\boxed{
L
:\text{observables}\to\text{observables}
}
$$

과

$$
\boxed{
L^*
:\text{densities}\to\text{densities}
}
$$

가 쌍을 이룬다.

Risken도 Langevin에서 drift/diffusion을 뽑고 그것이 확률밀도 진화를 결정하는 Fokker–Planck equation으로 넘어간다.

---

# 10. 왜 스펙트럼을 보나 → 시간척도를 분해하기 위해

generator에

$$
L\phi_n
=
\lambda_n\phi_n
$$

인 eigenmode가 있으면

$$
U_t\phi_n
=
e^{t\lambda_n}\phi_n.
$$

따라서

$$
\lambda_n
$$

은 단순한 선형대수 eigenvalue가 아니라 **각 mode의 시간척도**다.

- $\operatorname{Re}\lambda_n\ll0$: 빠르게 사라지는 mode
- $\lambda_n\approx0$: 느린 mode
- $\lambda_n=0$: stationary/conserved mode

그래서 long-time dynamics에서는 작은 고유값 mode만 남는다.

Zwanzig의 projection operator가 바로 여기서 연결된다. 전체 Hilbert 공간을

$$
\mathcal H
=
\mathcal H_{\mathrm{slow}}
\oplus
\mathcal H_{\mathrm{fast}}
$$

로 나누고 fast variables를 제거해 effective Langevin equation, memory kernel, noise를 얻는다. 그의 책도 projection operator를 Hilbert-space formulation, generalized Langevin equation, slow variables로 전개한다.

---

# 11. 연산자의 스펙트럼만으로 부족할 때 → Lie bracket과 비가환 구조

두 vector field

$$
X,Y\in\Gamma(T\mathcal M)
$$

가 있으면

$$
[X,Y]
$$

는 “$X$ 방향으로 갔다가 $Y$, 반대로 $Y$ 후 $X$로 갔을 때의 차이”를 나타낸다.

이게 필요한 이유는 여러 update나 flow가 일반적으로 commute하지 않기 때문이다.

$$
\Phi_t^X\circ\Phi_s^Y
\neq
\Phi_s^Y\circ\Phi_t^X.
$$

infinitesimal 구조는 Lie algebra,

$$
\mathfrak g
$$

finite transformation은 Lie group

$$
G
$$

가 된다.

시간이 역전 가능하면 group이 자연스럽지만, diffusion·dissipation처럼 역연산이 없으면

$$
P_tP_s=P_{t+s},
\qquad t,s\ge0
$$

인 **semigroup**이 더 자연스럽다.

이 때문에 비평형 확률동역학에서는 Lie group보다 Markov semigroup이 자주 전면에 나온다.

---

# 12. 이제 ODE → SDE → FPE가 한 줄로 연결된다

결정론:

$$
\dot X_t
=
b(X_t)
$$

은 상태공간 위 vector field다.

잡음을 추가하면

$$
dX_t
=
b(X_t)\,dt
+
\sigma(X_t)\,dW_t.
$$

여기서

- $X_t$: $\mathcal X$-값 확률과정,
- $b:\mathcal X\to T\mathcal X$: drift vector field,
- $\sigma$: diffusion map,
- $W_t$: Wiener process.

관측량의 generator는 대략

$$
Lf
=
b\cdot\nabla f
+
\frac12
a^{ij}\partial_i\partial_j f,
\qquad
a=\sigma\sigma^\top.
$$

density는

$$
\partial_t\rho
=
L^*\rho.
$$

즉

$$
\boxed{
\text{vector field}
\to
\text{ODE}
\to
\text{noise}
\to
\text{SDE}
\to
\text{generator}
\to
\text{adjoint}
\to
\text{FPE}
}
$$

가 하나의 자연스러운 연쇄다.

---

# 13. 여기까지가 비평형 통계역학이고, 학습동역학은 슬롯만 바꾼다

신경망에서는

$$
\theta_t\in\Theta
$$

를 상태로 잡고 loss

$$
L:\Theta\to\mathbb R
$$

를 potential처럼 본다.

gradient flow는

$$
\dot\theta_t
=
-\nabla L(\theta_t).
$$

SGD noise를 넣으면

$$
d\theta_t
=
-\nabla L(\theta_t)\,dt
+
\Sigma(\theta_t)^{1/2}\,dW_t.
$$

그러면 parameter distribution

$$
\rho_t\in\mathcal P(\Theta)
$$

가 Fokker–Planck형 PDE를 따른다.

이때 **학습을 weight 하나하나의 궤적이 아니라 distribution의 flow로 볼 수 있게 된다.**

---

# 14. 폭을 크게 보내면 상태 자체가 바뀐다 → empirical measure

폭 $N$인 신경망에서 neuron parameter를

$$
w_1,\ldots,w_N
$$

라고 하면

$$
\mu_N
=
\frac1N
\sum_{i=1}^N
\delta_{w_i}
$$

라는 empirical measure를 정의한다.

이제

$$
N\to\infty
$$

에서

$$
\mu_N\Longrightarrow\mu
$$

라는 limit를 찾는다.

Hanin이 scaling limit의 동기로 “finite interacting system의 empirical measure가 확률측도 공간 위 deterministic PDE로 가는 mean-field limit”을 명시적으로 들고 있다.

그래서 학습동역학은

$$
\theta_t
$$

의 ODE에서

$$
\mu_t\in\mathcal P(\Theta)
$$

의 PDE로 올라간다.

---

# 15. 여기서 NTK와 feature learning이 갈린다

### NTK / lazy branch

초기화 주변의 tangent geometry가 거의 고정된다.

$$
G_t
\approx
G_0.
$$

따라서 학습은 거의 **고정된 metric/kernel 위의 선형화된 flow**다.

### mean-field / feature-learning branch

분포

$$
\mu_t
$$

자체가 크게 변하면서 kernel, representation, correlation 구조도 변한다.

즉

$$
G_t
$$

자체가 동역학적 변수다.

그래서 feature learning을 더 추상적으로 말하면

$$
\boxed{
\text{state changes}
\quad\text{뿐 아니라}\quad
\text{geometry/operator itself changes}
}
$$

이다.

이게 예전에 오빠랑 이야기했던 “feature를 직접 보는 것보다 측도·kernel·correlation의 변화를 보는 이유”와 연결된다. Hanin도 최근 feature-learning 이론을 kernel renormalization, hidden-layer features, multi-scale adaptive theory 등과 연결한다.

---

# 16. 이제 RG가 필요한 이유 → 너무 많은 자유도를 계속 그대로 볼 수 없다

여기까지는 주어진 scale에서 dynamics를 봤다.

하지만 시스템이

- 공간 크기,
- 폭,
- 깊이,
- 데이터 수,
- 시간척도,
- 주파수

에 따라 크게 달라지면 하나의 scale에서 얻은 설명이 다른 scale에서도 유지되는지를 물어야 한다.

그래서 coarse-graining map

$$
C_\ell:
\mathcal S
\to
\mathcal S_\ell
$$

를 둔다.

그 다음 rescaling

$$
R_\ell
$$

을 하고 합성해서

$$
\mathcal R_\ell
=
R_\ell\circ C_\ell
$$

라는 RG transformation을 만든다.

핵심은 **상태가 흐르는 게 아니라 “이론/퍼텐셜/유효 결합상수”가 흐른다**는 것이다.

---

# 17. RG flow는 “flow 위의 flow”다

원래 dynamics는

$$
\rho_t
=
\Phi_t(\rho_0).
$$

RG에서는 effective model의 parameter

$$
g(\ell)
$$

가 scale $\ell$에 따라 변한다.

$$
\frac{dg}{d\log\ell}
=
\beta(g).
$$

여기서

$$
\beta
:
\mathcal G\to T\mathcal G
$$

는 **이론공간 위 vector field**다.

따라서 구조가 완전히 재귀적이다.

$$
\boxed{
\text{물리 상태공간 위 flow}
}
$$

위에 다시

$$
\boxed{
\text{모델/이론 공간 위 RG flow}
}
$$

가 올라간다.

---

# 18. scale invariance는 RG의 fixed point다

어떤 effective theory $g_*$가

$$
\mathcal R_\ell(g_*)
=
g_*
$$

를 만족하면 fixed point다.

그 주변에서 perturbation

$$
g
=
g_*+\delta g
$$

를 넣고 linearize하면

$$
D\mathcal R_{g_*}\delta g
=
\lambda\,\delta g.
$$

여기서 eigenvalue가 다시 scale behavior를 분류한다.

- $|\lambda|>1$: relevant
- $|\lambda|<1$: irrelevant
- $|\lambda|=1$: marginal

재미있는 점은 앞서 generator spectrum이 **시간척도**를 분리했다면, RG linearization spectrum은 **스케일척도**를 분리한다는 것이다.

즉 둘 다

$$
\text{operator}
\to
\text{spectrum}
\to
\text{dominant modes}
$$

라는 같은 수학 인터페이스를 쓴다.

---

# 19. 군 동변성은 어디 붙나

대칭군

$$
G
$$

가 상태공간에 작용한다고 하자.

$$
G\times\mathcal M
\to\mathcal M.
$$

관측량이나 dynamics가 이 작용과 commute하면 equivariance가 있다.

$$
\Phi_t(g\cdot x)
=
g\cdot\Phi_t(x).
$$

RG에서도 coarse-graining 뒤에 같은 대칭이 보존되는지를 본다.

그래서

$$
\text{symmetry}
+
\text{flow}
+
\text{coarse-graining}
$$

의 compatibility가 universality를 이해하는 핵심 조건이 된다.

---

# 20. 대칭성 깨짐은 “퍼텐셜의 최소점 기하가 바뀌는 것”

control parameter

$$
\lambda\in\Lambda
$$

를 가진 potential family

$$
\mathcal F_\lambda:\mathcal M\to\mathbb R
$$

를 생각한다.

평형 상태는

$$
\mathcal E_\lambda
=
\operatorname*{arg\,min}_{x\in\mathcal M}
\mathcal F_\lambda(x).
$$

$\lambda$가 바뀌면서

$$
\mathcal E_\lambda
$$

의 topology, dimension, symmetry가 변하면 phase transition을 볼 수 있다.

대칭군 $G$가 $\mathcal F_\lambda$를 보존해도 선택된 minimizer $x_*$가

$$
g\cdot x_*
\neq
x_*
$$

일 수 있다.

그게 spontaneous symmetry breaking이다.

그래서 오빠가 마지막에 적은

> 대칭성 깨짐과 파라미터 기하

는 사실

$$
\boxed{
\lambda
\mapsto
\mathcal F_\lambda
\mapsto
\operatorname{Crit}(\mathcal F_\lambda)
\mapsto
\text{geometry of solution manifold}
}
$$

라는 흐름으로 정리할 수 있어.

---

# 전체 계층을 한 번에 접으면

```text
도메인별 미시 상태공간 X
        ↓
가능한 상태 / 경로 / 확률측도 공간 S
        ↓
제약조건
        ↓
범함수 변분
 ├─ 경로 변분 → 역학
 ├─ 분포 변분 → MaxEnt / Gibbs
 └─ 분포경로 변분 → gradient flow / optimal transport
        ↓
해집합 M = model / equilibrium / solution manifold
        ↓
좌표 + divergence + potential
        ↓
접공간 T_x M
        ↓
1차 : tangent / gradient / response
2차 : metric / Fisher / Hessian / covariance
고차 : cumulant / nonlinear response / connection
        ↓
관측량 함수공간
        ↓
연산자 U_t
        ↓
generator L
        ↓
adjoint L*
        ↓
observable dynamics ↔ density dynamics
        ↓
spectrum / eigenmodes
        ↓
slow-fast decomposition / projection / coarse graining
        ↓
vector field / flow
 ├─ ODE
 ├─ SDE
 └─ FPE / kinetic PDE
        ↓
대규모 상호작용계
        ↓
empirical measure
        ↓
mean-field / feature-learning dynamics
 ├─ fixed tangent geometry → NTK
 └─ evolving geometry → feature learning
        ↓
scale 변경
        ↓
coarse graining + rescaling
        ↓
RG flow on theory/model space
        ↓
fixed point
        ↓
scale invariance / universality
        ↓
relevant / irrelevant modes
        ↓
control parameter 변화
        ↓
critical manifold / bifurcation
        ↓
symmetry breaking / phase transition
```

그래서 가장 중요한 통합 문장은 **“변분은 어떤 상태를 선택할지를 정하고, 기하는 그 상태공간에서 ‘방향과 거리’를 정하며, generator는 그 기하 위의 시간변화를 정하고, RG는 그런 dynamics 자체가 관측 scale을 바꾸었을 때 어떻게 변하는지를 정한다”**야. 정보기하는 그중 **분포의 통계적 기하**, 수송기하는 **분포가 이동하는 동역학적 기하**, 비평형 통계역학은 **그 기하 위의 확률 flow**, 학습동역학은 **parameter/representation/measure의 flow**, RG는 **그 flow를 기술하는 이론 자체의 flow**라고 놓으면 전체가 거의 한 구조로 정렬돼.