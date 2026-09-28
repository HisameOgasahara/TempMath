# 수학의 공통 인터페이스: 동역학의 대상에서 층위별 축약까지

$$
\boxed{
\begin{array}{l}
1.\ \text{무엇이 동역학의 대상인가}\\
\downarrow\\
2.\ \text{그 대상은 어떤 공간과 구조를 가지는가}\\
\downarrow\\
3.\ \text{가능한 경로나 벡터장 중 무엇이 실제 동역학을 정하는가}\\
\downarrow\\
4.\ \text{같은 계를 다른 층위의 객체에서 어떻게 표현하는가}\\
\downarrow\\
5.\ \text{각 층위에서 자유도와 복잡성을 어떻게 줄이는가}
\end{array}
}
$$

라그랑주역학·해밀턴역학·정보기하·수송기하·제어이론은 이 공통 질문에 넣는 대상·공간·구조·법칙에 따라 구체화된다. 동역학을 구성한 뒤에는 같은 계를 상태, 관측량, 분포, 작용·가치함수의 층위에서 표현하고, 각 층위의 자유도와 복잡성을 줄인다.

## 1. 무엇이 동역학의 대상인가

### 1.1 시간에 따라 변하는 객체

| 대상 층위 | 시간에 따라 변하는 객체 | 의미 |
|---|---|---|
| 배치 | $q_t\in Q$ | 위치·자세 등 configuration |
| 위상공간 상태 | $z_t=(q_t,p_t)\in T^*Q$ | 위치와 운동량을 포함한 상태 |
| 장·함수 | $u_t\in\mathcal X$ | 공간 전체에 정의된 함수 |
| 분포 | $\mu_t\in\mathcal P(M)$ | 상태들의 확률법칙 |
| 관측량 | $A_t\in\mathcal F(M)$ | 상태에서 값을 읽는 함수 |
| HJ 생성함수 | $S_t\in\mathcal F(Q)$ | 해밀턴 궤적족을 조직하는 함수 |
| HJB 가치함수 | $V_t\in\mathcal F(M)$ | 각 상태에서의 최적 미래비용 |

같은 물리계에서도 서로 다른 종류의 객체가 진화 대상으로 등장한다. 해밀턴계에서는 위상공간의 점 $z_t$를 추적할 수 있고, 그 흐름이 관측량 함수나 상태분포를 어떻게 변화시키는지 볼 수도 있다.

함수 $S_t$와 $V_t$도 시간에 따라 변하지만, 원래 계의 물리적 상태는 각각 $(q,p)$와 $x$이다. **원래 계의 상태와 그 동역학을 표현하는 객체**를 구별하면 함수의 동역학이 어느 층위에 있는지 명확해진다.

### 1.2 도메인에서 선택하는 대상

| 도메인 | 직접 기술하려는 대상 |
|---|---|
| 라그랑주역학 | 배치 경로 $q_\bullet$; 정칙한 경우 순간 상태 $(q,\dot q)$ |
| 해밀턴역학 | 위상공간 상태 $(q,p)$ |
| 정보기하 | 통계모형의 분포 $p_\theta$, 또는 그 매개변수 $\theta$ |
| 수송기하 | 공간 위의 질량분포 $\mu$ 또는 밀도 $\rho$ |
| 제어이론 | 입력에 따라 변하는 상태 $x$ |

하나의 객체 층위에 여러 도메인이 연결된다. 분포는 정보기하와 수송기하의 대상이면서, 다른 상태동역학으로부터 유도되는 객체일 수도 있다. 소산은 이러한 상태·함수·분포의 운동에서 나타나는 성질이며, 장기 거동은 끌개와 흡인영역을 통해 분석할 수 있다.

### 1.3 순간적인 객체와 경로 전체

순간 상태가 $x_t\in M$이면 운동 전체는

$$
x_\bullet:I\to M
$$

라는 경로다. 라그랑주역학에서는 경로 전체 $q_\bullet$를 작용 functional의 입력으로 삼아 가능한 운동들을 비교한다.

장에서는 $u_t:\Omega\to V$라는 함수 하나가 순간적인 객체이고, 분포에서는 $\mu_t\in\mathcal P(M)$가 순간적인 객체다. 따라서 시간에 따른 변화는 각각 함수들의 경로와 분포들의 경로가 된다.

### 1.4 상태에 포함할 정보의 범위

동역학의 대상을 선택할 때는 객체의 종류와 함께 **어느 범위의 변수를 하나의 상태에 포함하는가**를 정한다. 전체 상태를

$$
z=(x,y)
$$

로 쓰면 $x$는 남길 변수, $y$는 환경이나 내부 운동처럼 직접 추적하지 않을 변수들의 묶음이다. 예를 들어 질량–스프링에서는 $x=(q,p)$에 위치와 운동량을 담고, 주변 유체나 물체 내부의 상세 운동을 $y$에 담을 수 있다.

전체 상태에서 $x$만 남기는 선택은 5절의 축약으로 이어진다. 그 변수들만으로 운동이 닫히는지에 따라 필요한 법칙의 형태도 달라진다. 5.2절에서는 제거한 정보의 효과가 유효 힘·메모리·요동으로 남는 관계를 다룬다.

## 2. 그 대상은 어떤 공간과 구조를 가지는가

### 2.1 기본공간과 대상이 속하는 공간

$$
Q\longrightarrow TQ,\ T^*Q,\ \mathcal F(Q),
\qquad
\Omega\longrightarrow\mathcal X(\Omega),
\qquad
M\longrightarrow\mathcal F(M),\ \mathcal P(M).
$$

| 기본공간 | 대상이 속하는 공간 | 그 공간의 원소 |
|---|---|---|
| 구성다양체 $Q$ | 접다발 $TQ$ | $(q,\dot q)$ |
| 구성다양체 $Q$ | 공접다발 $T^*Q$ | $(q,p)$ |
| 공간 영역 $\Omega$ | 함수공간 $\mathcal X(\Omega)$ | $u_t$ |
| 상태공간 $M$ | 관측량 함수공간 $\mathcal F(M)$ | $A_t$ |
| 상태공간 $M$ | 확률측도 공간 $\mathcal P(M)$ | $\mu_t$ |
| 구성다양체 $Q$ | 함수공간 $\mathcal F(Q)$ | $S_t$ |
| 상태공간 $M$ | 가치함수 공간 | $V_t$ |

해밀턴역학에서는 $Q$로부터 $T^*Q$를 만들고 그 위의 점을 상태로 잡는다. 장에서는 이미 주어진 영역 $\Omega$ 위의 함수 전체를 대상으로 잡는다. 공간의 기하가 먼저 주어지기도 하고, 대상을 담을 공간을 구성하면서 추가 구조가 따라오기도 한다.

$T^*Q$에는 공접다발의 구성에서 canonical symplectic form이 생긴다. 반면 같은 함수공간이나 분포 공간 위에서도 사용할 계량과 정칙성은 별도로 선택할 수 있다.

### 2.2 가능한 변화와 경로

매끄러운 다양체 $M$의 점 $x$에서 가능한 순간변화는 접공간

$$
T_xM
$$

에 속한다. 가능한 경로와 벡터장은 각각

$$
\gamma:I\to M,\qquad X\in\Gamma(TM)
$$

으로 표현한다. 제약이 있으면 허용 상태나 허용 속도의 범위가 제한된다.

함수 $F:M\to\mathbb R$의 differential은

$$
dF_x\in T_x^*M
$$

이다. 이 공변벡터를 실제 변화 방향과 연결하려면 계량이나 심플렉틱 구조 등의 추가 데이터가 필요하다.

### 2.3 공간에 부여하는 공통 구조

