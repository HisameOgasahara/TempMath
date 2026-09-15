# HJE와 HJB의 해, 그라디언트, 궤적, 제어입력의 연결

원본 대화 링크: https://chatgpt.com/share/6aa9c9f1-6d80-83ee-b0b4-fa8ca357dae3?ogimg=plain

---

## 1. HJE의 해와 HJB의 해는 무엇의 함수인가?

### 사용자
HJE의 해와 HJB의 해가 어떻게 돼? 애초에 뭐의 함수야?

### ChatGPT
핵심은 둘 다 **시간 $t$와 현재 상태/좌표 $x$를 입력으로 받는 스칼라 함수**를 구하는 PDE라는 점이다. 다만 그 함수의 의미가 다르다.

| 방정식 | 해 | 함수의 입력 | 해의 의미 |
|---|---|---|---|
| HJE (Hamilton–Jacobi equation) | $S:[0,T]\times\mathcal X\to\mathbb R$ | 시간 $t$, 위치/상태 $x\in\mathcal X$ | 그 지점까지의 **작용(action)** |
| HJB (Hamilton–Jacobi–Bellman) | $V:[0,T]\times\mathcal X\to\mathbb R$ | 시간 $t$, 상태 $x\in\mathcal X$ | 그 상태에서 시작했을 때 얻을 수 있는 **최적 미래 비용** |

예를 들어 상태공간이 $\mathcal X=\mathbb R^d$이면,

$$
S:[0,T]\times\mathbb R^d\to\mathbb R,
\qquad
V:[0,T]\times\mathbb R^d\to\mathbb R.
$$

HJE는 보통

$$
\partial_t S(t,x)
+
H\!\left(x,\nabla_x S(t,x)\right)=0
$$

이고, 해 $S(t,x)$의 공간 미분에서

$$
p(t)=\nabla_x S(t,x)
$$

처럼 운동량 $p\in\mathbb R^d$을 얻는다. 즉 $S$ 자체가 궤적은 아니고, $S$라는 스칼라장의 gradient가 역학 정보를 준다.

HJB는 제어 $u\in\mathcal U$가 들어가서

$$
\partial_t V(t,x)
+
\inf_{u\in\mathcal U}
\left\{
\ell(x,u)
+
b(x,u)\cdot\nabla_xV(t,x)
+
\frac12\operatorname{Tr}
\!\left[
\sigma\sigma^\top(x,u)\nabla_x^2V(t,x)
\right]
\right\}
=0
$$

이 되고, 해 $V(t,x)$는 **현재가 $(t,x)$일 때 앞으로 최적으로 행동하면 드는 최소 기대비용**이다.

제일 짧게 말하면 **HJE의 해 $S(t,x)$ = action 함수, HJB의 해 $V(t,x)$ = optimal value 함수**다. 둘 다 “경로 자체”가 아니라 **상태공간 위의 스칼라장**이다.

---

## 2. 두 스칼라장이나 그 gradient가 만드는 상태궤적은 어떻게 되는가?

### 사용자
두 스칼라장이나 그 그라디언트가 만드는 상태궤적이 어떻게 돼? 전자는 시간별로 위치 운동량 찍힐거 같은데, 후자는 제어입력이 궤적에 어떻게 연결되는 지 모르겠어.

### ChatGPT
차이는 **HJE는 gradient가 바로 운동량을 주고, HJB는 gradient가 제어입력을 정한 다음 그 제어가 동역학을 통해 상태궤적을 만든다**는 것이다.

HJE에서는 $S:[0,T]\times\mathbb R^d\to\mathbb R$가 주어졌을 때

$$
p(t)=\nabla_x S(t,x(t))\in\mathbb R^d
$$

로 운동량이 정해지고, Hamiltonian $H:\mathbb R^d\times\mathbb R^d\to\mathbb R$에 대해

