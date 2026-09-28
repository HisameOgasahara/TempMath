# 해석역학에서 공학 모델로 내려가는 추상 인터페이스

이 문서는 **질점 해석역학의 라그랑주 구조에서 출발해 장 이론, Noether, balance law, constitutive law, geometry, reduction, IC/BC를 거쳐 실제 공학별 모델로 내려가는 공통 수학구조**를 한 흐름으로 정리한다.

목표는 특정 물리량의 공식을 외우는 것이 아니라,

> **어떤 공학 문제가 와도 같은 추상 인터페이스에서 무엇을 갈아끼우면 되는지**

를 보이게 하는 것이다.

---

# 0. 전체 흐름

가장 압축하면 다음과 같다.

$$
\boxed{
\begin{array}{c}
\text{State space} \\
\downarrow \\
\text{Action / variational structure} \\
\downarrow \\
\text{Euler--Lagrange equation} \\
\downarrow \\
\text{Symmetry / Noether} \\
\downarrow \\
\text{Local conservation / balance structure} \\
\downarrow \\
\text{Constitutive closure} \\
\downarrow \\
\text{Geometry / kinematic constraints} \\
\downarrow \\
\text{Approximation / reduction} \\
\downarrow \\
\text{IC / BC} \\
\downarrow \\
\text{Engineering model}
\end{array}
}
$$

각 단계의 역할은 다음과 같다.

1. **State space**: 무엇을 상태로 볼지 정한다.
2. **Action / variational structure**: 가능한 상태 경로 중 실제 운동을 고르는 원리를 둔다.
3. **Euler--Lagrange equation**: 변분 원리를 미분방정식으로 바꾼다.
4. **Symmetry / Noether**: 그 운동방정식 안에 숨어 있는 보존구조를 뽑는다.
5. **Balance law**: 저장 / 유입 / 유출 / 생성의 보편적 회계구조로 다시 쓴다.
6. **Constitutive law**: balance만으로 남는 보조 미지수를 실제 물질 / 매질의 반응법칙으로 닫는다.
7. **Geometry / constraints**: 실제 물체나 설비의 형상과 운동 제약을 넣는다.
8. **Approximation / reduction**: 필요 없는 자유도를 버려 PDE를 더 낮은 차원의 PDE / ODE / 대수식으로 줄인다.
9. **IC / BC**: 실제 문제의 초기 상태와 경계에서의 작용을 지정한다.
10. **Engineering model**: 특정 설비 / 재료 / 유체 / 열전달 문제에 맞는 최종 방정식을 얻는다.

---

# 1. 질점 해석역학: 상태 경로를 고르는 문제

## 1.1 목적

질점에서는 상태가 시간에 따라 하나의 벡터로 변한다.

$$
q:[t_0,t_1]\to Q
$$

여기서

- $Q$는 configuration space
- $q(t)\in Q$는 시간 $t$에서의 상태

이다.

예를 들어 $Q=\mathbb R^n$일 수 있다.

문제는 가능한 수많은 경로

$$
q:[t_0,t_1]\to Q
$$

중 실제 운동 $q_\ast$를 고르는 것이다.

---

## 1.2 왜 action을 만드는가

경로 전체를 평가하는 functional을 둔다.

$$
S[q]
=
\int_{t_0}^{t_1}
L(q(t),\dot q(t),t)\,dt
$$

여기서

$$
L:TQ\times[t_0,t_1]\to\mathbb R
$$

는 Lagrangian이다.

즉

$$
S:
\{\text{admissible paths }q\}
\to
\mathbb R
$$

이다.

### 목적

매 순간 힘을 직접 나열하는 대신

> **경로 전체 중 실제 경로를 하나의 변분 조건으로 고르기 위해**

action을 쓴다.

---

# 2. 변분에서 Euler--Lagrange가 왜 나오는가

## 2.1 작은 경로 변형

임의의 variation을

$$
\eta:[t_0,t_1]\to TQ
$$

라고 두고

$$
q_\varepsilon(t)
=
q(t)+\varepsilon\eta(t)
$$

로 경로를 조금 바꾼다.

끝점은 고정한다고 두면

$$
\eta(t_0)=\eta(t_1)=0
$$

이다.

실제 경로가 stationary하다는 조건은