| 공통 구조 | 수학적 객체 | 역할 | 구체화 |
|---|---|---|---|
| 미분구조 | $TM$, $T^*M$ | 가능한 속도와 함수의 미분을 정의 | 배치·위상공간, 매끄러운 통계모형 |
| 계량구조 | $g_x(v,w)$ 또는 거리 $d(x,y)$ | 변화의 크기와 공간의 거리를 정의 | Riemannian, Fisher, Wasserstein 기하 |
| 심플렉틱·Poisson 구조 | $\omega$, $\Pi$, $\{A,B\}$ | 공변벡터와 운동 방향, 관측량 사이의 작용을 연결 | 해밀턴역학 |

대상이 사는 공간에 어떤 공통 구조를 주는지에 따라 구체적인 기하가 정해진다. 이 구조와 에너지·작용 등의 데이터를 결합하면 3절의 실제 운동을 구성할 수 있다.

### 2.4 계량구조: 변화의 크기와 거리

Riemannian 계량은 각 접공간에 양의 정부호 대칭 쌍선형형식

$$
g_x:T_xM\times T_xM\to\mathbb R
$$

을 준다. 속도의 크기, 경로의 길이, 그리고 벡터와 공변벡터의 대응

$$
g^\flat_x:T_xM\to T_x^*M,\qquad
v\longmapsto g_x(v,\cdot)
$$

을 정의한다. 이 역대응이 함수의 미분을 기울기 벡터로 바꾸는 데 사용된다.

거리공간에서는 거리 $d$로 경로의 속도와 에너지의 경사를 정의하는 접근도 가능하다. 매끄러운 Riemannian 공간은 이 계량적 접근의 구체적인 경우이며, Wasserstein 공간의 gradient flow도 거리공간의 언어로 구성할 수 있다.

#### 통계모형에 주는 계량: Fisher

통계모형 $\{p_\theta:\theta\in\Theta\}$에서 Fisher 계량은

$$
g_{ij}(\theta)
=\mathbb E_\theta[
\partial_i\log p_\theta\,\partial_j\log p_\theta]
$$

이다. 정칙성·비퇴화 조건 아래 분포족의 접벡터 $\dot\theta$에 크기를 주는 Riemannian 계량이다. KL divergence의 국소 전개에서는

$$
D_{\rm KL}(p_\theta\Vert p_{\theta+d\theta})
=\frac12g_{ij}(\theta)d\theta^i d\theta^j
+O(\|d\theta\|^3)
$$

로 나타난다.

정칙한 최소 지수족

$$
p_\theta(x)
=h(x)\exp\bigl(\langle\theta,T(x)\rangle-\psi(\theta)\bigr)
$$

에서는

$$
\eta=\nabla\psi(\theta),\qquad
g=\nabla^2\psi(\theta)
=\operatorname{Cov}_{p_\theta}[T(X)].
$$

정보기하에서는 이 Fisher 계량에 쌍대 접속 등의 구조를 함께 사용한다. 적절한 divergence의 2차·3차 혼합미분은 계량과 쌍대 접속을 구성하는 데이터가 된다.

#### 분포의 질량 이동에 주는 계량: Wasserstein

바탕 공간의 거리를 사용해 유한 2차 모멘트를 갖는 분포 공간 $\mathcal P_2(M)$에 Wasserstein 거리 $W_2$를 준다.

유클리드 공간의 매끄러운 밀도에서는 변화 $\dot\rho$를

$$
\dot\rho+\nabla\cdot(\rho v)=0
$$

으로 표현하고, 그 변화를 만드는 속도장 중 최소 운동비용을 사용해 형식적으로

$$
\|\dot\rho\|_{W_2,\rho}^2
=\inf_{v:\,\dot\rho+\nabla\cdot(\rho v)=0}
\int\rho|v|^2\,dx
$$

로 크기를 정의한다. 이는 매끄러운 밀도에 대한 형식적 Riemannian 해석이고, 일반 측도에는 $W_2$ 거리 자체를 사용한다.

Fisher는 분포의 통계적 구별 가능성으로, Wasserstein은 질량을 옮기는 비용으로 변화의 크기를 정한다. 둘은 분포를 대상으로 하는 계량구조의 서로 다른 구체화다.

### 2.5 심플렉틱·Poisson 구조: 반대칭 대응

심플렉틱 구조는 닫힌 비퇴화 2-form

$$
\omega\in\Omega^2(M)
$$

이다. 각 점에서

$$
\omega^\flat_x:T_xM\to T_x^*M,\qquad
v\longmapsto\iota_v\omega
$$

라는 가역 대응을 준다. 계량의 대칭 대응과 달리 $\omega$는 반대칭이며, 3절에서는 그 역대응에 $dH$를 넣어 Hamiltonian 벡터장을 정한다.

공접다발 $T^*Q$의 canonical symplectic form은 이 구조의 대표적인 구현이다. Poisson 구조는 퇴화할 수 있는 반대칭 대응

$$
\Pi^\sharp:T^*M\to TM
$$

과 관측량의 괄호를 제공하며, Jacobi 항등식과 양립한다. 심플렉틱 구조는 비퇴화한 Poisson 구조에 대응한다.

### 2.6 미분방정식의 대상과 상태방정식의 공간

유한차원 상태 $x(t)\in M$와 함수값 상태 $u(t)\in\mathcal X$는 각각

$$
\dot x=F(x),
\qquad
\frac{d}{dt}u(t)=\mathcal G(u(t))
$$

로 진화한다. 시간 진화형 PDE에서는 한 시점의 함수 전체를 상태로 잡는다. 예를 들어 열방정식은

$$
\partial_tu=\Delta u
\quad\longleftrightarrow\quad
\frac{d}{dt}u(t)=Au(t),
\qquad
A=\Delta:D(A)\subseteq\mathcal X\to\mathcal X
$$

로 읽힌다. $\mathcal X$는 함수공간이고 $D(A)$는 필요한 공간 정칙성과 경계조건을 반영한다.

고계 ODE도 필요한 시간미분을 상태에 포함해 1차 상태방정식으로 바꿀 수 있다. 라그랑주역학에서 $(q,\dot q)$를 상태로 잡는 것이 그 예다. 따라서 ODE/PDE라는 식의 형태와, 어떤 객체를 상태로 잡는지가 연결된다.

---

**공간에서 법칙으로: 대상에 대한 연산자 작용**

바탕 공간 $\Omega$ 위의 함수나 장을 $u\in\mathcal X(\Omega)$로 잡으면, 미분연산자는 그 대상에 작용한다.

$$
\Omega
\longrightarrow
u\in\mathcal X(\Omega),
\qquad
L:D(L)\subseteq\mathcal X(\Omega)\to\mathcal Y.
$$

여기서 $\Omega$는 함수의 정의역이고, $\mathcal X(\Omega)$는 함수 자체가 속하는 공간이다. 방정식 $Lu=f$는 이 함수공간의 대상에 부과하는 관계다. 경로를 미지 대상으로 잡으면 시간미분을 포함한 연산자가 경로공간에 작용한다.

이 작용을 대수적으로 조직하면 모듈 구조가 된다. $K$-벡터공간 $E$의 선형연산자 $A:E\to E$에 대해

$$
p(\zeta)\cdot v:=p(A)v
$$

로 정의하면 $E$는 $K[\zeta]$-모듈이다. 미분에 닫힌 함수공간에서는 $D=d/dt$의 작용으로 $K[D]$-모듈을 구성하고, 상수계수 미분방정식을

$$
p(D)u=f
$$

라는 관계로 읽을 수 있다. 변수계수 미분연산자에는 함수의 곱셈과 미분이 이루는 비가환 연산자 대수를 사용한다. 비유계 연산자에서는 작용의 정의역도 함께 지정한다.

$$
\boxed{
\text{대상이 속한 공간}
\longrightarrow
\text{대상에 대한 연산자 작용}
\longrightarrow
\text{방정식·동역학의 선택}
}
$$

