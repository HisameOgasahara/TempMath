# 결정론적 역학계와 Markov 반군: 생성자, Flow, Pushforward, 수반연산자, Fokker–Planck의 연결

## 0. 전체 구조 한눈에 보기

결정론과 확률과정의 공통 뼈대는 다음과 같다.

$$
\boxed{
\text{무한소적 시간변화}
\;\longrightarrow\;
\text{유한시간 진화}
\;\longrightarrow\;
\text{관측량 또는 분포의 시간진화}
}
$$

결정론에서는 한 상태가 다음의 한 상태로 이동한다.

$$
x \longmapsto \Phi_t(x)
$$

확률과정에서는 한 상태에서 다음 상태가 하나로 정해지지 않고 확률분포가 나온다.

$$
x \longmapsto P_t(x,\cdot)
$$

따라서 확률과정은 결정론의 시간진화 구조를 버리는 것이 아니라,

$$
\boxed{
\text{점}\to\text{점}
\quad\rightsquigarrow\quad
\text{점}\to\text{확률분포}
}
$$

로 확장한 것으로 볼 수 있다.

---

# 1. 결정론: 벡터장 → ODE → flow

상태공간을 매끄러운 다양체 $M$이라 하고 벡터장을

$$
V:M\to TM,
\qquad
V(x)\in T_xM
$$

이라 하자.

이 벡터장이 만드는 ODE는

$$
\dot x_t=V(x_t)
$$

이다.

초기값 $x\in M$을 고정하면 시간 $t$ 뒤 상태를 주는 사상

$$
\Phi_t:M\to M,
\qquad
x\mapsto\Phi_t(x)
$$

이 생긴다.

ODE의 해가 유일하다면

$$
\Phi_{t+s}
=
\Phi_t\circ\Phi_s.
$$

또한 벡터장이 complete하여 음의 시간까지 해가 존재한다면

$$
\Phi_{-t}
=
\Phi_t^{-1}
$$

이므로 $\{\Phi_t\}_{t\in\mathbb R}$는 1-parameter group을 이룬다.

즉 구조적으로

$$
\boxed{
\text{vector field}
\longrightarrow
\text{flow}
}
$$

이고, Lie 이론의 언어로는 대략

$$
V
\overset{\exp}{\longmapsto}
\Phi_t
$$

와 같은 관계로 볼 수 있다.

---

# 2. 상태의 flow가 관측량 함수에 유도하는 작용

상태 자체가 아니라 관측량

$$
f:M\to\mathbb R
$$

을 보자.

flow $\Phi_t$가 있으면 함수공간에는

$$
(U_tf)(x)
:=
f(\Phi_t(x))
$$

라는 연산자가 유도된다.

그러면

$$
U_{t+s}
=
U_tU_s.
$$

이 연산자 반군 또는 군의 무한소 생성자는

$$
Af
:=
\left.
\frac{d}{dt}
\right|_{t=0}
U_tf.
$$

연쇄법칙을 쓰면

$$
Af
=
df(V)
=
Vf.
$$

즉 상태공간에서는 벡터장 $V$였던 것이 함수공간에서는 1차 미분연산자가 된다.

$$
\boxed{
\text{상태공간의 벡터장}
\quad\longleftrightarrow\quad
\text{함수공간의 1차 미분 생성자}
}
$$

---

# 3. Lie algebra는 어디에서 나오는가

벡터장 $V$는 함수에 대해 derivation으로 작용한다.

$$
V(fg)
=
fVg+gVf.
$$

두 벡터장 $V,W$에 대해 교환자를

$$
[V,W]f
:=
V(Wf)-W(Vf)
$$

로 정의하면 다시 벡터장이 된다.

따라서 벡터장들은 Lie bracket 아래 Lie algebra를 이룬다.

특히

$$
[V,W]=0
$$

이면 대응하는 두 flow는 서로 commute한다.

$$
\Phi_t^V\circ\Phi_s^W
=
\Phi_s^W\circ\Phi_t^V.
$$

따라서 결정론에서는

$$
\boxed{
\text{vector field}
\longleftrightarrow
\text{1차 미분 생성자}
\longrightarrow
\text{flow/group}
}
$$

가 기본 구조다.

---

# 4. 확률과정: 점의 flow에서 transition kernel로