$$
\left.
\frac{d}{d\varepsilon}
S[q_\varepsilon]
\right|_{\varepsilon=0}
=
0
$$

이다.

이것은 고등학교 미적분의

$$
f'(x_\ast)=0
$$

을 함수공간으로 확장한 것이다.

---

## 2.2 왜 두 항이 생기는가

$L$은 $q$와 $\dot q$에 의존한다.

따라서

$$
q_\varepsilon=q+\varepsilon\eta
$$

이면

$$
\dot q_\varepsilon
=
\dot q+\varepsilon\dot\eta
$$

도 변한다.

chain rule로

$$
\delta S
=
\int_{t_0}^{t_1}
\left[
\frac{\partial L}{\partial q}\,\eta
+
\frac{\partial L}{\partial \dot q}\,\dot\eta
\right]dt
$$

가 된다.

---

## 2.3 왜 부분적분이 필요한가

현재 식에는

$$
\eta
$$

와

$$
\dot\eta
$$

가 동시에 있다.

우리는 마지막에

$$
\int A(t)\eta(t)\,dt=0
$$

꼴을 만들고 싶다.

그래야 $\eta$가 임의라는 사실에서

$$
A(t)=0
$$

을 얻을 수 있다.

그래서

$$
\int
\frac{\partial L}{\partial\dot q}\,\dot\eta\,dt
$$

에 부분적분을 적용한다.

$$
\int_{t_0}^{t_1}
\frac{\partial L}{\partial\dot q}\,\dot\eta\,dt
=
\left[
\frac{\partial L}{\partial\dot q}\,\eta
\right]_{t_0}^{t_1}
-
\int_{t_0}^{t_1}
\frac{d}{dt}
\left(
\frac{\partial L}{\partial\dot q}
\right)
\eta\,dt
$$

끝점에서 $\eta=0$이므로 경계항이 사라지고

$$
\delta S
=
\int_{t_0}^{t_1}
\left[
\frac{\partial L}{\partial q}
-
\frac{d}{dt}
\left(
\frac{\partial L}{\partial\dot q}
\right)
\right]
\eta\,dt
$$

가 된다.

모든 admissible $\eta$에 대해 이 값이 0이어야 하므로

$$
\boxed{
\frac{d}{dt}
\left(
\frac{\partial L}{\partial\dot q}
\right)
-
\frac{\partial L}{\partial q}
=
0
}
$$

을 얻는다.

이것이 Euler--Lagrange equation이다.

---

# 3. 질점에서 장으로: $q(t)$에서 $u(x,t)$로

## 3.1 왜 상태가 장이 되는가

질점 하나는

$$
q(t)
$$

하나로 충분하다.

하지만 연속체에서는 공간의 서로 다른 위치가 서로 다르게 움직일 수 있다.

그래서 상태를

$$
u:\Omega\times[t_0,t_1]\to U
$$

로 확장한다.

여기서

- $\Omega\subset\mathbb R^d$는 공간 영역
- $U$는 한 점의 상태값 공간
- $u(x,t)$는 위치 $x$, 시간 $t$에서의 상태

이다.

질점과 장의 대응은

$$
q(t)
\longleftrightarrow
u(x,t)
$$

$$
\dot q(t)
\longleftrightarrow
\partial_tu(x,t)
$$

이다.

---

# 4. 왜 $\nabla u$가 추가되는가

## 4.1 $u$와 $\partial_tu$만 있으면 무엇이 부족한가

만약 장의 Lagrangian density가

$$
\mathcal L=\mathcal L(u,\partial_tu)
$$

뿐이라면 공간의 서로 다른 점은 서로 직접 연결되지 않는다.

즉 각 $x$에서

$$
u(x,t)
$$

가 독립적인 질점처럼 행동한다.

그러면 한 점의 변화가 이웃 점에 전달될 이유가 없다.

---

## 4.2 연속체에서는 이웃점의 상대적 차이가 중요하다

이웃한 두 위치 $x$와 $x+\Delta x$의 상태 차이는

$$
\frac{
u(x+\Delta x,t)-u(x,t)
}{
\Delta x
}
$$

로 측정되고, 극한에서

$$
\nabla u(x,t)
$$

가 된다.

따라서

