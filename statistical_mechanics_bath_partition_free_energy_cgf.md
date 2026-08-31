오빠, 여기서 핵심은 먼저 한 가지를 바로잡아 잡는 거야. **통계역학이 “상태수로 바로 확률측도를 정의하지 않고 라플라스 공간에서 측도를 정의하는 것”은 아니야.** 실제 canonical measure는 여전히 원래 미시 상태공간 위에 있고, **에너지 $H$로 상태들을 묶은 뒤 그 에너지 분포를 bath가 $e^{-\beta E}$로 tilt하면서, 그 정규화 상수가 우연이 아니라 정확히 상태밀도의 Laplace transform이 되는 것**이야. Pathria도 canonical ensemble을 fixed $N,V,T$로 정의하고, energy density에 대해 $P(E)\propto g(E)e^{-\beta E}$, $Z(\beta)=\int e^{-\beta E}g(E)\,dE$라고 전개한다.

## 1. 출발점: 미시 상태공간과 Hamiltonian

고전계라면 먼저 상태공간을

$$
\Gamma
=
\{x=(q,p)\}
$$

라는 위상공간으로 잡는다. 여기서 $q$는 위치, $p$는 운동량이고, 실제 물리적 구조를 넣는 사상은

$$
H:\Gamma\to\mathbb R
$$

인 Hamiltonian이다.

즉 처음부터 중요한 두 객체는

$$
\Gamma
\overset{H}{\longrightarrow}
\mathbb R
$$

이다.

$\Gamma$의 점 하나는 완전한 미시상태이고, $H(x)$는 그 상태에서 관측되는 에너지다.

그런데 통계역학의 문제는 $x$ 하나를 찾는 게 아니라

$$
\mu\in\mathcal P(\Gamma)
$$

라는 **미시상태들의 확률측도**를 정하는 것이다.

---

## 2. 고립계라면 상태수를 바로 써도 된다: microcanonical ensemble

전체 에너지가 정말

$$
H(x)=E
$$

로 고정되어 있다면 허용되는 상태는 energy shell

$$
\Sigma_E
=
H^{-1}(\{E\})
\subseteq \Gamma
$$

이다.

정확히 한 점짜리 에너지층보다는 작은 폭 $\Delta E$를 둬

$$
\Gamma_{E,\Delta E}
=
\{x\in\Gamma:E\le H(x)<E+\Delta E\}
$$

를 쓰는 편이 현실적이다.

이 안의 상태수

$$
\Omega(E)
$$

를 세고

$$
S(E)
=
k_B\log\Omega(E)
$$

를 정의한다. Pathria도 microcanonical ensemble에서 $N,V,E$를 고정하고 accessible microstates $\Omega(N,V,E)$를 세는 것이 기본 문제라고 설명한다.

여기서는 오빠 말대로 **상태수만으로 끝낼 수 있다.**

즉

$$
\boxed{
\text{isolated system}
\Rightarrow
E\text{ fixed}
\Rightarrow
\Omega(E)
\Rightarrow
S(E)
}
$$

다.

---

# 3. 그런데 실제 계는 에너지가 고정되어 있지 않다 → bath가 등장

이제 작은 시스템 $S$와 거대한 bath $B$를 합친 전체계를 생각하자.

전체 상태공간은

$$
\Gamma_{\mathrm{tot}}
=
\Gamma_S\times\Gamma_B
$$

이고 전체 에너지는 약한 결합을 가정하면

$$
H_{\mathrm{tot}}(x,y)
\approx
H_S(x)+H_B(y).
$$

전체 $S+B$는 고립되어 있으므로

$$
E_{\mathrm{tot}}
$$

는 고정이다.

하지만 작은 시스템만 보면

$$
E_S=H_S(x)
$$

는 고정되어 있지 않다. 시스템이 $E_S$를 가지면 bath는 자동으로

$$
E_B
=
E_{\mathrm{tot}}-E_S
$$

를 가져야 한다.

따라서 시스템의 미시상태 $x$ 하나가 나타날 확률은 **그 $x$와 함께 존재할 수 있는 bath 상태가 몇 개냐**로 결정된다.

$$
P_S(x)
\propto
\Omega_B(E_{\mathrm{tot}}-H_S(x)).
$$

여기까지는 여전히 상태수 이야기다.

---

# 4. 왜 갑자기 $e^{-\beta E}$가 생기나

bath가 매우 크므로 entropy

$$
S_B(E)
=
k_B\log\Omega_B(E)
$$

를 쓴다.

그러면