결정론에서는

$$
x
\overset{\Phi_t}{\longmapsto}
\Phi_t(x)
$$

라는 점에서 점으로의 사상이 있었다.

Markov 과정에서는 초기 상태 $x$를 고정해도 $t$ 뒤 상태가 하나로 정해지지 않는다.

대신

$$
x
\longmapsto
P_t(x,\cdot)
$$

가 생긴다.

여기서

$$
P_t(x,\cdot)\in\mathcal P(M)
$$

은 상태 $x$에서 출발했을 때 시간 $t$ 뒤 상태의 확률분포다.

따라서 구조적으로

$$
M\to M
$$

이

$$
M\to\mathcal P(M)
$$

으로 확장된 셈이다.

Markov 성질 때문에 transition kernel들은 Chapman–Kolmogorov 관계

$$
P_{t+s}(x,A)
=
\int_M
P_s(y,A)\,P_t(x,dy)
$$

를 만족한다.

이것이 확률과정에서 시간합성 구조를 만든다.

---

# 5. 관측량 쪽의 Markov semigroup

관측량

$$
f:M\to\mathbb R
$$

에 대해

$$
(P_tf)(x)
:=
\mathbb E_x[f(X_t)]
=
\int_M f(y)P_t(x,dy)
$$

라고 정의한다.

그러면 Chapman–Kolmogorov 관계 때문에

$$
P_{t+s}
=
P_tP_s
$$

가 성립한다.

이것이 보통 함수공간에서 말하는 Markov semigroup이다.

결정론과 나란히 쓰면

$$
\begin{aligned}
\text{결정론:}\qquad
(U_tf)(x)
&=
f(\Phi_t(x)),
\\[4pt]
\text{Markov:}\qquad
(P_tf)(x)
&=
\mathbb E_x[f(X_t)].
\end{aligned}
$$

결정론은 Markov 이론의 특수한 경우로 포함된다.

전이확률을

$$
P_t(x,dy)
=
\delta_{\Phi_t(x)}(dy)
$$

라고 놓으면

$$
P_tf(x)
=
\int_M f(y)\delta_{\Phi_t(x)}(dy)
=
f(\Phi_t(x)).
$$

따라서

$$
P_t=U_t.
$$

---

# 6. 확률과정의 generator

Markov semigroup의 generator는

$$
Lf
:=
\lim_{t\downarrow0}
\frac{P_tf-f}{t}
$$

로 정의된다.

결정론에서는

$$
dX_t=b(X_t)\,dt
$$

일 때

$$
Lf
=
b\cdot\nabla f.
$$

즉 generator는 1차 미분연산자다.

하지만 diffusion

$$
dX_t
=
b(X_t)\,dt
+
\sigma(X_t)\,dW_t
$$

에서는

$$
a(x)
:=
\sigma(x)\sigma(x)^\top
$$

라 두면

$$
Lf(x)
=
\sum_i b^i(x)\partial_i f(x)
+
\frac12
\sum_{i,j}
a^{ij}(x)
\partial_i\partial_jf(x).
$$

즉 확률화하면서

$$
\boxed{
\text{1차 미분연산자}
\quad\longrightarrow\quad
\text{2차 미분연산자}
}
$$

로 확장된다.

이 2차항은 Itô calculus의 quadratic variation

$$
(dW_t)^2=dt
$$

때문에 나타난다.

---

# 7. 확률 generator는 일반적으로 derivation이 아니다

결정론의 벡터장 $V$는

$$
V(fg)=fVg+gVf
$$

를 만족한다.

하지만 diffusion generator $L$은

$$
L(fg)
=
fLg+gLf
+
\sum_{i,j}
a^{ij}
(\partial_i f)(\partial_j g).
$$

즉 추가항이 존재한다.

따라서

$$
\boxed{
\text{확률 generator는 일반적으로 vector field가 아니며 derivation도 아니다.}
}
$$

Stratonovich 형태

$$
dX_t
=
V_0(X_t)\,dt
+
\sum_{\alpha=1}^m
V_\alpha(X_t)\circ dW_t^\alpha
$$

에서는 generator가

$$
L
=
V_0+
\frac12
\sum_{\alpha=1}^mV_\alpha^2
$$

로 표현된다.