$$
\dot x(t)=\nabla_p H(x(t),p(t)),\qquad
\dot p(t)=-\nabla_x H(x(t),p(t))
$$

를 적분하면

$$
t\mapsto (x(t),p(t))
$$

라는 phase-space 궤적이 나온다. 즉 “각 시간마다 위치 $x(t)$, 운동량 $p(t)$”가 찍히는 그림이 맞다.

반면 HJB에서는 $V:[0,T]\times\mathbb R^d\to\mathbb R$의 gradient가 **직접 속도나 운동량인 게 아니다.** 먼저 제어집합 $\mathcal U$와 제어 동역학

$$
\dot x(t)=f(x(t),u(t))
$$

이 있고, HJB가 각 $(t,x)$에서

$$
u^*(t,x)
=
\operatorname*{arg\,min}_{u\in\mathcal U}
\left\{
\ell(x,u)+\nabla_xV(t,x)\cdot f(x,u)
\right\}
$$

를 정한다. 즉

$$
\nabla V
\longrightarrow
u^*(t,x)
\longrightarrow
f(x,u^*)
\longrightarrow
\dot x
$$

순서다. 그런 다음 초기상태 $x(0)=x_0$를 주고

$$
\dot x(t)=f\!\left(x(t),u^*(t,x(t))\right)
$$

를 적분해서 $t\mapsto x(t)$라는 최적 상태궤적을 얻는다.

예를 들어 아주 단순하게

$$
f:\mathbb R^d\times\mathbb R^d\to\mathbb R^d,
\qquad
f(x,u)=u
$$

이고 제어비용이

$$
\ell(x,u)=U(x)+\frac{\rho}{2}\|u\|^2
$$

라면

$$
u^*(t,x)=-\frac1\rho\nabla_xV(t,x)
$$

가 되므로,

$$
\dot x(t)
=
-\frac1\rho\nabla_xV(t,x(t)).
$$

이 특수한 경우에는 정말로 **$V$의 gradient 방향을 따라 상태가 움직인다**고 볼 수 있다.

한 줄로 하면 **HJE: $\nabla S\to p\to(x,p)$ 궤적, HJB: $\nabla V\to u^*\to\dot x\to x$ 궤적**이다.

---

## 3. 목적과 필요의 연쇄에 따라 단계적으로 보기

### 사용자
야 수식 중간 중간에 설명을 안하고 그냥 수식만 던질래? 목적과 필요의 연쇄에 따라 단계적으로 번호붙여 설명해.

### ChatGPT
### 1. HJE에서 먼저 알고 싶은 것: “최적 경로의 운동량은 무엇인가?”

상태공간을 $\mathcal X=\mathbb R^d$라 하고, 시간구간을 $[0,T]$라 하자. HJE의 해는 스칼라 함수

$$
S:[0,T]\times\mathbb R^d\to\mathbb R
$$

이다. 여기서 $S(t,x)$는 시각 $t$, 위치 $x$에서의 **action 값**이다.

왜 이 스칼라장이 필요한가 하면, 경로 전체를 일일이 저장하지 않고도 **그 위치에서 어떤 운동량을 가져야 하는지** 얻기 위해서다.

그래서 다음을 정의한다.

$$
p(t)=\nabla_x S(t,x(t)),
\qquad
p(t)\in\mathbb R^d.
$$

즉 $S$를 공간방향으로 미분하면 현재 경로의 운동량 $p(t)$가 나온다.

### 2. 그런데 운동량만 알아서는 위치가 어떻게 움직이는지 모른다

우리가 원하는 것은 실제 상태궤적 $x(t)$다.

운동량 $p(t)$가 주어졌다고 해서 곧바로 $\dot x(t)$가 결정되는 것은 아니고, Hamiltonian

$$
H:\mathbb R^d\times\mathbb R^d\to\mathbb R
$$

이 필요하다.

이 함수는 “현재 위치 $x$와 운동량 $p$가 있을 때 시스템의 에너지 구조가 어떻게 되는가”를 담는다.