- $\partial_tu$: 한 위치의 시간 변화
- $\nabla u$: 이웃 위치들과의 공간적 상대 변화

를 나타낸다.

연속체의 내부 결합, 변형, 전달은 바로 이 공간적 상대 변화 때문에 생긴다.

---

# 5. 장의 Lagrangian density

그래서 일반적인 1차 장 이론에서는

$$
\mathcal L
:
U
\times
U
\times
(U\otimes\mathbb R^d)
\times
\Omega
\times
[t_0,t_1]
\to
\mathbb R
$$

를 두고

$$
\mathcal L
=
\mathcal L
\left(
u,
\partial_tu,
\nabla u,
x,
t
\right)
$$

라고 쓴다.

$x,t$는 반드시 필요한 것은 아니다.

공간적으로 균질하고 시간불변이면

$$
\mathcal L
=
\mathcal L(u,\partial_tu,\nabla u)
$$

만으로 충분하다.

---

# 6. 장의 Euler--Lagrange equation

variation을

$$
\eta:\Omega\times[t_0,t_1]\to U
$$

라고 두고

$$
u_\varepsilon
=
u+\varepsilon\eta
$$

로 바꾸면

$$
\partial_tu_\varepsilon
=
\partial_tu
+
\varepsilon\partial_t\eta
$$

$$
\nabla u_\varepsilon
=
\nabla u
+
\varepsilon\nabla\eta
$$

가 된다.

따라서

$$
\delta S
=
\int_{t_0}^{t_1}
\int_\Omega
\left[
\frac{\partial\mathcal L}{\partial u}\eta
+
\frac{\partial\mathcal L}{\partial(\partial_tu)}
\partial_t\eta
+
\frac{\partial\mathcal L}{\partial(\nabla u)}
:
\nabla\eta
\right]
dx\,dt
$$

가 된다.

시간 부분적분과 공간 부분적분을 하면

$$
\boxed{
\frac{\partial\mathcal L}{\partial u}
-
\partial_t
\left(
\frac{\partial\mathcal L}{\partial(\partial_tu)}
\right)
-
\nabla\cdot
\left(
\frac{\partial\mathcal L}{\partial(\nabla u)}
\right)
=
0
}
$$

을 얻는다.

---

# 7. $\partial\mathcal L/\partial(\nabla u)$의 의미

$$
\frac{\partial\mathcal L}{\partial(\nabla u)}
$$

는

> **공간적 상대 변화 $\nabla u$를 조금 바꿨을 때 Lagrangian density가 얼마나 변하는가**

를 나타낸다.

질점에서

$$
\frac{\partial L}{\partial\dot q}
$$

가 속도 변화에 대한 Lagrangian의 반응이었다면,

장에서는 추가로

$$
\frac{\partial\mathcal L}{\partial(\nabla u)}
$$

가 공간적 결합에 대한 반응을 나타낸다.

그리고 공간 부분적분 때문에

$$
\nabla\cdot
\left(
\frac{\partial\mathcal L}{\partial(\nabla u)}
\right)
$$

꼴이 Euler--Lagrange equation에 나타난다.

즉

$$
\boxed{
\text{spatial coupling}
\to
\nabla u
\to
\frac{\partial\mathcal L}{\partial(\nabla u)}
\to
\nabla\cdot(\cdot)
}
$$

이다.

---

# 8. Noether: 왜 보존량을 따로 뽑는가

## 8.1 목적

Euler--Lagrange equation을 얻었다고 해서 항상 직접 풀고 싶은 것은 아니다.

우리는 먼저

> **이 운동이 반드시 보존하는 양이 무엇인가**

를 알고 싶다.

action이 어떤 연속 변환에 대해 불변이면 Noether theorem은 corresponding conserved current를 준다.

추상적으로

$$
\boxed{
\text{symmetry of }S
\to
\text{conserved current}
}
$$

이다.

---

## 8.2 질점과 장의 차이

질점에서는 보존량 하나를

$$
C(t)\in\mathbb R
$$

로 두고

$$
\frac{dC}{dt}=0
$$

라고 하면 된다.

장에서는 보존량이 공간에 퍼져 있으므로

$$
a:\Omega\times[t_0,t_1]\to A
$$

라는 density와

$$
J:\Omega\times[t_0,t_1]\to A\otimes\mathbb R^d
$$