여기서 각각의 $V_\alpha$는 여전히 벡터장이지만, 전체 generator는 벡터장들의 합뿐 아니라 합성 $V_\alpha^2$까지 포함한다.

따라서 대략

$$
\boxed{
\text{Lie algebra of vector fields}
\quad\longrightarrow\quad
\text{더 큰 differential-operator algebra}
}
$$

로 확장된다고 볼 수 있다.

---

# 8. 왜 확률과정에서는 group보다 semigroup인가

결정론에서 충분히 좋은 ODE라면

$$
x
\xrightarrow{\Phi_t}
x_t
\xrightarrow{\Phi_{-t}}
x
$$

로 돌아갈 수 있다.

따라서 group 구조가 자연스럽다.

하지만 Markov operator는

$$
(P_tf)(x)
=
\mathbb E_x[f(X_t)]
$$

처럼 여러 미래를 평균내 버린다.

즉 정보가 소실되므로 일반적으로

$$
P_t^{-1}
$$

가 존재하지 않는다.

그래서

$$
t\ge0
$$

에서 정의되는 semigroup이 자연스럽다.

---

# 9. 실제 응용에서는 이 추상구조가 어떤 계산으로 나타나는가

실제 응용에서는 Lie algebra, group, semigroup이라는 말을 직접 계산하는 경우보다

$$
\boxed{
\text{국소적인 변화율}
\longrightarrow
\text{한 스텝 업데이트}
\longrightarrow
\text{반복하여 유한시간 진화}
}
$$

의 형태로 나타나는 경우가 많다.

## 9.1 선형 ODE

상태 $x(t)\in\mathbb R^n$와 행렬 $A$에 대해

$$
\dot x(t)=Ax(t)
$$

이면

$$
x(t)=e^{tA}x(0).
$$

여기서 $A$가 infinitesimal generator이고

$$
e^{tA}
$$

가 유한시간 진화다.

수치계산에서는

$$
x_{k+1}
\approx
(I+\Delta tA)x_k
$$

같은 time stepping으로 구현할 수 있다.

즉

$$
\boxed{
\text{generator}
\to
\text{한 스텝 업데이트}
\to
\text{전체 궤적}
}
$$

이다.

---

# 10. 로봇 회전에서 Lie algebra가 실제 계산으로 나타나는 모습

자세를

$$
R(t)\in SO(3)
$$

라 하고 각속도를

$$
\omega
=
(\omega_1,\omega_2,\omega_3)\in\mathbb R^3
$$

라 하자.

이를 skew-symmetric matrix로 보내면

$$
\widehat\omega
=
\begin{pmatrix}
0&-\omega_3&\omega_2\\
\omega_3&0&-\omega_1\\
-\omega_2&\omega_1&0
\end{pmatrix}
\in\mathfrak{so}(3).
$$

짧은 시간 $\Delta t$ 뒤 자세는

$$
R(t+\Delta t)
\approx
R(t)\exp(\Delta t\,\widehat\omega).
$$

즉 실제 계산에서는

$$
\boxed{
\text{각속도}
\to
\text{Lie algebra 원소}
\to
\exp
\to
\text{rotation matrix 업데이트}
}
$$

로 나타난다.

---

# 11. Lie bracket이 제어에서 실제 계산으로 나타나는 모습

두 제어 벡터장 $X,Y$를 아주 짧은 시간 $\varepsilon$씩 번갈아 실행하면

$$
e^{\varepsilon X}
e^{\varepsilon Y}
e^{-\varepsilon X}
e^{-\varepsilon Y}
=
e^{\varepsilon^2[X,Y]+O(\varepsilon^3)}.
$$

따라서 직접 제어할 수 없는 방향도 여러 조작을 합성하면 새롭게 나타날 수 있다.

예를 들어 자동차처럼 옆으로 직접 이동할 수 없는 시스템에서도

- 앞으로 이동
- 회전
- 뒤로 이동
- 역회전

같은 조작을 합성하면 직접 입력하지 않은 방향의 순변위를 만들 수 있다.

즉 Lie bracket은 응용에서

$$
\boxed{
\text{입력으로 직접 만들 수 없는 방향을 조작의 합성으로 만들 수 있는가}
}
$$

를 검사하는 계산으로 나타난다.

---

# 12. 유한상태 Markov chain에서 semigroup의 실제 모습