기하구조는 가능한 변화와 그 관계를 제공하고, 연산자 작용은 대상에 수행하는 연산을 표현한다. 실제 법칙은 이 구조들을 사용해 특정 벡터장·생성자·변분 조건 등을 선택한다. 선택된 선형 작용의 다항식 관계는 4절에서 모듈·스펙트럼·대수기하로 연결된다.

---

## 3. 가능한 경로나 벡터장 중 무엇이 실제 동역학을 정하는가

공간과 구조가 주어지면 여러 경로와 벡터장을 생각할 수 있다. 실제 운동을 정하는 주요 방식은 **함수·functional의 미분을 기하구조로 벡터장에 대응시키는 것**이다. 라그랑주역학에서는 경로에 대한 작용을 변분해 운동을 선택하고, 제어에서는 허용 운동 중 입력이나 정책으로 실제 운동을 선택한다.

### 3.1 공통 구조: 미분에서 벡터장으로

함수 또는 functional

$$
F:M\to\mathbb R
$$

가 주어지면 그 미분은

$$
dF_x\in T_x^*M
$$

이다. $dF_x$는 가능한 변화 $\delta x$에 대해 $F$가 얼마나 변하는지 평가하는 공변벡터다.

$$
\delta x\in T_xM
\quad\longmapsto\quad
dF_x[\delta x]\in\mathbb R.
$$

실제 운동의 속도는 $T_xM$의 벡터이므로, 이 미분을 벡터로 대응시키는 구조가 필요하다. 2절에서 정한 계량·심플렉틱 구조·이동도 등이 그 역할을 한다.

$$
\boxed{
\begin{array}{c}
\text{함수·functional }F\\
\downarrow\ \text{미분·변분}\\
dF_x\in T_x^*M\\
\downarrow\ \text{기하구조에 의한 대응}\\
X_F(x)\in T_xM\\
\downarrow\ \dot x=X_F(x)\\
\text{실제 흐름}
\end{array}
}
$$

형식적으로는 대응 사상 $\mathcal B_x:T_x^*M\to T_xM$를 사용해

$$
X_F(x)=\mathcal B_x(dF_x)
$$

로 쓸 수 있다. 어떤 $F$를 주는지, 어떤 구조로 대응시키는지, 하강·상승 등 어느 운동 규칙을 선택하는지에 따라 실제 벡터장이 정해진다.

함수공간과 분포 공간에서도 같은 역할 구분을 사용한다. 이때 변분미분, 접공간, 대응 연산자의 정의역과 정칙성은 해당 공간에 맞게 해석한다.

### 3.2 같은 공통 구조의 서로 다른 구현

| 구현 | 미분하는 대상 | 미분을 벡터로 보내는 구조 | 실제 운동 |
|---|---|---|---|
| 해밀턴역학 | Hamiltonian $H$ | 심플렉틱 구조의 대응 또는 Poisson 구조 | $\iota_{X_H}\omega=dH$, $\dot z=X_H$ |
| 정보기하의 하강 흐름 | 목적함수 $F(\theta)$ | Fisher 계량의 역대응과 하강 부호 | $\dot\theta=-g_{\rm Fisher}^{\sharp}dF$ |
| 수송기하의 하강 흐름 | 분포 에너지 $\mathcal F[\rho]$ | Wasserstein 구조와 하강 부호 | $\partial_t\rho=\nabla\cdot(\rho\nabla\frac{\delta\mathcal F}{\delta\rho})$ |

정보기하와 수송기하는 이 대응에 사용하는 기하를 제공한다. 목적함수와 하강 규칙을 결합한 흐름은 각각의 기하에서 동역학을 구성하는 대표적인 구현이다.

#### 해밀턴역학: 심플렉틱 구조의 대응

심플렉틱 구조가 주는 사상은

$$
\omega^\flat_x:T_xM\to T_x^*M,
\qquad
v\longmapsto\iota_v\omega
$$

이다. 비퇴화성 때문에 역대응이 존재하므로

$$
X_H=(\omega^\flat)^{-1}dH
$$

로 운동을 정한다. $T^*Q$에서 $\omega=\sum_i dq^i\wedge dp_i$를 사용하면

$$
\dot q^i=\frac{\partial H}{\partial p_i},
\qquad
\dot p_i=-\frac{\partial H}{\partial q^i}.
$$

자율계에서는 반대칭성에 의해

$$
\frac{dH}{dt}=dH[X_H]=\omega(X_H,X_H)=0
$$

이다. Poisson 구조에서도 $dH$를 벡터장으로 대응시킬 수 있으며, 그 대응은 퇴화할 수 있다.

#### 계량·이동도로 하강 방향 구성

Riemannian 계량은

$$
g^\flat_x(v)=g_x(v,\cdot)
$$

로 벡터와 공변벡터를 연결한다. 역대응을 $g^\sharp$라 하면

$$
\operatorname{grad}_gF=g^\sharp dF.
$$

여기에 하강 규칙을 선택하면

$$
\dot x=-\operatorname{grad}_gF,
\qquad
\frac{dF}{dt}
=-g(\operatorname{grad}_gF,\operatorname{grad}_gF)\leq0.
$$

더 일반적으로 대칭 양의 준정부호 이동도 $K_x:T_x^*M\to T_xM$를 사용하면

$$
\dot x=-K_xdF_x,\qquad
\frac{dF}{dt}=-\langle dF_x,K_xdF_x\rangle\leq0.
$$

심플렉틱 대응의 반대칭성은 에너지 보존에, 계량·이동도의 양의 성질과 하강 부호는 에너지 감소에 연결된다.

#### 정보기하: Fisher 계량을 대입

정칙한 통계모형에서 가역인 Fisher 계량과 목적함수 $F(\theta)$를 선택하면

$$
dF=\partial_jF\,d\theta^j
\quad\longmapsto\quad
\operatorname{grad}_{g_{\rm Fisher}}F
=g^{ij}(\theta)\partial_jF\,\partial_i.
$$

하강 규칙을 선택한 자연기울기 흐름은

$$
\dot\theta^i=-g^{ij}(\theta)\partial_jF(\theta)
$$

이다. 일반적인 계량 gradient flow에 Fisher 구조를 넣은 것이다. 이 매개변수 경로는 $p_{\theta_t}$라는 분포 경로를 유도한다.

#### 수송기하: Wasserstein 구조를 대입

분포 에너지 $\mathcal F[\rho]$의 변분미분은 밀도 변화에 대한 에너지 변화를 평가한다.

$$
D\mathcal F[\rho](\delta\rho)
=\int\frac{\delta\mathcal F}{\delta\rho}\,\delta\rho\,dx.
$$

질량을 보존하는 변분에서는 변분미분을 상수 차이까지 동일하게 취급한다. 유클리드 공간의 매끄러운 밀도와 적절한 경계조건 아래 Wasserstein 대응은 형식적으로

$$
\operatorname{grad}_{W_2}\mathcal F(\rho)
=-\nabla\cdot\left(\rho\nabla\frac{\delta\mathcal F}{\delta\rho}\right)
$$

가 된다. 따라서 하강 흐름은

$$
\partial_t\rho
=-\operatorname{grad}_{W_2}\mathcal F(\rho)
=\nabla\cdot\left(\rho\nabla\frac{\delta\mathcal F}{\delta\rho}\right).
$$

여기서 분포 공간의 접벡터는 밀도의 변화 $\partial_t\rho$이다. 이를 질량 이동 속도

$$
v=-\nabla\frac{\delta\mathcal F}{\delta\rho}
$$

와 연속방정식 $\partial_t\rho+\nabla\cdot(\rho v)=0$으로 표현할 수 있다.

예를 들어 $\beta>0$에 대해

$$
\mathcal F[\rho]
=\int U(x)\rho(x)\,dx
+\beta^{-1}\int\rho(x)\log\rho(x)\,dx
$$

를 주면

$$
\partial_t\rho
=\nabla\cdot(\rho\nabla U)+\beta^{-1}\Delta\rho.
$$