라는 current / flux가 필요하다.

Noether가 주는 local conservation law는 추상적으로

$$
\boxed{
\partial_t a
+
\nabla\cdot J
=
0
}
$$

꼴이다.

---

# 9. Conservation law에서 balance law로

Noether가 주는 구조는 source가 없는 보존법칙이다.

하지만 실제 공학 시스템에는 외부 입력, 내부 생성, 소산, 반응 등이 있을 수 있다.

그래서 더 일반적인 구조를

$$
\boxed{
\partial_t a
+
\nabla\cdot J
=
s
}
$$

로 확장한다.

여기서

- $a$는 stored quantity density
- $J$는 flux / transport quantity
- $s$는 source / sink

이다.

이 식의 의미는

> **어떤 작은 영역 안에 저장된 양의 변화는 경계를 통한 유입 / 유출과 내부 생성 / 소멸로만 설명되어야 한다**

는 것이다.

즉 balance law는 특정 물리량의 공식이라기보다

$$
\boxed{
\text{accumulation}
+
\text{net outward transport}
=
\text{source}
}
$$

라는 공통 회계구조이다.

---

# 10. Balance law만으로 왜 부족한가

## 10.1 우리가 최종적으로 알고 싶은 것

상태를

$$
u:\Omega\times[0,T]\to U
$$

로 선택했다고 하자.

최종 목표는 $u$에 대한 방정식

$$
\mathcal L(u)=f
$$

을 얻는 것이다.

---

## 10.2 그런데 balance law에는 새 미지수가 생긴다

일반 balance law는

$$
\partial_ta(u)
+
\nabla\cdot J
=
s
$$

이다.

여기에는

$$
u
$$

뿐 아니라

$$
J
$$

도 미지수로 들어 있다.

즉 balance law는

$$
\mathcal B(u,J)=s
$$

라는 관계를 줄 뿐이다.

이것은

> **허용 가능한 $(u,J)$ 쌍의 집합**

을 정하는 것이지,

> **주어진 $u$에서 실제 $J$가 무엇인지**

를 정하지 않는다.

---

# 11. "방정식이 닫히지 않았다"의 정확한 의미

우리가 선택한 주된 상태변수가 $u$인데도

$$
\mathcal B(u,J)=s
$$

안에 별도의 보조 미지수 $J$가 남아 있다.

따라서 $u$만으로 evolution을 계산할 수 없다.

이를 unclosed라고 본다.

닫힌다는 것은

$$
\boxed{
\text{모든 보조 미지수가 선택한 상태변수와 알려진 데이터로 표현된다}
}
$$

는 뜻이다.

즉 목표는

$$
\mathcal L(u)=s
$$

처럼 미지수를 선택한 상태변수들로 정리하는 것이다.

---

# 12. Constitutive law의 역할

balance가 $u$와 $J$ 사이의 보편적 제약만 준다면, 이제 실제 시스템이 어떤 $J$를 만드는지 정해야 한다.

그 역할이 constitutive law이다.

가장 일반적으로

$$
\boxed{
J
=
\mathcal C
\left(
u,
\nabla u,
\partial_tu,
\xi,
x,
t
\right)
}
$$

라고 쓸 수 있다.

여기서

$$
\mathcal C:
U
\times
(U\otimes\mathbb R^d)
\times
U
\times
Z
\times
\Omega
\times
[0,T]
\to
A\otimes\mathbb R^d
$$

는 constitutive map이고,

$$
\xi:\Omega\times[0,T]\to Z
$$

는 필요할 경우 사용하는 internal state variable이다.

---

# 13. Balance와 constitutive law의 역할 차이

## 13.1 Balance law

$$
\mathcal B(u,J)=s
$$

### 역할

**무엇이 허용되는가**를 정한다.

즉 저장량, 이동량, source가 서로 모순되지 않도록 하는 보편적인 제약이다.

---

## 13.2 Constitutive law

$$
J=\mathcal C(u,\nabla u,\partial_tu,\xi,x,t)
$$

### 역할

**허용되는 것들 중 이 물질 / 매질 / 시스템이 실제로 어떻게 반응하는가**를 정한다.

즉 balance만으로 남아 있는 자유도를 제거한다.

---