유한상태 continuous-time Markov chain의 generator를 행렬 $Q$라고 하자.

분포 $p(t)$는

$$
\frac{d}{dt}p(t)
=
p(t)Q
$$

를 만족하고,

$$
p(t)
=
p(0)e^{tQ}.
$$

따라서

- $Q$: 순간적인 상태전이율
- $e^{tQ}$: 시간 $t$ 후의 전이확률 행렬

이다.

즉 추상적인 Markov semigroup은 실제 계산에서는 transition matrix를 시간에 따라 만드는 것으로 나타난다.

---

# 13. SDE에서는 semigroup이 PDE 또는 Monte Carlo로 계산된다

SDE

$$
dX_t
=
b(X_t)\,dt
+
\sigma(X_t)\,dW_t
$$

의 generator가

$$
Lf
=
b\cdot\nabla f
+
\frac12a:\nabla^2f
$$

라 하자.

여기서

$$
a
=
\sigma\sigma^\top.
$$

함수

$$
u(t,x)
:=
\mathbb E_x[f(X_t)]
$$

는 backward equation

$$
\partial_tu
=
Lu
$$

를 만족한다.

형식적으로

$$
u(t)
=
e^{tL}f
=
P_tf.
$$

실제 계산에서는 $e^{tL}$이라는 무한차원 연산자를 직접 구성하기보다

1. PDE solver로 $\partial_tu=Lu$를 풀거나,
2. SDE를 여러 번 simulation하여 Monte Carlo 평균을 계산한다.

Monte Carlo에서는

$$
(P_tf)(x)
=
\mathbb E_x[f(X_t)]
\approx
\frac1N
\sum_{i=1}^N
f(X_t^{(i)}).
$$

따라서 실제 계산 관점에서

$$
\boxed{
\text{generator}
\longrightarrow
\begin{cases}
\text{matrix exponential}\\
\text{time stepping}\\
\text{PDE evolution}\\
\text{transition matrix}\\
\text{Monte Carlo expectation}
\end{cases}
\longrightarrow
\text{finite-time evolution}
}
$$

이라고 볼 수 있다.

---

# 14. 확률과정에서 flow라는 말을 쓰는 경우

Markov semigroup $P_t$ 자체를 보통 flow라고 부르지는 않는다.

하지만 같은 noise realization $\omega$를 고정하고 모든 초기값 $x$에 대해 SDE를 동시에 풀어

$$
x
\longmapsto
X_t^x(\omega)
$$

라는 랜덤한 사상을 만들면 이것을 stochastic flow라고 부른다.

즉

- $P_t$: Markov semigroup
- $x\mapsto X_t^x(\omega)$: stochastic flow

로 구별하면 된다.

---

# 15. Fokker–Planck equation과 pushforward의 연결

먼저 결정론에서 ODE

$$
\dot x_t
=
b(x_t)
$$

가 flow

$$
\Phi_t:M\to M
$$

를 만든다고 하자.

초기 분포

$$
\mu_0\in\mathcal P(M)
$$

가 있으면 시간 $t$ 후 분포는 pushforward

$$
\mu_t
=
(\Phi_t)_\#\mu_0
$$

가 된다.

즉 한 점 수준에서는

$$
x\mapsto\Phi_t(x)
$$

이고, 앙상블 수준에서는

$$
\mu_0
\mapsto
(\Phi_t)_\#\mu_0
$$

이다.

---

# 16. 관측량의 pullback과 분포의 pushforward는 쌍대다

관측량

$$
f:M\to\mathbb R
$$

에 대해

$$
(U_tf)(x)
=
f(\Phi_t(x))
$$

라 하자.

함수와 측도의 pairing을

$$
\langle f,\mu\rangle
:=
\int_M f\,d\mu
$$

로 정의하면