이 역시 functional의 미분을 기하구조로 변화 방향에 대응시키는 같은 구성이다.

### 3.3 라그랑주역학: 경로의 작용을 변분해 운동 선택

라그랑지언

$$
L:TQ\to\mathbb R
$$

으로부터 경로의 작용

$$
\mathscr S[q]=\int_{t_0}^{t_1}L(q,\dot q)\,dt
$$

을 만든다. 여기서 변분의 대상은 경로 전체이고, 끝점이 고정된 허용 변분에 대해

$$
D\mathscr S[q](\delta q)=0
$$

을 요구한다. 이 정류 조건으로

$$
\frac{d}{dt}\frac{\partial L}{\partial\dot q^i}
-\frac{\partial L}{\partial q^i}=0
$$

을 얻는다.

$$
\boxed{
L
\longrightarrow
\mathscr S[q]
\longrightarrow
\text{경로에 대한 변분}
\longrightarrow
\text{정류 조건}
\longrightarrow
\text{운동 경로}
}
$$

이 구성에서는 작용의 미분을 허용 변분에 대해 0으로 두어 경로를 선택한다. 앞의 구성은 순간 상태 위 함수의 미분을 벡터장으로 대응시켜 운동을 정한다.

속도 Hessian이 가역인 정칙한 경우에는 Euler–Lagrange 식을 $TQ$ 위의 1차 동역학으로 읽을 수 있다. 또한 Legendre 사상이 가역인 영역에서

$$
p_i=\frac{\partial L}{\partial\dot q^i},\qquad
H(q,p)=p\cdot\dot q-L(q,\dot q)
$$

로 해밀턴 표현에 연결된다. 같은 운동이 경로의 정류 조건과 기하구조에 의한 벡터장 선택이라는 두 방식으로 표현된다.

### 3.4 제어이론: 허용 벡터장 중 입력으로 운동 선택

제어계

$$
\dot x=f(x,u,t),\qquad u(t)\in\mathcal U
$$

는 입력에 따라 선택할 수 있는 운동을 정한다. 입력 경로 $u(t)$ 또는 피드백 $u=\pi(t,x)$를 주면 실제 운동법칙이 선택된다.

Control-affine 계에서는

$$
\dot x=X_0(x)+\sum_i u_i(t)X_i(x)
$$

로 표현한다. 주어진 벡터장들의 결합을 입력으로 선택하는 것이다. 최적 입력을 찾으려면 비용 functional을 추가하고, 그 문제는 4절의 가치함수 표현으로 연결된다.

제어계가 해밀턴·소산 구조를 갖는 경우에는 앞에서 구성한 벡터장에 입력을 결합할 수 있다. 따라서 제어의 입력 선택은 기하로 운동을 구성하는 방식과 함께 사용될 수 있다.

### 3.5 선택한 법칙에서 실제 경로로

벡터장 $X$가 정해진 뒤

$$
\dot x=X(x),\qquad x(0)=x_0
$$

를 풀면 해당 초기값의 경로를 얻는다. 해의 존재·유일성이 확보된 범위에서 이를 초기값마다 모으면 flow $\Phi_t$가 된다.

이때 해 경로집합은

$$
\operatorname{Sol}_I(X)
=\{\gamma:I\to M:\dot\gamma=X(\gamma)\}
$$

으로 경로공간에 놓인다. 허용 상태공간 $M$과 그 위에서 법칙을 만족하는 경로들의 집합은 구별된다.

### 3.6 미분방정식의 생성자에서 상태의 진화로

기하구조로 구성한 벡터장도 상태방정식의 우변을 정한다. 선형 상태동역학에서는 이 역할을 생성자 $A$가 담당한다.

$$
\dot x=Ax,
\qquad
\partial_tu=Au.
$$

유한차원에서는 $x(t)=e^{tA}x_0$이고, 함수공간에서는 적절한 생성 조건 아래 반군 $T_t$를 사용해

$$
u(t)=T_tu_0,\qquad T_{t+s}=T_tT_s
$$

로 표현한다. 해밀턴 벡터장의 흐름과 소산 PDE의 반군은 각각 선택한 무한소 법칙을 유한시간 진화에 연결하는 구현이다.

$$
\boxed{
\text{벡터장·생성자}
\longrightarrow
\text{ODE/PDE 또는 상태방정식}
\longrightarrow
\text{flow·반군}
}
$$

이 진화를 함수·분포·주파수 영역에서 표현하면 작용의 분해와 가역성을 해당 표현의 도구로 분석할 수 있다.

## 4. 같은 계를 다른 층위의 객체에서 어떻게 표현하는가

| 층위 | 진화하는 객체 | 원래 동역학과의 연결 |
|---|---|---|
| 상태 | $x_t\in M$ | flow $\Phi_t$로 상태를 이동 |
| 관측량 | $A_t\in\mathcal F(M)$ | flow가 관측량 함수에 작용 |
| 분포 | $\mu_t\in\mathcal P(M)$ | flow 또는 전이법칙으로 분포를 이동 |
| HJ 생성함수 | $S_t:Q\to\mathbb R$ | $dS_t$가 조직하는 해밀턴 궤적족 |
| HJB 가치함수 | $V_t:M\to\mathbb R$ | 제어와 비용으로 정의한 최적 미래비용 |

각 표현의 연결에는 필요한 조건과 데이터가 있다. 특히 HJB에는 제어계에 비용과 최적화 문제가 추가되고, 하나의 HJ 생성함수는 그 함수로 표현되는 궤적족을 담는다.

### 4.1 상태에서 관측량으로

상태 flow가

$$
x_t=\Phi_t(x_0)
$$

이면 관측량 $A:M\to\mathbb R$에

$$
(U_tA)(x)=A(\Phi_t(x))
$$

가 작용한다. $U_t$는 관측량 함수공간의 Koopman operator다.

$$
x_0\mapsto\Phi_t(x_0)
\qquad\longleftrightarrow\qquad
A\mapsto U_tA.
$$

벡터장이 $X$이면 관측량 생성자는 $\mathcal LA=X[A]$이다. 해밀턴계에서는

$$
\mathcal LA=\{A,H\}
$$

가 된다. 상태 경로를 직접 보는 것과 관측량 함수의 진화를 보는 것이 같은 동역학에 연결된다.

### 4.2 상태에서 분포로

초기 상태분포가 $\mu_0$이면

$$
\mu_t=(\Phi_t)_\#\mu_0.
$$

관측량과 분포의 진화는

$$
\int A\,d\mu_t=\int U_tA\,d\mu_0
$$

로 쌍대적으로 연결된다. 매끄러운 밀도가 존재하는 유클리드 공간에서는

$$
\partial_t\rho+\nabla\cdot(\rho X)=0
$$

이라는 연속방정식으로 나타난다. 해밀턴계의 분포 진화는 Liouville 표현으로 이어진다.

확률적 운동에서는

$$
(P_tA)(x)=\mathbb E[A(X_t)\mid X_0=x],
\qquad
\mu_t=P_t^*\mu_0
$$

를 사용한다. 관측량 생성자가 $\mathcal L$이면 분포는 수반 생성자 $\mathcal L^*$로 진화한다.

수송·소산 흐름의 경우

$$
dX_t=-\nabla U(X_t)\,dt+\sqrt{2\beta^{-1}}\,dW_t
$$

의 밀도 진화는

$$
\partial_t\rho
=\nabla\cdot(\rho\nabla U)+\beta^{-1}\Delta\rho
$$

가 되어 3.2절의 Wasserstein gradient flow와 연결된다. 이러한 연결은 해당 에너지·확산 구조가 맞는 경우에 성립한다.

### 4.3 해밀턴 상태에서 HJ 생성함수로

해밀턴계의 상태는 $(q,p)\in T^*Q$이고, 생성함수는

$$
S:I\times Q\to\mathbb R
$$

이다. 각 시간에

$$
p=d_qS(t,q),
\qquad
q\longmapsto(q,d_qS(t,q))
$$