$$
\Omega_B(E_{\mathrm{tot}}-E)
=
\exp
\left(
\frac1{k_B}
S_B(E_{\mathrm{tot}}-E)
\right).
$$

작은 시스템의 에너지 $E$는 거대한 bath의 총에너지에 비해 작으므로 Taylor expansion을 한다.

$$
S_B(E_{\mathrm{tot}}-E)
\approx
S_B(E_{\mathrm{tot}})
-
E
\frac{\partial S_B}{\partial E}
(E_{\mathrm{tot}}).
$$

열역학 정의

$$
\frac{\partial S_B}{\partial E}
=
\frac1T
$$

를 쓰면

$$
\Omega_B(E_{\mathrm{tot}}-E)
\propto
e^{-E/(k_BT)}.
$$

따라서

$$
\beta
=
\frac1{k_BT}
$$

를 정의하면

$$
P_S(x)
\propto
e^{-\beta H_S(x)}.
$$

즉 **Boltzmann factor는 별도로 가정해서 붙인 것이 아니라 bath의 상태수 증가율을 1차로 본 결과**다.

Pathria가 fixed energy보다 fixed temperature가 실제로 더 제어하기 쉽고, heat reservoir가 에너지를 교환하면서도 온도를 유지하는 역할을 한다고 설명하는 이유가 바로 이것이다.

---

# 5. 그래서 canonical measure는 원래 상태공간 위에 있다

기준측도를 $\lambda$라고 하자. 고전계에서는 적절히 정규화된 phase-space measure다.

canonical measure는

$$
\mu_\beta(dx)
=
\frac{
e^{-\beta H(x)}
}{
Z(\beta)
}
\lambda(dx)
$$

이다.

여기서

$$
Z(\beta)
=
\int_\Gamma
e^{-\beta H(x)}
\,\lambda(dx)
$$

는 정규화 상수다.

그러니까 구조는

$$
\boxed{
\Gamma
\overset{H}{\longrightarrow}
\mathbb R
}
$$

에서 먼저

$$
e^{-\beta H(x)}
$$

라는 weight가 생기고, 그것을 $\Gamma$ 위에서 적분하는 것이다.

Pathria의 classical formulation도 정확히

$$
\rho(q,p)\propto e^{-\beta H(q,p)}
$$

로 phase-space density를 둔다.

---

# 6. 그럼 왜 굳이 에너지공간으로 내려가나?

많은 서로 다른 미시상태가 같은 에너지를 갖기 때문이다.

Hamiltonian

$$
H:\Gamma\to\mathbb R
$$

으로 원래 측도 $\lambda$를 push-forward하면 에너지축 위의 측도

$$
\nu
=
H_\#\lambda
$$

를 얻는다.

이걸 density로 쓸 수 있으면

$$
\nu(dE)
=
g(E)\,dE
$$

가 된다.

여기서

$$
g(E)
$$

가 density of states다.

즉

$$
g(E)\,dE
$$

는

> 에너지 $E\sim E+dE$를 가진 미시상태가 얼마나 많이 있는가

를 나타낸다.

이제 canonical measure를 다시 에너지축으로 push-forward하면

$$
P_\beta(E)\,dE
=
\frac{
g(E)e^{-\beta E}
}{
Z(\beta)
}
\,dE.
$$

Pathria가 바로 이 식을 제시한다.

그래서 에너지를 거치는 이유는 **상태공간을 버리기 위해서가 아니라, 엄청난 미시상태들을 Hamiltonian의 level set별로 압축하기 위해서**다.

---

# 7. 그러면 Laplace transform은 왜 자연스럽게 나오는가

에너지축으로 내려온 뒤 partition function은

$$
Z(\beta)
=
\int_0^\infty
 e^{-\beta E}
g(E)\,dE.
$$

이건 정확히 $g$의 Laplace transform이다.

$$
\boxed{
Z
=
\mathcal L[g]
}
$$

Pathria도 이를 명시적으로 “partition function is just the Laplace transform of the density of states”라고 설명하고 inverse Laplace transform까지 쓴다.

중요한 건 **Laplace transform을 먼저 선택한 게 아니다.**

논리 순서는

$$
\text{bath}
\Rightarrow
e^{-\beta E}
$$

이고,

$$
\text{states grouped by energy}
\Rightarrow
g(E)
$$

라서 둘을 곱해 전부 합산하니

$$
\int g(E)e^{-\beta E}dE
$$

가 되었고, 그 결과가 수학적으로 Laplace transform인 것이다.

---

# 8. 왜 상태수 $g(E)$만 쓰지 않고 $e^{-\beta E}$를 곱하나