그다음 Hamilton 방정식을 쓴다.

$$
\dot x(t)
=
\nabla_p H(x(t),p(t)),
$$

$$
\dot p(t)
=
-\nabla_x H(x(t),p(t)).
$$

목적은 간단하다. 첫 번째 식은 **운동량으로부터 위치의 속도**를 만들고, 두 번째 식은 **위치에 따라 운동량이 어떻게 변하는지** 만든다.

그래서 HJE 쪽 연쇄는

$$
S(t,x)
\rightarrow
\nabla_xS(t,x)
\rightarrow
p(t)
\rightarrow
(\dot x(t),\dot p(t))
\rightarrow
(x(t),p(t))
$$

이다.

즉 최종적으로는 시간마다

$$
t\mapsto (x(t),p(t))
$$

가 찍힌다.

### 3. HJB에서 먼저 알고 싶은 것: “이 상태에서 어떤 제어를 해야 미래 비용이 가장 작나?”

이번에는 제어계가 있다.

상태를 $x(t)\in\mathbb R^d$, 제어를 $u(t)\in\mathcal U$라 하고, 동역학을

$$
\dot x(t)
=
f(x(t),u(t)),
$$

$$
f:\mathbb R^d\times\mathcal U\to\mathbb R^d
$$

라고 하자.

여기서 중요한 점은 HJB의 목적이 바로 $x(t)$를 만드는 게 아니라는 것이다.

먼저

$$
V:[0,T]\times\mathbb R^d\to\mathbb R
$$

라는 optimal value function을 구한다.

$V(t,x)$의 의미는

$$
V(t,x)
=
\text{현재 }(t,x)\text{에서 시작했을 때 앞으로 얻을 수 있는 최소 미래비용}
$$

이다. 즉 HJB의 스칼라장은 **“앞으로 얼마나 비싼 곳인가”를 적어놓은 지도**다.

### 4. 그런데 $V(t,x)$만 있어서는 제어 $u$가 무엇인지 아직 모른다

그래서 현재 제어 $u$를 하나 시험해본다고 생각한다.

즉시비용을

$$
\ell:\mathbb R^d\times\mathcal U\to\mathbb R
$$

라고 하자.

제어 $u$를 쓰면 현재 순간에는

$$
\ell(x,u)
$$

만큼 비용이 든다.

그런데 더 중요한 것은 그 제어가 상태를 움직여서 미래 위치를 바꾼다는 것이다.

상태변화 방향은

$$
f(x,u)
$$

이고, 그 방향으로 움직였을 때 미래비용 $V$가 얼마나 변하는지는

$$
\nabla_xV(t,x)\cdot f(x,u)
$$

로 측정된다.

즉 이 항의 목적은 **“이 제어를 쓰면 가치함수 지도 위에서 비싼 쪽으로 가나, 싼 쪽으로 가나?”**를 보는 것이다.

### 5. 그래서 HJB는 각 제어 후보를 비교한다

현재 제어 $u\in\mathcal U$ 하나의 총 국소적 평가는

$$
\ell(x,u)
+
\nabla_xV(t,x)\cdot f(x,u)
$$

로 생각할 수 있다.

첫 항은 지금 드는 비용, 두 번째 항은 그 제어가 미래비용을 어떻게 바꾸는지다.

그래서 최적 제어를

$$
u^*(t,x)
=
\operatorname*{arg\,min}_{u\in\mathcal U}
\left\{
\ell(x,u)
+
\nabla_xV(t,x)\cdot f(x,u)
\right\}
$$

로 정한다.

이 식의 목적은 **gradient를 제어입력으로 변환하는 것**이다.

즉

$$
\nabla V
\rightarrow
\text{각 }u\text{의 미래비용 변화 계산}
\rightarrow
\operatorname{argmin}
\rightarrow
u^*
$$

이다.