를 통해 $T^*Q$ 안의 Lagrangian 그래프를 구성한다.

Hamilton–Jacobi 방정식은

$$
\partial_tS(t,q)+H(q,d_qS(t,q),t)=0.
$$

매끄러운 해가 존재하는 영역에서 특성곡선은

$$
\dot q=\partial_pH(q,d_qS,t),\qquad p=d_qS(t,q)
$$

로 Hamilton 운동에 연결된다.

따라서 궤적을 하나씩 추적하는 표현에서, 그 궤적족을 조직하는 함수 $S_t$의 진화로 옮겨 간다. 생성함수의 초기자료와 그래프가 유지되는 범위가 어떤 궤적족을 표현하는지 정한다.

### 4.4 제어 상태에서 HJB 가치함수로

제어계 $\dot x=f(x,u,t)$에 누적 비용 $\ell$, 종단 비용 $\varphi$를 주면

$$
V(t,x)=\inf_{u_\bullet}
\left\{\int_t^T\ell(x_s,u_s,s)\,ds+\varphi(x_T)\right\},
\qquad x_t=x
$$

가 각 상태에서의 최적 미래비용을 담는다. 매끄러운 경우

$$
\partial_tV+\inf_{u\in\mathcal U}
\{\ell(x,u,t)+d_xV[f(x,u,t)]\}=0,
\qquad V(T,x)=\varphi(x)
$$

이라는 HJB 방정식을 얻는다.

최솟값을 달성하는 적절한 선택자가 존재하면

$$
d_xV
\longrightarrow
u^*(t,x)\in\arg\min_u\{\ell+d_xV[f]\}
\longrightarrow
\dot x=f(x,u^*(t,x),t)
$$

로 최적 상태궤적을 구한다. 비매끄러운 가치함수에는 viscosity solution 등의 해 개념을 사용한다.

HJ의 $dS$는 운동량에, HJB의 $dV$는 비용과 입력 법칙을 통한 최적 입력 선택에 연결된다. 두 경우 모두 함수의 진화를 원래 상태의 운동과 연결해 읽는다.

### 4.5 조화해석: 미분 작용을 모드별 작용으로 표현

관측량·분포·생성함수로 옮기는 경우에는 진화하는 객체의 종류가 달라진다. Fourier/Laplace 변환에서는 주어진 상태나 함수를 주파수·복소변수로 표현한다.

선형연산자의 고유모드 $Av=\lambda v$에서는 작용이 스칼라 곱으로 단순화된다. 무한차원 self-adjoint 연산자는 스펙트럼 측도 $E_A$를 사용해

$$
A=\int_{\sigma(A)}\lambda\,dE_A(\lambda)
$$

로 표현할 수 있다. 연속 스펙트럼까지 포함하므로 이산 고유벡터의 합보다 넓은 분해다.

대칭군의 표현이 주어지면 적절한 조건 아래 불변 성분으로 분해한다. 특히 유클리드 공간의 평행이동에 대응하는 Fourier 모드는 $e^{i\xi\cdot x}$이다. 적절한 함수공간에서

$$
\widehat{\partial_j u}(\xi)=i\xi_j\widehat u(\xi),
\qquad
\widehat{P(\partial)u}(\xi)=P(i\xi)\widehat u(\xi)
$$

이므로 상수계수 미분연산자의 작용이 주파수별 곱셈으로 바뀐다.

$$
\boxed{
\text{미분연산자의 작용}
\longrightarrow
\text{대칭·스펙트럼에 따른 모드}
\longrightarrow
\text{모드별 곱셈}
}
$$

전체 모드를 유지하면 표현을 바꾼 것이고, 일부 모드만 남기는 일은 5절의 축약이다.

### 4.6 상태방정식·Laplace 변환·리졸벤트의 연결

선형 상태방정식

$$
\dot x=Ax+Bu,\qquad y=Cx
$$

을 단측 Laplace 변환하면

$$
(sI-A)\widehat x(s)=x_0+B\widehat u(s).
$$

리졸벤트

$$
R(s,A)=(sI-A)^{-1}
$$

를 사용하면

$$
\widehat x(s)=R(s,A)x_0+R(s,A)B\widehat u(s).
$$

따라서 리졸벤트는 상태진화의 생성자를 초기값·입력에 대한 응답으로 연결한다. 영 초기조건에서 전달함수는

$$
G(s)=CR(s,A)B
$$

이다. 전달함수의 극은 입력·출력에 나타나는 모드와 pole-zero cancellation을 반영한다. 내부 상태의 전체 모드는 상태연산자의 고유값으로 분석한다.

함수공간의 강연속 반군도 적절한 수렴 반평면에서

$$
R(s,A)v=\int_0^\infty e^{-st}T_tv\,dt
$$

로 연결된다. 역연산자가 적분핵으로 표현되는 경우에는 Green function으로 응답을 기술할 수 있다.

$$
\boxed{
A
\longrightarrow
T_t
\quad\longleftrightarrow\quad
R(s,A)
\longrightarrow
\text{초기값·입력 응답}
}
$$

리졸벤트가 유계 역연산자로 존재하는 영역과 그 여집합인 스펙트럼이 연산자의 가역성을 구별한다. 유한차원에서는 고유값이 리졸벤트의 극이 된다. 무한차원에서는 연속 스펙트럼 등도 함께 다룬다.

### 4.7 미분방정식의 모드와 다항식의 영점

상수계수 미분연산자 $P(D)$에 대해

$$
P(D)e^{st}=P(s)e^{st}
$$

이므로 $P(D)u=0$의 지수 모드는 $P(s)=0$에서 정해진다. 거듭제곱 인자가 있으면 $t^ke^{st}$ 형태의 일반화된 모드도 생긴다.

$$
\boxed{
\text{시간 영역의 미분방정식}
\longrightarrow
\text{복소변수의 다항식 관계}
\longrightarrow
\text{영점과 중복도}
}
$$

여러 변수의 상수계수 PDE에서도 symbol의 다항식 관계를 사용한다. 주파수 영역에서는 $P(i\xi)$가 작용하며, PDE의 characteristic set에는 보통 principal symbol을 사용한다. 미분 작용의 표현이 다항식의 영점 기하에 연결되는 지점이다.

### 4.8 모듈·대수기하·리졸벤트를 함께 읽기

유한차원 복소벡터공간 $E$의 선형연산자 $A$에 대해 $p(\zeta)\cdot v=p(A)v$로 $\mathbb C[\zeta]$-모듈을 구성하자. 연산자가 만족하는 다항식 관계는 annihilator

$$
\operatorname{Ann}_{\mathbb C[\zeta]}(E)
=\{p:p(A)=0\}
=(m_A)
$$

에 담긴다. $m_A$는 최소다항식이다.

모듈이 살아 있는 소아이디얼들을 모은 support는

$$
\operatorname{Supp}_{\mathbb C[\zeta]}(E)
=\{\mathfrak p:E_{\mathfrak p}\neq0\}
=V(m_A)\subseteq\operatorname{Spec}\mathbb C[\zeta].
$$

이 유한차원 경우 support의 점 $(\zeta-\lambda)$들은 $A$의 고유값에 대응한다. 각 점에서 모듈을 국소화하면 해당 일반화 고유값 성분을 분리해 볼 수 있다.

$$
\boxed{
A
\longrightarrow
\mathbb C[\zeta]\text{-모듈 }E
\longrightarrow
\operatorname{Ann}(E)
\longrightarrow
\operatorname{Supp}(E)
}
$$

$\operatorname{Spec}\bigl(\mathbb C[\zeta]/(m_A)\bigr)$의 구조층에는 최소다항식의 거듭제곱 관계가 남는다. 예를 들어 한 일반화 고유공간에서

$$
A=\lambda I+N,\qquad N^r=0,\quad N^{r-1}\neq0
$$