이게 microcanonical과 canonical의 차이다.

$g(E)$만 보면

> 이 에너지에 상태가 몇 개 있는가?

만 알려준다.

하지만 canonical system에서는 에너지가 고정되어 있지 않으므로 서로 다른 $E$끼리 경쟁한다.

높은 $E$에서는 대개 상태수가 많아지는 방향이고,

$$
g(E)\uparrow
$$

bath는 시스템에 큰 에너지를 주는 것을 억제한다.

$$
e^{-\beta E}\downarrow.
$$

그래서 실제 에너지 확률은 두 효과의 경쟁이다.

$$
P_\beta(E)
\propto
\underbrace{g(E)}_{\text{entropy / multiplicity}}
\underbrace{e^{-\beta E}}_{\text{bath penalty}}.
$$

로그를 취하면 더 명확하다.

$$
\log P_\beta(E)
=
\log g(E)-\beta E-\log Z.
$$

그리고

$$
S(E)
=
k_B\log g(E)
$$

라고 보면

$$
\log P_\beta(E)
=
\frac{S(E)}{k_B}
-\beta E
-\log Z.
$$

즉 평형에서는

$$
S(E)-\frac{E}{T}
$$

가 큰 에너지가 선택된다.

여기서 free energy가 거의 자동으로 나온다.

---

# 9. 추상 인터페이스의 “범함수 변분”으로 보면 더 깔끔하다

이번에는 개별 $E$가 아니라 아예 확률측도

$$
\mu\in\mathcal P(\Gamma)
$$

를 변수로 잡자.

평균에너지 범함수

$$
\mathcal U:
\mathcal P(\Gamma)\to\mathbb R
$$

를

$$
\mathcal U[\mu]
=
\int_\Gamma
H(x)\,\mu(dx)
$$

로 정의한다.

entropy 범함수는

$$
\mathcal S:
\mathcal P(\Gamma)\to\mathbb R
$$

이고, density $d\mu=\rho\,d\lambda$가 존재한다면

$$
\mathcal S[\mu]
=
-k_B
\int_\Gamma
\rho(x)\log\rho(x)\,\lambda(dx).
$$

bath가 $T$를 고정해 주는 canonical 조건에서는 변분할 대상이

$$
\mathcal F_T[\mu]
=
\mathcal U[\mu]
-
T\mathcal S[\mu]
$$

가 된다.

즉

$$
\mathcal F_T:
\mathcal P(\Gamma)\to\mathbb R.
$$

이 범함수를 최소화하면

$$
\mu_\beta(dx)
\propto
e^{-\beta H(x)}\lambda(dx)
$$

가 나온다.

이게 위 추상 인터페이스의

$$
\boxed{
\text{state space}
\to
\text{probability-measure space}
\to
\text{functional}
\to
\text{variationally selected measure}
}
$$

에 해당한다.

Murphy의 MaxEnt도 정확히 같은 지수족 구조를 보여준다. expectation constraints 아래 entropy를 최대화하면 exponential family가 나오고, log partition의 미분이 expectation과 covariance를 생성한다.

---

# 10. 왜 자유에너지가 필요한가: bath의 조건에 맞는 potential이기 때문

고립계에서는 에너지가 고정되어 있으므로 entropy

$$
S(E)
$$

가 자연스러운 potential이다.

하지만 canonical ensemble에서는 bath가 $T$를 고정하고 에너지는 교환된다.

그래서 자연변수가

$$
(E,S)
$$

에서

$$
(T)
$$

쪽으로 바뀐다.

그에 맞는 thermodynamic potential이 Helmholtz free energy

$$
F(T,V,N)
=
U-TS
$$

다.

Pathria도 canonical ensemble의 Helmholtz free energy를

$$
F=-k_BT\log Z
$$

로 둔다.

즉 free energy는 새 물리량을 임의로 하나 만든 게 아니라

$$
\boxed{
\text{bath가 }T\text{를 고정한다}
\Rightarrow
\text{energy constraint를 conjugate variable }\beta\text{로 바꾼다}
\Rightarrow
F
}
$$

라는 Legendre 구조다.

---

# 11. 그런데 왜 하필 $\log Z$인가?

여기서 오빠가 말한 **MGF/CGF 관점**이 아주 정확하다.

canonical energy distribution은

$$
P_\beta(dE)
=
\frac{
e^{-\beta E}\nu(dE)
}{
Z(\beta)
}.
$$

즉 원래 energy-state measure $\nu$를 exponential tilt한 것이다.