### 6. 이제서야 제어입력이 실제 상태궤적으로 연결된다

HJB가 각 $(t,x)$에서 최적 제어

$$
u^*(t,x)
$$

를 만들어줬다고 하자.

이건 하나의 feedback policy다.

$$
u^*:[0,T]\times\mathbb R^d\to\mathcal U.
$$

이제 실제 현재 상태가 $x(t)$이면 제어기는

$$
u(t)=u^*(t,x(t))
$$

를 출력한다.

그리고 이 제어를 원래 동역학에 넣는다.

$$
\dot x(t)
=
f\!\left(x(t),u^*(t,x(t))\right).
$$

이제 이 ODE를 초기조건

$$
x(0)=x_0
$$

와 함께 적분하면 실제 최적 상태궤적

$$
t\mapsto x(t)
$$

가 나온다.

그러니까 HJB 쪽 전체 연쇄는

$$
V(t,x)
\rightarrow
\nabla_xV(t,x)
\rightarrow
u^*(t,x)
\rightarrow
f(x,u^*)
\rightarrow
\dot x(t)
\rightarrow
x(t).
$$

### 7. HJE와 HJB를 나란히 보면

HJE:

$$
S
\rightarrow
\nabla S
\rightarrow
p
\rightarrow
\text{Hamiltonian dynamics}
\rightarrow
(x(t),p(t)).
$$

HJB:

$$
V
\rightarrow
\nabla V
\rightarrow
u^*
\rightarrow
\text{controlled dynamics}
\rightarrow
x(t).
$$

핵심 차이는 **HJE에서는 gradient가 운동량을 주고, HJB에서는 gradient가 제어를 고르는 기준으로 들어간다**는 것이다.

---

## 4. HJE/HJB의 해에서 바로 궤적이 나오는가?

### 사용자
잠만 HJE든 HJB든 나온해에서 바로 나온 해가 만드는 운동량으로는 궤적이 바로 안나와? 해밀토니안이 따로 주어져야해?

### ChatGPT
**운동량 $p=\nabla_x S$만으로는 일반적으로 위치 궤적 $x(t)$가 바로 안 나온다.** 이유는 운동량 $p$와 속도 $\dot x$가 항상 같은 게 아니기 때문이다.

### 1. HJE의 해가 먼저 주는 것

HJE의 해는

$$
S:[0,T]\times\mathbb R^d\to\mathbb R
$$

이고, 여기서

$$
p(t)=\nabla_x S(t,x(t))
$$

를 얻는다. 하지만 이것은 **운동량**이지 아직 위치의 시간미분 $\dot x(t)$가 아니다.

### 2. 실제 궤적을 얻으려면 운동량을 속도로 바꾸는 법이 필요하다

그 역할을 Hamiltonian

$$
H:\mathbb R^d\times\mathbb R^d\to\mathbb R
$$

이 한다. 구체적으로

$$
\dot x(t)=\nabla_p H(x(t),p(t))
$$

이므로, $p(t)$를 알아도 $H$를 모르면 $\dot x(t)$를 일반적으로 결정할 수 없다.

### 3. 특수한 경우에는 바로 연결된다

예를 들어 질량이 $m>0$인 자유입자에서

$$
H(x,p)=\frac{\|p\|^2}{2m}+U(x)
$$

이면

$$
\dot x=\nabla_p H=\frac{p}{m}.
$$

그래서 이 경우에는

$$
\dot x(t)=\frac1m\nabla_x S(t,x(t))
$$

가 되어 gradient만 봐도 사실상 궤적 ODE가 바로 나온다.

### 4. HJB도 비슷하다

해 $V(t,x)$에서 $\nabla V$가 나와도 그것이 곧 속도는 아니고, 먼저 제어

$$
u^*(t,x)
=
\operatorname*{arg\,min}_{u\in\mathcal U}
\{\ell(x,u)+\nabla V(t,x)\cdot f(x,u)\}
$$