이면 해당 최소다항식 인자는 $(\zeta-\lambda)^r$이다. 같은 성분의 리졸벤트는

$$
R(s,A)
=\frac{I}{s-\lambda}
+\frac{N}{(s-\lambda)^2}
+\cdots+
\frac{N^{r-1}}{(s-\lambda)^r}.
$$

고유값은 support의 점으로, nilpotent 관계는 그 점의 비축약 구조로, 최대 Jordan block의 크기는 리졸벤트의 극 차수로 연결된다. 각 Jordan block의 개수와 크기는 모듈 전체에 담긴다.

일반적으로 $\mathbb C[\zeta_1,\ldots,\zeta_n]/I$의 닫힌 점은 다항식들의 공통 영점 $V(I)$와 연결된다. 가환하는 여러 연산자도 이런 다항식환의 작용으로 볼 수 있다.

연산자 스펙트럼 $\sigma(A)$와 환의 소아이디얼 공간 $\operatorname{Spec}R$는 이 모듈 구성을 통해 연결된다. 리졸벤트의 극은 역연산자의 특이성을 나타낸다. 바탕 공간 $\operatorname{Spec}\mathbb C[\zeta]$는 매끄러운 아핀 직선이며, 모듈의 관계는 그 위의 support와 구조층을 통해 읽는다. 함수공간의 비유계 연산자로 확장할 때는 위상·정의역·연속 스펙트럼을 추가로 고려한다.

## 5. 각 층위에서 자유도와 복잡성을 어떻게 줄이는가

| 축약할 층위 | 남기는 객체 | 대표 방법 |
|---|---|---|
| 상태 | 동치류, 느린 변수, 선택한 모드 | 대칭축약, center/slow manifold, modal truncation |
| 관측량 | 유한 관측량 부분공간 | Koopman 부분공간·모드 절단 |
| 분포 | 모멘트 또는 분포족의 매개변수 | moment closure, 유한차원 분포족 투영 |
| HJ/HJB | 작용·가치함수의 기저 계수 | basis approximation, reduced ansatz |

### 5.1 상태 층위의 축약

대칭에 의해 동등한 상태를 묶으면

$$
M\longrightarrow M/G
$$

라는 quotient를 생각할 수 있다. 군의 작용과 운동이 양립하고 필요한 정칙성이 있으면 quotient 위에 동역학을 내린다. 보존량의 준위집합과 불변 구조도 운동이 놓이는 범위를 제한한다.

불변다양체 $N\subseteq M$에서는 벡터장이 $T_xN$에 접하므로 그 안에서 시작한 운동을 제한해 기술한다. Center manifold는 평형점 부근의 국소 거동을, slow manifold는 시간척도 분리가 있는 경우 느린 운동을 다룬다.

장이나 고차원 상태를

$$
x(t)\approx\sum_{j=1}^kc_j(t)\phi_j
$$

로 표현하면 선택한 모드의 계수만 남긴다. 버린 성분의 영향이 남은 변수에 어떻게 반영되는지에 따라 정확한 축약이나 근사 모델이 된다.

일반적인 축약 사상 $r:M\to N$에 대해

$$
Dr_xX(x)=\bar X(r(x))
$$

인 $\bar X$가 존재하면 $y=r(x)$의 운동이 $\dot y=\bar X(y)$로 정확히 닫힌다. 그렇지 않으면 추가 변수나 폐쇄 가정 등이 필요하다.

전체 상태에서 일부 변수만 남기는 경우에도 같은 닫힘의 문제가 생긴다. 5.2절에서는 이 선택을 $z=(x,y)\mapsto x$로 쓰고, 제거한 변수의 영향을 유효 운동법칙에 남기는 과정을 살핀다.

### 5.2 보존적 모델에서 현실적 동역학으로: 유효항과 장기 거동

#### ① 익숙한 보존 모델에서 감쇠·구동이 있는 모델로

질량–스프링에서는 물체의 위치 $q$와 운동량을, LC 회로에서는 전하 $Q$와 전류 $I=\dot Q$를 남겨 운동을 기술한다. 점 하나는 시간에 따른 변화율, 점 둘은 그 변화율의 변화다. 따라서 $\dot q$는 속도, $\ddot q$는 가속도다.

손실과 외부 구동을 생략한 이상적 모델은

$$
m\ddot q+kq=0,
\qquad
L\ddot Q+\frac{Q}{C}=0.
$$

여기서 $m$은 질량, $k$는 스프링 상수, $L$은 인덕턴스, $C$는 정전용량이다. 각각의 에너지는

$$
E_{\rm mech}=\frac12m\dot q^2+\frac12kq^2,
\qquad
E_{\rm LC}=\frac12L\dot Q^2+\frac{Q^2}{2C}.
$$

질량–스프링에서는 운동에너지와 탄성에너지가, LC에서는 자기장과 전기장의 에너지가 교환된다. 이상적 모델에서 각 합은 일정하다.

감쇠와 외부 입력을 포함하면

$$
m\ddot q+c\dot q+kq=f(t),
\qquad
L\ddot Q+R\dot Q+\frac{Q}{C}=V_{\rm ext}(t).
$$

| 역할 | 질량–스프링–댐퍼 | RLC 회로 |
|---|---|---|
| 운동의 변화에 대응하는 항 | 관성 $m\ddot q$ | $L\ddot Q$ |
| 운동을 감쇠시키는 항 | $c\dot q$ | 저항에 의한 $R\dot Q$ |
| 복원항 | $kq$ | $Q/C$ |
| 외부 구동 | 힘 $f(t)$ | 전압 $V_{\rm ext}(t)$ |

힘에 속도를 곱하면 단위시간당 전달되는 에너지, 즉 일이 전달되는 속도가 된다. 전압과 전류의 곱도 같은 역할을 한다. 운동방정식을 이용하면

$$
\frac{dE_{\rm mech}}{dt}
=-c\dot q^2+f(t)\dot q,
\qquad
\frac{dE_{\rm LC}}{dt}
=-R\dot Q^2+V_{\rm ext}(t)\dot Q.
$$

첫 항은 소산에 따른 에너지의 시간당 변화량이고, 둘째 항은 외부와의 에너지 교환률이다. 빠져나간 에너지는 주변 유체나 재료의 미시 운동 등으로 전달될 수 있다.

보존적 이상화에서 구체적인 대상을 기술할 때는 계의 경계와 관측 해상도를 선택한다. 효과를 무시하는 이상화와, 상세 자유도를 제거하면서 그 효과를 유효항으로 남기는 축약을 구분해 읽는다.

| 계·상황 | 남기는 변수 | 생략하거나 제거하는 상세 자유도 | 남는 효과·항 |
|---|---|---|---|
| 이상적 질량–스프링 | 위치 $q$, 속도 $\dot q$ | 내부 변형의 상세 모드, 공기·지지대의 운동 등을 이상화 | 관성 $m\ddot q$, 복원력 $-kq$ |
| 질량–스프링–댐퍼 | $q,\dot q$ | 주변 유체 분자, 내부 진동 등 | 근사에 따라 마찰 $-c\dot q$, 메모리, 요동 |
| 이상적 LC | 전하 $Q$, 전류 $\dot Q$ | 전자기장의 상세 공간분포를 소수 변수로 근사하고 손실을 생략 | 유효 계수 $L,C$, 전기·자기 에너지 교환 |
| RLC와 열잡음 | $Q,\dot Q$ | 저항체의 전하 운반자·격자 등의 미시 운동 | 저항항 $R\dot Q$, 열잡음 전압 |
| 액체 속 브라운 입자 | 입자의 위치·속도 | 주변 액체 분자들의 위치·속도 | 평균 힘, 마찰·메모리, 불규칙한 힘 |
| 장의 스케일 축약 | 긴 파장의 장·거시 변수 | 짧은 파장의 요동 | 바뀐 유효 계수와 상호작용 |