# 14. Constitutive closure

balance law에 constitutive law를 대입하면

$$
\partial_ta(u)
+
\nabla\cdot
\mathcal C
\left(
u,
\nabla u,
\partial_tu,
\xi,
x,
t
\right)
=
s
$$

가 된다.

따라서

$$
\mathcal L(u,\xi)
:=
\partial_ta(u)
+
\nabla\cdot
\mathcal C
\left(
u,
\nabla u,
\partial_tu,
\xi,
x,
t
\right)
$$

라고 두면

$$
\boxed{
\mathcal L(u,\xi)=s
}
$$

라는 닫힌 evolution equation에 가까워진다.

내부변수 $\xi$가 있다면 $\xi$의 evolution law도 추가해야 완전히 닫힌다.

예를 들어

$$
\partial_t\xi
=
\mathcal G(u,\nabla u,\partial_tu,\xi,x,t)
$$

같은 식이 추가될 수 있다.

그러면 상태를 확장해서

$$
z:=(u,\xi)
$$

로 두고

$$
\boxed{
\mathcal F(z)=0
}
$$

라는 하나의 닫힌 시스템으로 본다.

---

# 15. Constitutive law가 공학으로 내려가는 첫 큰 분기점인 이유

State, variational structure, Euler--Lagrange, symmetry, conservation, balance까지는 대체로

> **어떤 시스템도 따라야 할 공통 수학 / 물리 구조**

를 다룬다.

하지만 constitutive law에서는

> **이 물질 / 이 매질 / 이 장치가 실제로 어떤 반응을 보이는가**

를 지정한다.

즉

$$
\boxed{
\text{common structure}
\to
\text{constitutive specialization}
}
$$

이 첫 번째 큰 구체화이다.

다만 constitutive law 하나만으로 공학 문제가 끝나는 것은 아니다.

그 뒤에도 geometry, constraints, regime, BC, IC, device architecture가 추가된다.

---

# 16. Geometry와 kinematic constraints

## 16.1 목적

constitutive law가 **무엇으로 만들어진 시스템인지** 정한다면,

geometry는 **어떤 모양과 연결구조를 가진 시스템인지** 정한다.

예를 들어 원래 상태가

$$
u:\Omega\subset\mathbb R^3\to U
$$

라면 실제 $\Omega$의 모양이

- 긴 구조
- 얇은 구조
- 관 모양
- 회전체
- 연결된 여러 부품

중 무엇인지에 따라 admissible state가 달라진다.

---

## 16.2 수학적 역할

geometry / kinematic constraint는 admissible state space를 줄인다.

원래

$$
u\in X
$$

였던 것을

$$
u\in X_{\mathrm{adm}}
\subset X
$$

로 제한한다.

또는 constraint map

$$
G:X\to Y_G
$$

를 두고

$$
G(u)=0
$$

을 만족하게 할 수 있다.

즉 geometry는 단순한 그림 정보가 아니라

> **허용 가능한 상태 함수의 집합을 제한하는 구조**

이다.

---

# 17. Approximation / reduction

## 17.1 목적

3차원 연속체 PDE를 그대로 풀 필요가 없는 경우가 많다.

그래서 실제 관심 자유도만 남긴다.

원래

$$
u\in X
$$

를 저차원 변수

$$
q\in\mathbb R^n
$$

으로 근사하기 위해

$$
R:\mathbb R^n\to X
$$

라는 reconstruction map을 두고

$$
u\approx R(q)
$$

라고 한다.

예를 들어 basis $\{\phi_i\}_{i=1}^n$를 쓰면

$$
u(x,t)
\approx
\sum_{i=1}^{n}
q_i(t)\phi_i(x)
$$

이다.

그러면 PDE가

$$
\mathcal L(u)=f
$$

에서

$$
\boxed{
M(q)\ddot q
+
C(q,\dot q)
+
K(q)
=
F(t)
}
$$

같은 finite-dimensional ODE로 줄어들 수 있다.

여기서 중요한 것은 특정 식 자체가 아니라

$$
\boxed{
\text{field}
\to
\text{restricted basis / geometry}
\to
\text{finite degrees of freedom}
}
$$

라는 reduction 구조이다.

---

# 18. IC / BC

## 18.1 초기조건