를 정한 뒤

$$
\dot x(t)=f(x(t),u^*(t,x(t)))
$$

로 궤적을 만든다.

핵심은 **HJE에서는 $S$만으로 충분한 게 아니라, HJE 자체에 들어 있던 Hamiltonian $H$가 같이 있어야 궤적이 정해진다**는 것이다. 정확히는 $S$와 $H$가 한 쌍으로 characteristic trajectory를 만든다고 보면 된다.

---

## 5. $\nabla V$와 제어입력 $u$는 어떻게 연결되는가?

### 사용자
잠만 V의 그라디언트와 제어입력은 어떻게 연결돼? HJE때와 달리 뭐 더 거치나?

### ChatGPT
**HJB는 HJE보다 한 단계 더 거친다고 보면 된다.**

### 1. $\nabla_xV$의 의미

HJB의 해는

$$
V:[0,T]\times \mathbb R^d\to\mathbb R
$$

이고, $\nabla_xV(t,x)\in\mathbb R^d$는 **상태를 조금 움직였을 때 최적 미래비용 $V$가 어느 방향으로 얼마나 변하는지** 알려준다.

### 2. HJE와의 차이

HJE에서는 보통

$$
p=\nabla_x S
$$

처럼 gradient가 바로 **costate/운동량 $p$**로 해석된다. 그래서 그다음 Hamiltonian으로

$$
\dot x=\nabla_p H
$$

를 얻는다.

### 3. HJB에서는 $\nabla V$가 바로 제어 $u$가 아니다

현재 제어 $u\in\mathcal U$가 상태를 어떻게 움직이는지는 동역학

$$
f:\mathbb R^d\times\mathcal U\to\mathbb R^d
$$

가 정한다. 그래서 각 후보 $u$에 대해

$$
\nabla_xV(t,x)\cdot f(x,u)
$$

를 계산한다. 이 항은 **“이 제어를 쓰면 value가 증가하나 감소하나”**를 재는 것이다.

### 4. 즉시비용을 함께 본다

거기에 즉시비용

$$
\ell:\mathbb R^d\times\mathcal U\to\mathbb R
$$

까지 더해서

$$
\ell(x,u)+\nabla_xV(t,x)\cdot f(x,u)
$$

를 비교한다.

### 5. 최적 제어를 선택한다

그래서 최적 제어는

$$
u^*(t,x)
=
\operatorname*{arg\,min}_{u\in\mathcal U}
\left\{
\ell(x,u)+\nabla_xV(t,x)\cdot f(x,u)
\right\}
$$

로 얻는다.

즉 연쇄가

$$
\boxed{
\nabla V
\rightarrow
\text{각 }u\text{가 만드는 }f(x,u)
\rightarrow
\nabla V\cdot f(x,u)+\ell(x,u)
\rightarrow
\arg\min
\rightarrow
u^*
}
$$

이다.

그래서 **HJE는 $\nabla S\to p$가 거의 직접 연결이고, HJB는 $\nabla V\to$ 각 제어 후보 평가 $\to u^*$**라고 보면 된다.

---

## 6. 왜 HJB에서는 비용을 더 거치는가?

### 사용자
왜 비용을 더 거치는 거야?

### ChatGPT
이유는 **HJB가 “어느 방향으로 가면 $V$가 줄어드나?”만 보는 문제가 아니라, 그 방향으로 가기 위해 지금 당장 얼마의 비용을 내야 하는지도 같이 최적화하기 때문**이다.

### 1. $\nabla_xV$만 보면 미래비용이 어느 방향으로 줄어드는지만 안다

현재 상태 $x$에서 제어 $u\in\mathcal U$가 동역학

$$
\dot x=f(x,u)
$$

를 만들면, 그 제어로 인해 $V$가 순간적으로 변하는 양은

$$
\nabla_xV(t,x)\cdot f(x,u)
$$