마찰과 저항은 측정에 맞추어 현상론적으로 지정할 수도 있다. 미시적 환경에서 유도할 때는 제거할 변수와 시간척도에 따라 순간 마찰, 메모리, 요동 등을 얻는다.

외부 구동은 외력·입력·source로, 환경의 지연된 반응은 메모리로, 미해상 자유도의 영향은 요동으로 표현할 수 있다. 여러 스케일의 비선형 결합은 유효 계수와 폐쇄 관계에 반영된다. 이 효과들은 한 모델 안에서 함께 나타날 수 있다.

#### ② 전체 상태에서 일부 자유도를 제거하면 무엇이 남는가

1.4절의 대상 선택을 전체 상태

$$
z=(x,y),\qquad
\dot x=f(x,y),\qquad
\dot y=g(x,y)
$$

로 구체화하자. $x$는 남길 변수들의 묶음이고, $y$는 직접 추적하지 않을 환경·내부 변수들의 묶음이다. 질량–스프링에서는 $x=(q,p)$를 남기고 주변 분자나 내부 진동을 $y$에 포함할 수 있다.

닫힌 전체계가 자율 Hamiltonian 운동을 따르면 전체 에너지를 보존하며, 흐름이 존재하는 범위에서 가역적인 운동을 한다. 현재의 $(x,y)$에는 다음 운동을 결정할 정보가 담긴다.

그런데 같은 $x$에서도 환경 상태 $y$에 따라 힘이 달라질 수 있다. 또한 현재의 $y$에는 과거에 $x$와 상호작용한 영향이 남아 있다. $y$를 제거한 뒤 그 영향을 표현하려면 $x$의 과거 경로와 환경의 초기상태 $y_0$에 관한 정보가 필요할 수 있다.

$$
\boxed{
\text{전체 상태 }z=(x,y)
\longrightarrow
\text{남길 변수 }x
\longrightarrow
\text{유효 힘·메모리·요동을 포함한 운동}
}
$$

대표적인 일반화된 Langevin 형태는

$$
m\ddot q(t)
=
-\nabla U_{\rm eff}(q(t))
-\int_0^tK(t-s)\dot q(s)\,ds
+\eta(t)+f_{\rm ext}(t).
$$

여기서 $q$는 남긴 입자의 위치이고, 전체 축약 상태 $x$에는 속도나 운동량도 포함된다. 1차원에서는 $\nabla U_{\rm eff}$를 $dU_{\rm eff}/dq$로 읽으면 된다.

| 항 | 수학적 역할 | 쉬운 해석 |
|---|---|---|
| $-\nabla U_{\rm eff}$ | 유효 퍼텐셜에서 얻는 힘 | 환경의 평균적 영향까지 반영한 힘 |
| $-\int_0^tK(t-s)\dot q(s)\,ds$ | 메모리 마찰 | 과거 운동에 대한 환경의 반응이 현재에 돌아오는 효과 |
| $K(t-s)$ | 메모리 커널 | 얼마나 오래전의 운동을 얼마나 강하게 기억하는지 나타내는 가중치 |
| $\eta(t)$ | 요동력 | 추적하지 않는 환경의 세부 상태에서 오는 불규칙한 힘 |
| $f_{\rm ext}(t)$ | 외부 구동 | 밖에서 가하는 힘 |

적분은 과거의 각 순간 $s$에서 온 영향을 가중해 모두 더한 것이다. $\eta$는 제거한 자유도의 초기상태와 진화에 의존하고, 그 초기상태를 확률적으로 기술하면 확률적 힘으로 다룬다.