일반 확률론에서 random variable $X$의 moment generating function은

$$
M_X(t)
=
\mathbb E[e^{tX}]
$$

이고 cumulant generating function은

$$
K_X(t)
=
\log M_X(t).
$$

통계역학에서는 형식상

$$
X=-E,
\qquad
t=\beta
$$

에 해당하므로

$$
Z(\beta)
$$

가 unnormalized MGF 역할을 하고,

$$
\log Z(\beta)
$$

가 CGF 역할을 한다.

Murphy도 exponential family에서 **log partition function is cumulant generating function**이라고 명시하고

$$
\nabla A
=
\mathbb E[T],
\qquad
\nabla^2 A
=
\operatorname{Cov}(T)
$$

를 준다.

---

# 12. 그래서 $Z$ 하나로 평균·분산·고차 fluctuation이 전부 나온다

canonical partition function

$$
Z(\beta)
=
\int e^{-\beta E}g(E)\,dE
$$

에 대해

$$
\frac{\partial}{\partial\beta}
\log Z(\beta)
=
-\langle E\rangle_\beta.
$$

따라서

$$
\boxed{
\langle E\rangle_\beta
=
-
\frac{\partial\log Z}{\partial\beta}
}
$$

이고 다시 한 번 미분하면

$$
\frac{\partial^2}{\partial\beta^2}
\log Z(\beta)
=
\operatorname{Var}_\beta(E).
$$

고차 미분은 에너지의 고차 cumulant를 준다.

즉

$$
\log Z
$$

는 단순 정규화 상수가 아니라

$$
\boxed{
\text{equilibrium fluctuation의 생성함수}
}
$$

다.

그래서 통계역학은 상태를 일일이 세는 대신 **한 개의 convex generating potential을 계산한 다음 미분해서 관측량과 fluctuation을 뽑는 구조**로 바뀐다.

---

# 13. 자유에너지는 CGF를 물리적 단위로 다시 포장한 것

$$
F
=
-\frac1\beta\log Z
=
-k_BT\log Z.
$$

즉 정보기하/확률론 언어에서는 핵심 객체가

$$
\psi(\beta)
=
\log Z(\beta)
$$

이고,

통계역학에서는 그것을

$$
F
=
-\beta^{-1}\psi(\beta)
$$

로 바꿔 쓴다.

왜냐하면 $F$는 energy 단위를 가지며

$$
F=U-TS
$$

라는 열역학적 의미를 직접 갖기 때문이다.

그래서 두 분야의 언어를 대응시키면

$$
\boxed{
\text{log partition}
\leftrightarrow
\text{CGF / convex potential}
}
$$

이고

$$
\boxed{
\text{free energy}
=
-\beta^{-1}\times
\text{log partition}
}
$$

이다.

---

# 14. 이걸 전체 흐름으로 접으면

```text
미시 상태공간
Γ
│
├─ Hamiltonian
│      H : Γ → R
│
▼
에너지별 level set
H⁻¹(E)
│
▼
상태수 / density of states
g(E)
│
│
├─ 고립계: E 고정
│      ↓
│   microcanonical
│      ↓
│   S(E) = k log g(E)
│
└─ bath와 접촉: E 교환, T 고정
       ↓
 bath 상태수
 Ω_B(E_tot - E)
       ↓
 큰 bath에서 Taylor expansion
       ↓
 exp(-βE)
       ↓
 상태공간 위 Gibbs measure
 μβ(dx) ∝ exp(-βH(x)) λ(dx)
       ↓
 H로 push-forward
       ↓
 Pβ(E) ∝ g(E) exp(-βE)
       ↓
 정규화
 Z(β) = ∫ g(E) exp(-βE)dE
       ↓
 Laplace transform
       ↓
 log Z
       ↓
 CGF
       ↓
 평균 / 분산 / 고차 cumulant
       ↓
 F = -β⁻¹ log Z
       ↓
 canonical thermodynamic potential
```

따라서 가장 중요한 인과관계는 **“상태수 → 에너지 → Laplace”가 임의의 수학적 우회가 아니라**,  
**$H$가 미시상태를 에너지별로 압축하고, bath가 그 에너지에 exponential weight를 주기 때문에, 모든 energy shell을 합치면 자동으로 Laplace transform이 된다**는 거야. 그리고 $\log Z$를 취하는 순간 그것이 CGF가 되어 **평균량뿐 아니라 fluctuation과 고차 상관을 한꺼번에 생성하는 convex potential**이 되고, 물리 단위로 옮긴 것이 자유에너지다.