이다.

### 2. 하지만 어떤 제어는 $V$를 빨리 줄여도 제어 자체가 비쌀 수 있다

예를 들어

$$
\ell(x,u)=U(x)+\frac{\rho}{2}\|u\|^2
$$

라면 큰 $u$를 쓰면 목표 쪽으로 빨리 갈 수 있지만 $\|u\|^2$ 때문에 제어비용이 커진다.

### 3. 그래서 현재비용과 미래비용 변화를 함께 본다

HJB는

$$
\ell(x,u)
+
\nabla_xV(t,x)\cdot f(x,u)
$$

를 비교한다.

첫 항은 **지금 제어를 쓰는 즉시비용**, 두 번째 항은 **그 제어 때문에 미래비용이 얼마나 변하는지**다.

즉

$$
\boxed{
\text{지금 드는 비용}
+
\text{그 행동이 미래비용에 주는 변화}
}
$$

를 최소화하는 제어를 고른다.

비용항을 빼면 “미래 $V$를 가장 빨리 낮추는 제어”만 선택하게 되고, 제어를 얼마나 세게 쓰는지가 공짜가 되어버릴 수 있다. HJB는 **현재비용과 미래비용을 동시에 묶어서 최적화**하기 때문에 $\ell$이 들어간다.

---

## 7. 기호와 의미의 대응

### 사용자
기호랑 의미랑 누가누구랑 대응되는데

### ChatGPT
현재 식

$$
u^*(t,x)
=
\operatorname*{arg\,min}_{u\in\mathcal U}
\left\{
\ell(x,u)+\nabla_xV(t,x)\cdot f(x,u)
\right\}
$$

에서 기호 대응은 다음과 같다.

| 기호 | 타입 | 의미 |
|---|---|---|
| $t\in[0,T]$ | 스칼라 | 현재 시간 |
| $x\in\mathbb R^d$ | 상태 벡터 | 현재 상태/위치 |
| $u\in\mathcal U$ | 제어 벡터 | 지금 넣어볼 제어입력 |
| $f:\mathbb R^d\times\mathcal U\to\mathbb R^d$ | 동역학 함수 | 제어 $u$를 넣었을 때 상태가 어느 방향으로 움직이는지 |
| $f(x,u)=\dot x$ | 상태 변화율 벡터 | 실제 이동 방향과 속도 |
| $\ell:\mathbb R^d\times\mathcal U\to\mathbb R$ | 비용 함수 | 현재 상태에서 제어 $u$를 쓰는 즉시비용 |
| $V:[0,T]\times\mathbb R^d\to\mathbb R$ | 스칼라장 | 현재부터 앞으로 최적으로 행동했을 때의 최소 미래비용 |
| $\nabla_xV(t,x)\in\mathbb R^d$ | gradient 벡터 | 상태를 어느 방향으로 움직이면 미래비용 $V$가 얼마나 변하는지 |
| $\nabla_xV\cdot f(x,u)\in\mathbb R$ | 스칼라 | 제어 $u$ 때문에 미래비용이 순간적으로 얼마나 변하는지 |
| $u^*(t,x)\in\mathcal U$ | 최적 제어 | 현재 $(t,x)$에서 실제 선택할 제어 |

대응 관계는 다음과 같다.

$$
\boxed{
u
\overset{f}{\longrightarrow}
\dot x
}
$$

제어 $u$를 넣으면 동역학 $f$가 실제 상태 이동 $\dot x$를 만든다.

그 이동이 value에 미치는 영향은

$$
\boxed{
\dot x=f(x,u)
\quad\Longrightarrow\quad
\nabla V\cdot \dot x
=
\nabla V\cdot f(x,u)
}
$$

이다.

그래서 각 제어 $u$마다

$$
\boxed{
\ell(x,u)
+
\nabla V\cdot f(x,u)
}
$$

를 계산하고, 가장 작은 $u$를 $u^*$로 고른다.