시간 evolution이 있다면 시작 상태가 필요하다.

$$
u(x,0)=u_0(x)
$$

필요하면

$$
\partial_tu(x,0)=v_0(x)
$$

도 둔다.

---

## 18.2 경계조건

공간 영역 $\Omega$의 경계

$$
\partial\Omega
$$

에서 상태나 flux를 지정한다.

추상적으로

$$
B(u,J)=g
\qquad
\text{on }\partial\Omega
$$

라고 쓸 수 있다.

즉 PDE의 내부 법칙만으로는 실제 해가 하나로 정해지지 않기 때문에

> **외부 세계와 시스템이 어떻게 연결되는지**

를 경계조건으로 준다.

---

# 19. 최종 추상 인터페이스

이제 전체를 하나의 인터페이스로 쓰면 다음과 같다.

## 19.1 상태

$$
z=(u,\xi)\in X
$$

---

## 19.2 보편적 balance

$$
\partial_ta(z)
+
\nabla\cdot J
=
s
$$

---

## 19.3 constitutive closure

$$
J
=
\mathcal C
\left(
z,
\nabla z,
\partial_tz,
x,
t
\right)
$$

---

## 19.4 internal evolution이 필요하면

$$
\partial_t\xi
=
\mathcal G
\left(
z,
\nabla z,
\partial_tz,
x,
t
\right)
$$

---

## 19.5 geometry / constraints

$$
G(z)=0
$$

---

## 19.6 boundary / initial data

$$
B(z)=g
\qquad
\text{on }\partial\Omega
$$

$$
z(\cdot,0)=z_0
$$

---

## 19.7 최종 형태

위 식들을 합쳐

$$
\boxed{
\mathcal F
\left(
z,
\partial_tz,
\nabla z,
\nabla^2z,
x,
t
\right)
=
0
}
$$

꼴의 닫힌 PDE system을 얻는다.

그 후 필요하면 reduction을 통해

$$
\boxed{
\mathcal R(q,\dot q,\ddot q,t)=0
}
$$

꼴의 ODE / DAE / algebraic model로 내려간다.

---

# 20. 공통 구조와 도메인 특화가 갈라지는 위치

## 공통 구조

아래는 특정 재료 / 설비에 독립적인 층이다.

$$
\boxed{
\begin{array}{c}
\text{state} \\
\downarrow \\
\text{action / variation} \\
\downarrow \\
\text{Euler--Lagrange} \\
\downarrow \\
\text{symmetry / Noether} \\
\downarrow \\
\text{conservation / balance}
\end{array}
}
$$

---

## 첫 번째 큰 특화

$$
\boxed{
J=\mathcal C(\text{state / gradient / rate / internal variables})
}
$$

여기서 물질 / 매질 / 반응 특성이 들어온다.

---

## 두 번째 큰 특화

$$
\boxed{
\Omega,\ G,\ B
}
$$

즉 geometry, kinematic constraints, boundary interaction이 들어온다.

---

## 세 번째 큰 특화

$$
\boxed{
u\approx R(q)
}
$$

같은 reduction에서 실제 공학에서 사용할 자유도와 근사 regime이 정해진다.

---

# 21. 예시 표: 같은 추상 구조가 분야별로 어떻게 갈라지는가

아래 표는 **먼저 추상 구조를 고정하고**, 각 분야에서 무엇을 갈아끼우는지를 보여준다.

| 추상 슬롯 | 고체 / 재료 | 유체 | 열전달 | 물질전달 | 전기전도 |
|---|---|---|---|---|---|
| 상태 $u$ | 변위 / 속도 / 내부변수 | 속도 / 밀도 / 압력 등 | 온도 | 농도 | 전위 / 장 |
| 저장량 $a(u)$ | 운동량 / 에너지 | 질량 / 운동량 / 에너지 | 내부에너지 | 성분량 | 전하 |
| flux / stress $J$ | 응력 / 에너지 flux | 운동량 flux / 점성응력 | 열 flux | 물질 flux | 전류밀도 |
| constitutive map $\mathcal C$ | 변형 / 변형률률 → 응력 | 속도구배 등 → 응력 | 온도구배 → 열 flux | 농도구배 → 물질 flux | 전기장 → 전류밀도 |
| geometry | 보 / 판 / 쉘 / 축 / 접촉면 | 관 / 채널 / 탱크 | 벽 / 핀 / 교환면 | 막 / packed bed | 도체 / 절연체 형상 |
| reduction | beam / modal ODE | 1D pipe / lumped model | thermal network | compartment model | circuit model |