위 식은 속도 이력에 선형으로 작용하는 메모리를 사용한 대표 형태다. 일반적인 축약에서는 메모리가 상태와 과거 경로에 더 복잡하게 의존할 수 있다. 이 유효항들을 체계적으로 유도하는 출발점이 Mori–Zwanzig 투영과 일반화된 Langevin 방정식이다. [Zwanzig의 유도](https://courses.physics.ucsd.edu/2020/Fall/physics210b/Zwanzig1973_NonlinearGeneralizedLangevinEq.pdf)

환경의 기억이 지속되는 동안 입자의 속도가 거의 일정하다면 $\dot q(s)\approx\dot q(t)$로 놓을 수 있다. 커널이 빠르게 감쇠하고 적분 가능하며 그 초기 과도구간을 지난 경우,

$$
\int_0^tK(t-s)\dot q(s)\,ds
\approx
\left(\int_0^\infty K(\tau)\,d\tau\right)\dot q(t)
=\gamma\dot q(t).
$$

$\gamma$는 환경의 짧은 기억을 한 계수로 모은 것이다. 이 근사에서 익숙한 순간 마찰 $-\gamma\dot q(t)$가 나온다. 메모리 마찰과 단순 감쇠항은 이렇게 연결된다.

열평형 환경에서는 적절한 조건 아래 마찰의 응답과 열적 요동의 상관관계가 요동–소산 관계로 연결된다. 저항과 Johnson–Nyquist 열잡음이 구체적인 예다. 따라서 감쇠와 잡음의 크기는 환경의 온도와 응답을 함께 반영한다. [MIT 열잡음 자료](https://ocw.mit.edu/courses/8-13-14-experimental-physics-i-ii-junior-lab-fall-2016-spring-2017/pages/experiments/johnson-noise-and-shot-noise/)

공간 스케일을 줄여 기술할 때는 짧은 파장의 요동을 제거하고 그 영향을 남은 계수·상호작용에 반영한다. 이 변화와 스케일 재조정을 추적하는 방법이 RG이며, 5.6절의 모드·스케일 축약에 연결된다. [RG와 짧은 파장 모드의 제거](https://www.damtp.cam.ac.uk/user/tong/sft/sfthtml/S3.html)

#### ③ 유효 동역학의 장기 거동: 안정성·끌개·흡인영역

소산 운동에서는 **시간이 흐른 뒤 어떤 집합에 접근하며, 어떤 초기조건들이 같은 장기 거동으로 이어지는가**를 묻는다. 3절의 계량·이동도 기반 하강 흐름은 이러한 운동을 구성하는 한 방식이다. 장기 거동의 분석에는 Lyapunov 함수, 불변집합, 끌개, 흡인영역을 사용한다.

##### Lyapunov 함수와 접근하는 불변집합

상태방정식 $\dot x=X(x)$에서 함수 $W$가

$$
\frac{d}{dt}W(x_t)=dW_{x_t}[X(x_t)]\leq0
$$

을 만족하면 감소하는 양을 통해 운동의 범위를 제한할 수 있다. 평형점 근처에서 양의 정부호인 $W$와 그 시간미분의 조건을 이용하면 안정성이나 점근안정성을 판정한다.

예를 들어 양의 불변인 콤팩트 집합 안에서 LaSalle 불변성 원리의 조건이 성립하면, 궤적은

$$
\{x:dW_x[X(x)]=0\}
$$

안의 가장 큰 불변집합에 접근한다. 이로써 함수의 감소를 장기 운동이 놓이는 집합에 연결한다.

##### 끌개와 흡인영역

끌개(attractor) $\mathcal A$는 주변 궤적들을 끌어들이는 불변집합이다. 그 흡인영역(basin of attraction)은

$$
\mathcal B(\mathcal A)
=\{x_0:\operatorname{dist}(\Phi_t(x_0),\mathcal A)\to0
\text{ as }t\to\infty\}
$$

으로 표현할 수 있다. 여기서는 모든 양의 시간에 존재하는 궤적을 대상으로 한다.

끌개는 안정한 평형점, 주기궤도, 더 복잡한 불변집합 등으로 나타날 수 있다. 여러 끌개가 공존하면 흡인영역은 초기조건에 따른 장기 거동을 나누며, 그 경계는 어떤 변화가 다른 거동으로 이어지는지를 보여준다.


외력이 없는 질량–스프링–댐퍼에서 $m,k,c>0$이면

$$
W(q,\dot q)=\frac12m\dot q^2+\frac12kq^2,
\qquad
\dot W=-c\dot q^2\leq0.
$$

이 $W$는 저장된 역학적 에너지이며, 운동을 따라 낮아지는 높이처럼 생각할 수 있다. $\dot W=0$인 순간에는 $\dot q=0$이지만, $q\neq0$이면 스프링이 다시 움직이게 한다. 그 집합 안에 계속 머무를 수 있는 상태는 $(q,\dot q)=(0,0)$이고, 운동은 이 평형점으로 접근한다.

주기적인 외력을 받는 감쇠 스프링은 과도 운동이 줄어든 뒤에도 외력에 맞춰 진동할 수 있다. 외부에서 공급한 에너지가 소산을 보충하기 때문이다. 이때 구동의 위상까지 상태에 포함하면 장기 주기운동을 불변궤도로 다룰 수 있다. 따라서 장기 거동을 판단할 때는 감쇠와 함께 입력도 살핀다.

##### 장기 거동에서 축약으로

$$
\text{감소량·안정성}
\longrightarrow
\text{장기 불변집합과 끌개}
\longrightarrow
\text{흡인영역}
\longrightarrow
\text{장기 거동에 필요한 변수 선택}.
$$

빠르게 감쇠하는 방향과 오래 남는 운동을 분리할 수 있으면 느린 변수나 선택한 모드로 유효 동역학을 구성한다. 유한차원 축약을 얻으려면 끌개의 구조, 시간척도 분리, 남긴 변수의 닫힘 등을 함께 살핀다. 복잡한 끌개에서는 통계적 관측량이나 분포의 축약이 유용할 수 있다.

관측량·분포·반군 표현은 이 장기 거동에도 적용된다. 따라서 상태 층위의 끌개 분석을 관측량의 수렴, 분포의 정상상태, 생성자의 감쇠 모드와 연결할 수 있다.

#### ④ 다루는 범위와 심화의 출발점

여기서는 보존적 모델과 구체적인 계의 관계, 자유도 제거가 남기는 유효 힘·메모리·요동의 의미, 짧은 기억 근사와 순간 마찰의 연결, 그리고 안정성·끌개·흡인영역을 통한 장기 거동까지 다룬다. 미시적 유도와 정리의 증명은 다음 주제에서 이어진다.

| 더 알고 싶은 질문 | 심화의 출발점 |
|---|---|
| 제거한 변수에서 메모리와 요동을 어떻게 유도하는가 | Mori–Zwanzig 투영, 일반화된 Langevin 방정식 |
| 마찰과 열잡음의 크기는 어떻게 연결되는가 | 요동–소산 정리, Johnson–Nyquist 잡음 |
| 어느 조건에서 기억을 순간 반응으로 근사할 수 있는가 | 시간척도 분리, Markov 근사 |
| 관측 스케일에 따라 계수와 상호작용이 왜 달라지는가 | Coarse graining, RG |
| 어디로 접근하며 초기조건에 따라 무엇이 달라지는가 | Lyapunov·LaSalle 이론, attractor·basin |
| 장기 거동을 어떤 적은 변수로 기술할 수 있는가 | 불변·느린 다양체, 모드 축약, 폐쇄 |

### 5.3 관측량 층위의 축약

관측량 함수공간에서

$$
\mathcal V_k
=\operatorname{span}\{\phi_1,\ldots,\phi_k\}
\subseteq\mathcal F(M)
$$

를 남긴다. 이 부분공간이 생성자 아래 불변이면

$$
\mathcal L\phi_i=\sum_jB_{ij}\phi_j
$$

로 닫힌 관측량 진화를 얻는다.

Koopman 모드 절단이나 유한 기저 근사는 어떤 관측량 성분을 유지할지 선택한다. 선택한 공간 밖으로 나가는 성분이 있으면 투영 근사가 들어간다. 남긴 관측량에서 원래 상태를 재구성할 수 있는지는 별도의 정보 조건에 달려 있다.

### 5.4 분포 층위의 축약

분포 전체 대신 모멘트

$$
m_i(t)=\int\phi_i(x)\,d\mu_t(x)
$$

를 남기면

$$
\dot m_i(t)=\int\mathcal L\phi_i(x)\,d\mu_t(x).
$$

오른쪽이 선택한 모멘트만으로 표현되면 닫힌 식을 얻는다. 고차 모멘트가 필요하면 그 효과를 연결하는 moment closure가 추가된다.

또는

$$
\mu_t\approx\mu_{\theta(t)},\qquad
\{\mu_\theta:\theta\in\Theta\}
$$

라는 유한차원 분포족으로 제한한다. 분포 진화를 그 족의 접공간으로 어떻게 투영할지 정할 때 Fisher 또는 Wasserstein 구조 등을 사용할 수 있다.

이때 정보기하·수송기하는 이미 주어진 분포 동역학을 축약하는 기준으로도 작용한다. 3절에서 기하와 에너지로 운동을 구성하는 역할과 연결되지만, 두 구성이 일치하는지는 추가 조건에 달려 있다.

### 5.5 HJ/HJB 층위의 축약

작용·가치함수 전체 대신

$$
S(t,q)\approx\sum_{j=1}^ka_j(t)\phi_j(q),
\qquad
V(t,x)\approx\sum_{j=1}^kb_j(t)\psi_j(x)
$$

같은 기저 근사나 reduced ansatz를 사용한다. 이를 HJ/HJB에 대입하고 투영하면 계수의 진화식이나 근사 문제가 된다.

남기는 것은 함수공간의 표현 자유도다. 상태공간의 차원을 줄이는 것과 별개의 선택이며, 함수 근사의 오차는 복원되는 궤적이나 선택되는 제어입력에도 영향을 준다.

### 5.6 변환·모드 표현에서 각 층위의 성분을 줄이기

4절의 스펙트럼·대수적 분해는 어떤 성분들이 있는지를 드러낸다. 일부 성분을 유지할 때 축약이 시작된다.

| 표현 | 유지하는 정보 | 적용되는 층위 |
|---|---|---|
| 고유모드·일반화 고유모드 | 선택한 불변 성분 | 선형 상태, 선형화된 상태 |
| Koopman 스펙트럼 | 선택한 관측량 모드 | 관측량 |
| 분포 생성자의 스펙트럼 | 선택한 분포 변화 성분 | 분포 |
| Fourier·공간 기저 | 선택한 주파수·기저 계수 | 장, 분포 밀도, HJ/HJB 함수 |
| 모듈의 국소 성분 | 선택한 일반화 고유값 성분 | 유한차원 선형연산자가 작용하는 객체 |

완전한 분해와 유한차원 근사는 구별된다. 비선형 동역학에서는 남긴 성분과 버린 성분이 결합하므로 폐쇄나 유효항이 필요할 수 있다.

함수의 스케일별 성분은 적절한 함수공간에서 형식적으로

$$
u=\sum_{j\in\mathbb Z}\Delta_j u,\qquad |\xi|\sim2^j
$$

라는 Littlewood–Paley 분해로 분석할 수 있다. 관심 대역을 남기고 제거한 성분의 영향을 처리하는 일은 해당 함수 층위의 축약이다.

$$
u=u_{\rm coarse}+u_{\rm fine}
\quad\longrightarrow\quad
\partial_tu_{\rm coarse}
=\mathcal L_{\rm eff}u_{\rm coarse}
+\text{유효 보정항}.
$$

Coarse graining이나 RG에서는 제거한 성분의 효과를 남은 매개변수와 상호작용에 반영한다. RG의 스케일 변화는 물리적 시간진화와 구별되며, 유효 모형이 스케일에 따라 어떻게 달라지는지를 기술한다.

상태·관측량·분포·작용·가치함수 중 어떤 객체를 선택하든, 그 층위에서 남길 정보를 정하고 남은 객체의 진화가 닫히는지를 묻는다.