$$
\int_M
f\,d((\Phi_t)_\#\mu)
=
\int_M
f\circ\Phi_t\,d\mu.
$$

즉

$$
\boxed{
\langle f,(\Phi_t)_\#\mu\rangle
=
\langle U_tf,\mu\rangle.
}
$$

따라서

- 함수 쪽: $f\mapsto f\circ\Phi_t$
- 측도 쪽: $\mu\mapsto(\Phi_t)_\#\mu$

는 같은 dynamics를 서로 쌍대적인 두 층위에서 표현한 것이다.

---

# 17. 확률과정에서는 pushforward가 $P_t^*$로 일반화된다

Markov kernel $P_t(x,dy)$가 있을 때 관측량에는

$$
(P_tf)(x)
=
\int_M
f(y)P_t(x,dy)
$$

가 작용한다.

분포 $\mu$에는

$$
(P_t^*\mu)(A)
:=
\int_M
P_t(x,A)\,\mu(dx)
$$

가 작용한다.

그러면

$$
\boxed{
\langle P_tf,\mu\rangle
=
\langle f,P_t^*\mu\rangle.
}
$$

시간 $t$ 후 분포는

$$
\mu_t
=
P_t^*\mu_0.
$$

결정론에서는

$$
P_t(x,dy)
=
\delta_{\Phi_t(x)}(dy)
$$

이므로

$$
P_t^*\mu
=
(\Phi_t)_\#\mu.
$$

따라서

$$
\boxed{
P_t^*
\text{는 확률론에서 deterministic pushforward의 일반화}
}
$$

라고 볼 수 있다.

---

# 18. generator의 수반과 Fokker–Planck equation

관측량 쪽 generator를

$$
Lf
=
\lim_{t\downarrow0}
\frac{P_tf-f}{t}
$$

라 하자.

분포가

$$
\mu_t
=
P_t^*\mu_0
$$

로 진화할 때

$$
\frac{d}{dt}
\langle f,\mu_t\rangle
=
\langle Lf,\mu_t\rangle.
$$

$L^*$를 pairing에 대한 수반으로

$$
\boxed{
\langle Lf,\mu\rangle
=
\langle f,L^*\mu\rangle
}
$$

라 정의하면

$$
\boxed{
\partial_t\mu_t
=
L^*\mu_t.
}
$$

이것이 Fokker–Planck equation의 측도 형태다.

---

# 19. 밀도 형태의 Fokker–Planck equation

SDE

$$
dX_t
=
b(X_t)\,dt
+
\sigma(X_t)\,dW_t
$$

와

$$
a
:=
\sigma\sigma^\top
$$

에 대해

$$
Lf
=
\sum_i
b_i\partial_i f
+
\frac12
\sum_{i,j}
a_{ij}
\partial_i\partial_jf.
$$

분포가 기준측도 $dx$에 대해 밀도

$$
\mu_t(dx)
=
\rho_t(x)\,dx
$$

를 가진다고 하자.

적분 by parts로 $L$을 밀도 쪽으로 넘기면

$$
L^*\rho
=
-\sum_i
\partial_i(b_i\rho)
+
\frac12
\sum_{i,j}
\partial_i\partial_j(a_{ij}\rho).
$$

따라서 Fokker–Planck equation은

$$
\boxed{
\partial_t\rho_t
=
-\nabla\cdot(b\rho_t)
+
\frac12
\sum_{i,j}
\partial_i\partial_j(a_{ij}\rho_t).
}
$$

가 된다.

즉

$$
\boxed{
\text{pushforward}
\leftrightarrow
\text{분포의 실제 운반}
}
$$

이고

$$
\boxed{
\text{adjoint}
\leftrightarrow
\text{같은 운반을 함수-측도 pairing으로 표현한 것}
}
$$

이며

$$
\boxed{
\text{FPE}
\leftrightarrow
\text{그 분포 진화를 infinitesimal하게 쓴 방정식}
}
$$

이다.

---

# 20. Markov 반군이 작용하는 세 층위

Markov 시간진화는 세 층위에서 볼 수 있다.

$$
\boxed{
\begin{array}{ccc}
\text{상태/전이 층위}
&
\text{관측량 층위}
&
\text{분포 층위}
\\[2mm]
x\mapsto P_t(x,\cdot)
&
f\mapsto P_tf
&
\mu\mapsto P_t^*\mu
\end{array}
}
$$

## 20.1 상태/전이 층위

$$
P_t(x,\cdot)\in\mathcal P(E)
$$

는 초기 상태 $x$에서 시작했을 때 시간 $t$ 뒤 상태의 분포다.

즉

$$
x
\mapsto
P_t(x,\cdot).
$$

이 kernel들이 Chapman–Kolmogorov 관계를 만족한다.

$$
P_{t+s}(x,A)
=
\int_E
P_s(y,A)P_t(x,dy).
$$

## 20.2 관측량 층위

관측량

$$
f:E\to\mathbb R
$$

에 대해

$$
(P_tf)(x)
=
\int_E
f(y)P_t(x,dy)
=
\mathbb E_x[f(X_t)].
$$

즉

$$
P_t:
\mathcal F(E)
\to
\mathcal F(E)
$$

라는 함수공간 연산자가 된다.

## 20.3 분포 층위

초기분포

$$
\mu\in\mathcal P(E)
$$

에 대해

$$
(P_t^*\mu)(A)
=
\int_E
P_t(x,A)\,\mu(dx).
$$

즉

$$
P_t^*:
\mathcal P(E)
\to
\mathcal P(E)
$$

가 된다.

---

# 21. 왜 세 층위 모두에서 semigroup 구조가 나타나는가

세 개의 서로 다른 반군이 우연히 동시에 생기는 것이 아니다.

공통 데이터는 하나의 transition kernel

$$
K_t:
x\longmapsto K_t(x,\cdot)\in\mathcal P(E)
$$

이다.

이 kernel이 Chapman–Kolmogorov 관계

$$
K_{t+s}(x,A)
=
\int_E
K_s(y,A)
K_t(x,dy)
$$

를 만족한다.

이 하나의 합성법칙을 관측량과 분포에서 각각 읽으면 두 반군이 자동으로 생긴다.

관측량에서는

$$
(P_tf)(x)
:=
\int_E
f(y)K_t(x,dy),
$$

분포에서는

$$
(P_t^*\mu)(A)
:=
\int_E
K_t(x,A)\mu(dx).
$$

따라서

$$
P_{t+s}
=
P_tP_s
$$

이고

$$
P_{t+s}^*
=
P_t^*P_s^*.
$$

즉

$$
\boxed{
\text{하나의 Chapman–Kolmogorov 합성법칙}
\Rightarrow
\text{여러 표현공간에서 동일한 semigroup 구조}
}
$$

이다.

---

# 22. 세 층위는 서로 동등한가

충분히 풍부한 공간에서 본다면 상당 부분 서로 복원 가능하다.

## 22.1 함수 쪽에서 kernel 복원

함수 쪽 $P_t$가 bounded measurable functions 전체에 정의되어 있다면 indicator function $1_A$를 넣어서

$$
\boxed{
K_t(x,A)
=
(P_t1_A)(x)
}
$$

로 kernel을 복원할 수 있다.

## 22.2 측도 쪽에서 kernel 복원

분포 쪽 $P_t^*$를 알고 있다면 Dirac measure $\delta_x$를 넣어서

$$
\boxed{
K_t(x,\cdot)
=
P_t^*\delta_x
}
$$

로 복원할 수 있다.

따라서 적절한 조건 아래

$$
\boxed{
K_t
\Longleftrightarrow
P_t
\Longleftrightarrow
P_t^*
}
$$

라고 볼 수 있다.

---

# 23. 왜 항상 완전히 동등하지는 않은가

실제 해석학에서는 $P_t$를 모든 measurable function이 아니라

$$
C_0(E),\qquad
L^p(E),\qquad
C_b(E)
$$

같은 특정 함수공간에서만 다루는 경우가 많다.

이때 indicator function $1_A$가 그 함수공간에 들어가지 않을 수 있다.

그러면

$$
K_t(x,A)
=
(P_t1_A)(x)
$$

를 바로 사용할 수 없다.

이 경우 kernel을 복원하려면

- 상태공간의 위상
- positivity
- continuity
- Riesz representation theorem을 적용할 수 있는 조건

등이 추가로 필요하다.

따라서

$$
\boxed{
\text{표현들이 완전히 동등한지는 사용하는 함수공간과 위상적 조건에 달려 있다.}
}
$$

---

# 24. generator에서 semigroup으로 가는 것은 더 어려운 문제다

semigroup에서 generator는

$$
Lf
=
\lim_{t\downarrow0}
\frac{P_tf-f}{t}
$$

로 얻을 수 있다.

하지만 임의의 연산자 $L$을 하나 준다고 항상 어떤 Markov semigroup $P_t$가 존재하는 것은 아니다.

즉

$$
\boxed{
P_t\to L
}
$$

보다

$$
\boxed{
L\to P_t
}
$$

가 더 어려운 문제다.

generator에서 semigroup을 만들기 위해서는 보통

- 적절한 domain
- closedness
- dissipativity
- range 조건
- continuity 조건

등이 필요하다.

Hille–Yosida류 정리는 바로

$$
\boxed{
\text{어떤 infinitesimal operator가 실제 semigroup을 생성하는가}
}
$$

를 판정한다.

---

# 25. 무엇이 가장 근본적인가

무엇을 근본적이라 보는지는 관점에 따라 다르다.

## 확률론적 관점

가장 직접적인 것은 transition kernel

$$
K_t(x,dy)
$$

이다.

이는

$$
\text{현재 상태 }x
\longmapsto
\text{시간 }t\text{ 뒤 상태의 확률법칙}
$$

을 직접 표현한다.

## 해석학/PDE 관점

함수공간 semigroup

$$
P_t
$$

와 generator

$$
L
$$

가 자연스럽다.

특히

$$
\partial_tu
=
Lu
$$

같은 PDE와 직접 연결된다.

## 분포/FPE 관점

분포 쪽 semigroup

$$
P_t^*
$$

와 수반 generator

$$
L^*
$$

가 자연스럽다.

$$
\partial_t\mu_t
=
L^*\mu_t
$$

가 바로 분포의 시간진화이기 때문이다.

---

# 26. 실제 확률과정 자체와 semigroup은 완전히 같은 정보인가

실제 확률과정은

$$
\{X_t\}_{t\ge0}
$$

이라는 경로 수준의 객체다.

Markov semigroup은 각 시간 사이의 전이법칙을 담지만

- sample path의 연속성
- càdlàg 여부
- 같은 transition law를 갖는 서로 다른 realization

같은 경로 수준의 구조를 모두 직접 담는 것은 아니다.

따라서

$$
\boxed{
\text{transition semigroup}
\neq
\text{모든 pathwise 정보}
}
$$

라고 구분해야 한다.

---

# 27. 전체 구조 정리

결정론에서는

$$
\boxed{
\begin{array}{ccccc}
\text{상태}&&\text{관측량}&&\text{분포}\\[1mm]
\Phi_t
&\longleftrightarrow&
U_tf=f\circ\Phi_t
&\longleftrightarrow&
(\Phi_t)_\#\mu
\\[2mm]
V
&&
Vf
&&
V^*\mu
\end{array}
}
$$

확률과정에서는

$$
\boxed{
\begin{array}{ccccc}
\text{상태/전이}&&\text{관측량}&&\text{분포}\\[1mm]
P_t(x,dy)
&\longleftrightarrow&
P_tf
&\longleftrightarrow&
P_t^*\mu
\\[2mm]
&&L&&L^*
\\[2mm]
&&\partial_tu=Lu
&&\partial_t\mu=L^*\mu
\end{array}
}
$$

결정론은

$$
P_t(x,dy)
=
\delta_{\Phi_t(x)}(dy)
$$

인 특수한 경우다.

따라서 가장 압축하면

$$
\boxed{
\text{하나의 시간진화 법칙}
\Rightarrow
\begin{cases}
\text{점에서 보면 transition}\\
\text{관측량에서 보면 operator semigroup}\\
\text{분포에서 보면 dual semigroup}
\end{cases}
}
$$

이고,

$$
\boxed{
\text{generator}
\longleftrightarrow
\text{무한소적 시간진화}
}
$$

$$
\boxed{
\text{semigroup}
\longleftrightarrow
\text{유한시간 시간진화}
}
$$

$$
\boxed{
\text{Fokker–Planck}
\longleftrightarrow
\text{분포 쪽 generator }L^*\text{의 진화방정식}
}
$$

으로 이해하면 전체가 하나의 구조로 연결된다.

---

## 참고 문헌

- John M. Lee, *Introduction to Smooth Manifolds*, 2nd ed.
- Stewart N. Ethier and Thomas G. Kurtz, *Markov Processes: Characterization and Convergence*.
- Ioannis Karatzas and Steven E. Shreve, *Brownian Motion and Stochastic Calculus*, 2nd ed.
- Amnon Pazy, *Semigroups of Linear Operators and Applications to Partial Differential Equations*.