---

# 22. 예시 표: constitutive law가 왜 도메인 분기점인가

| 단계 | 보편성 | 무엇을 결정하는가 |
|---|---|---|
| State space | 매우 높음 | 무엇을 상태로 볼지 |
| Variational structure | 높음 | 실제 운동을 고르는 원리 |
| Euler--Lagrange | 높음 | 변분을 PDE / ODE로 바꾸기 |
| Noether | 높음 | 대칭에서 보존량 추출 |
| Balance law | 매우 높음 | 저장 / 이동 / 생성의 회계구조 |
| Constitutive law | 중간 | 실제 물질 / 매질의 반응 |
| Geometry / constraints | 낮아짐 | 실제 형상 / 연결 / 구속 |
| Reduction | 낮아짐 | 실제 사용 자유도 / 근사 |
| IC / BC | 매우 구체적 | 실제 운전 / 실험 / 설비 조건 |
| Final engineering model | 가장 구체적 | 특정 설비 / 공정의 예측 |

---

# 23. 공학별로 내려가는 공통 패턴

실제 공학 문제는 아래처럼 보면 된다.

$$
\boxed{
\text{① choose state}
\to
\text{② write balances}
\to
\text{③ identify extra unknown flux / stress / internal variables}
\to
\text{④ choose constitutive laws}
\to
\text{⑤ impose geometry / constraints}
\to
\text{⑥ reduce if needed}
\to
\text{⑦ set IC / BC}
\to
\text{⑧ solve / simulate}
}
$$

이 인터페이스에서 공학별 차이는 주로

$$
\boxed{
\mathcal C,\ \Omega,\ G,\ B,\ R
}
$$

를 무엇으로 선택하느냐에 있다.

즉

- $\mathcal C$: constitutive response
- $\Omega$: geometry
- $G$: kinematic / algebraic constraints
- $B$: boundary interaction
- $R$: model reduction / approximation

가 실제 도메인 고유 구조를 넣는 핵심 슬롯이다.

---

# 24. 해석역학과 공학의 관계를 한 문장으로 정리

해석역학의 공통 구조는

> **상태, action, variation, symmetry, conservation**

을 제공하고,

연속체 / 공학으로 내려가면

> **balance, constitutive closure, geometry, constraint, approximation, IC / BC**

를 추가해서 실제 설비 / 재료 / 유체 / 열 시스템의 방정식을 만든다.

따라서 공학식들은 완전히 별개의 공식 모음이 아니라

$$
\boxed{
\text{common variational / balance structure}
+
\text{constitutive specialization}
+
\text{geometry / constraints}
+
\text{reduction}
+
\text{IC / BC}
}
$$

로 이해할 수 있다.

---

# 25. 최종 압축 인터페이스

앞으로 공학 문제를 볼 때는 아래 슬롯만 찾으면 된다.

$$
\boxed{
\begin{array}{ll}
\textbf{State} & z \in X \\[1mm]
\textbf{Stored quantity} & a=a(z) \\[1mm]
\textbf{Balance} &
\partial_t a(z)+\nabla\cdot J=s \\[1mm]
\textbf{Constitutive law} &
J=\mathcal C(z,\nabla z,\partial_tz,\xi,x,t) \\[1mm]
\textbf{Internal evolution} &
\partial_t\xi=\mathcal G(z,\nabla z,\partial_tz,\xi,x,t) \\[1mm]
\textbf{Geometry / constraints} &
G(z)=0 \\[1mm]
\textbf{Boundary condition} &
B(z,J)=g \\[1mm]
\textbf{Initial condition} &
z(\cdot,0)=z_0 \\[1mm]
\textbf{Reduction} &
z\approx R(q) \\[1mm]
\textbf{Final model} &
\mathcal R(q,\dot q,\ddot q,t)=0
\end{array}
}
$$

이 틀을 유지한 채 각 도메인에서 필요한 물리량 / 물성 / 형상 / 설비조건만 갈아끼우면 된다.