즉 역할만 줄이면

$$
\boxed{
\ell=\text{지금 비용},\qquad
V=\text{미래 비용},\qquad
\nabla V\cdot f=\text{이 제어가 미래 비용을 바꾸는 양}
}
$$

이다.

---

## 8. 왜 $\nabla_xV$와 $u$가 연결되는가?

### 사용자
그라디언트V랑 u랑 뭔상관이길래 그라디언트x함수야?

### ChatGPT
핵심은 **$u$가 $V$에 직접 들어가는 게 아니라, $u$가 상태 $x$를 움직이고 그 $x$를 통해 $V$를 바꾸기 때문**이다.

### 1. 가치함수는 상태 $x$의 함수다

가치함수는

$$
V:[0,T]\times\mathbb R^d\to\mathbb R
$$

이고, $V(t,x)$는 현재 상태 $x$에서의 미래 최소비용이다. 그래서

$$
\nabla_x V(t,x)\in\mathbb R^d
$$

는 **상태 $x$를 어느 방향으로 움직였을 때 $V$가 얼마나 변하는가**를 나타낸다.

### 2. 상태를 움직이는 것은 제어 $u$다

동역학

$$
f:\mathbb R^d\times\mathcal U\to\mathbb R^d
$$

가 주어져서

$$
\dot x(t)=f(x(t),u(t))
$$

가 된다. 즉

$$
u \longrightarrow f(x,u)=\dot x
$$

라는 관계다.

### 3. 알고 싶은 것은 “이 제어 $u$를 넣으면 $V$가 얼마나 변하나?”다

경로 $x(t)$를 따라 $V(t,x(t))$를 시간미분하면 연쇄법칙 때문에

$$
\frac{d}{dt}V(t,x(t))
=
\partial_tV(t,x(t))
+
\nabla_xV(t,x(t))\cdot\dot x(t).
$$

### 4. 여기에 제어 동역학을 대입한다

$\dot x=f(x,u)$였으므로 그대로 대입하면

$$
\frac{d}{dt}V
=
\partial_tV
+
\nabla_xV\cdot f(x,u).
$$

바로 여기서 **$\nabla V$와 $u$의 연결**이 생긴다.

$$
\boxed{
u
\rightarrow
f(x,u)=\dot x
\rightarrow
\nabla V\cdot\dot x
=
\nabla V\cdot f(x,u)
}
$$

즉 **$\nabla V\cdot f(x,u)$**는 뜬금없이 곱한 게 아니라, **제어 $u$가 상태를 움직인 결과로 가치 $V$가 얼마나 빨리 변하는지**를 연쇄법칙으로 계산한 것이다.

그래서 $u$와 $\nabla V$는 직접 연결된 게 아니라

$$
\boxed{u\rightarrow\dot x\rightarrow V\text{의 변화}}
$$

라는 한 단계를 사이에 두고 연결된다.

---

## 핵심 압축

HJE에서는

$$
S
\rightarrow
\nabla S=p
\rightarrow
H
\rightarrow
(\dot x,\dot p)
\rightarrow
(x(t),p(t))
$$

이고,

HJB에서는

$$
V
\rightarrow
\nabla V
\rightarrow
\text{각 제어 }u\text{가 만드는 }f(x,u)\text{ 평가}
\rightarrow
u^*(t,x)
\rightarrow
\dot x=f(x,u^*)
\rightarrow
x(t)
$$

이다.

특히 HJB에서 $\nabla V$와 $u$가 연결되는 이유는

$$
\frac{d}{dt}V(t,x(t))
=
\partial_tV+
\nabla_xV\cdot\dot x
$$

라는 연쇄법칙과

$$
\dot x=f(x,u)
$$

를 결합하면

$$
\frac{d}{dt}V
=
\partial_tV+
\nabla_xV\cdot f(x,u)
$$

가 되기 때문이다.
