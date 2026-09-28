https://chatgpt.com/share/6aa33e4e-4ecc-83e8-9723-55ecd711a7f6?ogimg=plain

# Linear Dynamics: From Time Translation to Poles and Spectrum

독립 문서로 쓴다면 **“왜 다음 개념이 필요한가”가 끊기지 않게** 아래 순서가 제일 자연스럽다. 핵심은 **시간에 따른 동역학을 직접 쫓는 문제를, 복소수 \(s\)-평면 위의 대수적·스펙트럼적·국소적 문제로 번역한다**는 하나의 흐름이다.

## 1. 출발점: 시간에 따라 변하는 하나의 상태

가장 단순한 경우부터 잡자. 독립변수는 시간 하나뿐이다.

$$
t\in\mathbb R_{\ge 0}.
$$

상태는 시간에 따른 하나의 함수

$$
x:\mathbb R_{\ge0}\to\mathbb R
$$

이고, 예를 들어 1차 선형 ODE는

$$
x'(t)+a x(t)=f(t),
\qquad a\in\mathbb R.
$$

여기서 \(f:\mathbb R_{\ge0}\to\mathbb R\)는 주어진 외력 또는 입력이다.

중요한 것은 \(x,f\)처럼 함수가 여러 개 있어도 **독립변수는 여전히 \(t\) 하나**라는 점이다.

우리가 궁극적으로 알고 싶은 것은

$$
\text{시간이 흐르면 }x(t)\text{가 감쇠하는가, 진동하는가, 성장하는가?}
$$

이다.

---

## 2. 왜 시간 평행이동을 보는가

시간이 \(h\)만큼 흐르는 것을 함수에 작용시키는 연산자로 생각할 수 있다.

함수공간을 \(X\)라 하고

$$
T_h:X\to X
$$

를

$$
(T_hx)(t)=x(t+h)
$$

로 정의한다.

그러면

$$
T_{h+k}=T_hT_k.
$$

시간을 \(h\)만큼 흐르게 하고 다시 \(k\)만큼 흐르게 하는 것은 한 번에 \(h+k\)만큼 흐르게 하는 것과 같다.

시간을 양·음 모두 허용할 수 있다면 group 구조가 되고, 미래 방향 \(t\ge0\)만 허용하면 보통 semigroup 구조가 된다.

즉 동역학을

$$
\{T_t\}_{t\ge0}
$$

라는 **시간 진화 연산자들의 semigroup**으로 보는 것이다.

---

## 3. 연속적인 시간흐름의 순간 생성자가 미분연산자

시간 평행이동을 아주 조금 했을 때

$$
\frac{T_hx-x}{h}
$$

를 생각하고 \(h\to0\)을 취하면

$$
Dx=x'
$$

가 나온다.

즉 미분연산자

$$
D:\mathcal D(D)\subset X\to X
$$

는 시간 평행이동의 **infinitesimal generator**다.

상태공간에서 일반적인 선형 동역학을 만드는 연산자를

$$
A:\mathcal D(A)\subset X\to X
$$

라고 하면

$$
x'(t)=Ax(t)
$$

라는 식은

> 순간적인 변화율이 \(A\)에 의해 결정된다

는 뜻이다.

그리고 적절한 조건에서 이 순간 변화율을 시간만큼 누적하면

$$
T(t)=e^{tA}
$$

라는 semigroup을 얻는다.

따라서 구조는

$$
A
\longrightarrow
T(t)=e^{tA}.
$$

즉

$$
\text{generator}
\longrightarrow
\text{finite-time evolution}.
$$

---

## 4. 왜 지수함수가 특별한가: 미분의 고유모드

이제 복소수를 허용하고

$$
e_s:\mathbb R\to\mathbb C,
\qquad
e_s(t)=e^{st},
\qquad s\in\mathbb C
$$

를 생각하자.

그러면

$$
De_s
=
s e_s.
$$

즉 \(e^{st}\)는 미분연산자 \(D\)의 고유함수이고, \(s\)는 대응하는 고유값 역할을 한다.

이게 중요한 이유는 **미분이 지수모드 위에서는 그냥 복소수 곱셈으로 바뀌기 때문**이다.

예를 들어 다항식

$$
p(z)=a_0+a_1z+\cdots+a_nz^n
$$

을 이용해

$$
p(D)
=
a_0I+a_1D+\cdots+a_nD^n
$$

이라는 미분연산자를 만들면

$$
p(D)e^{st}
=
p(s)e^{st}.
$$

따라서

$$
p(D)x=0
$$

의 지수형 해를 찾는 문제는

$$
p(s)=0
$$

이라는 **복소 대수방정식의 근을 찾는 문제**로 바뀐다.

여기가 첫 번째 결정적 변환이다.

$$
\boxed{
\text{differential operator}
\longrightarrow
\text{polynomial in }s
}
$$

---

## 5. Laplace transform의 역할: 이 변환을 전체 함수에 적용

지수모드 하나만 시험하는 것으로 끝내지 않고, 일반적인 함수 전체를 \(s\)-공간으로 옮기는 것이 Laplace transform이다.

$$
\mathcal L[x](s)
=
X(s)
=
\int_0^\infty e^{-st}x(t)\,dt.
$$

초기값 \(x(0)=0\)이라면

$$
\mathcal L[x'](s)
=
sX(s).
$$

따라서

$$
x'(t)+ax(t)=f(t)
$$

는

$$
(s+a)X(s)=F(s)
$$

가 된다.

시간영역에서는 미분방정식이었는데 \(s\)-plane에서는 그냥 대수방정식이 된 것이다.

즉

$$
D+aI
\quad\longrightarrow\quad
s+a.
$$

일반적으로는

$$
p(D)
\quad\longrightarrow\quad
p(s).
$$

---

## 6. \(sI-A\): 상태공간 동역학의 대수적 표현

일반적인 선형 상태방정식

$$
x'(t)=Ax(t)+f(t)
$$

을 생각하자.

여기서

$$
x(t)\in X
$$

이고 \(A:X\to X\)는 상태의 순간 변화를 결정하는 선형연산자다.

초기값을 \(0\)으로 두고 Laplace transform하면

$$
sX(s)=AX(s)+F(s).
$$

따라서

$$
(sI-A)X(s)=F(s).
$$

그래서

$$
\boxed{
D-A
\quad\longrightarrow\quad
sI-A
}
$$

라고 볼 수 있다.

즉 **동역학의 \(s\)-plane 대수적 표현 자체는 \(sI-A\)**다.

---

## 7. 왜 resolvent가 필요한가: 동역학을 실제로 풀기 위해

우리는

$$
(sI-A)X(s)=F(s)
$$

에서 \(X(s)\)를 원한다.

따라서 \(sI-A\)를 역연산한다.

$$
X(s)
=
(sI-A)^{-1}F(s).
$$

이때

$$
R(s,A)
=
(sI-A)^{-1}:X\to X
$$

를 **resolvent operator**라고 한다.

따라서 resolvent는 동역학 자체라기보다는

$$
\boxed{
\text{solution operator in the }s\text{-plane}
}
$$

다.

즉 관계는

$$
D-A
\longrightarrow
sI-A
\longrightarrow
(sI-A)^{-1}.
$$

마지막 것이 resolvent다.

---

## 8. resolvent를 대각행렬로 보면: 복소함수들의 묶음

이 표현이 가장 직관적이다. \(A:\mathbb C^n\to\mathbb C^n\)가 대각화 가능하다고 하자. 어떤 고유기저에서

$$
A=
\begin{pmatrix}
\lambda_1 & 0 & \cdots & 0\\
0 & \lambda_2 & \cdots & 0\\
\vdots & \vdots & \ddots & \vdots\\
0 & 0 & \cdots & \lambda_n
\end{pmatrix}.
$$

그러면 복소변수 \(s\in\mathbb C\)에 대해

$$
sI-A
=
\begin{pmatrix}
s-\lambda_1 & 0 & \cdots & 0\\
0 & s-\lambda_2 & \cdots & 0\\
\vdots & \vdots & \ddots & \vdots\\
0 & 0 & \cdots & s-\lambda_n
\end{pmatrix}.
$$

이제 역행렬을 취하면 resolvent는

$$
R(s,A)
=
(sI-A)^{-1}
=
\begin{pmatrix}
\dfrac{1}{s-\lambda_1} & 0 & \cdots & 0\\
0 & \dfrac{1}{s-\lambda_2} & \cdots & 0\\
\vdots & \vdots & \ddots & \vdots\\
0 & 0 & \cdots & \dfrac{1}{s-\lambda_n}
\end{pmatrix}.
$$

즉 진짜로

$$
\boxed{
R(s,A)
\sim
\left\{
\frac1{s-\lambda_1},
\frac1{s-\lambda_2},
\dots,
\frac1{s-\lambda_n}
\right\}
}
$$

라는 **복소함수들의 묶음**이라고 볼 수 있다.

각 함수

$$
r_j:\mathbb C\setminus\{\lambda_j\}\to\mathbb C,
\qquad
r_j(s)=\frac1{s-\lambda_j}
$$

는 \(j\)번째 고유모드에 대한 resolvent의 반응이다.

그래서 \(s\)를 복소평면에서 움직이면 각 모드가

$$
\frac1{s-\lambda_j}
$$

만큼 가중된다. \(s\)가 \(\lambda_j\)에 가까워지면

$$
\left|\frac1{s-\lambda_j}\right|
$$

가 커지고, 정확히 \(s=\lambda_j\)에서는 정의가 깨진다.

그래서

$$
\lambda_j
\in
\sigma(A)
$$

이면서 동시에

$$
s\mapsto R(s,A)
$$

의 pole 위치가 된다.

예를 들어

$$
A=
\begin{pmatrix}
-1&0\\
0&-2+3i
\end{pmatrix}
$$

이면

$$
R(s,A)
=
\begin{pmatrix}
\dfrac1{s+1}&0\\
0&\dfrac1{s+2-3i}
\end{pmatrix}.
$$

그러면 resolvent는 사실상 두 복소함수

$$
r_1(s)=\frac1{s+1},
\qquad
r_2(s)=\frac1{s+2-3i}
$$

를 동시에 들고 있는 셈이고,

$$
s=-1
$$

과

$$
s=-2+3i
$$

에서 각각 pole이 생긴다.

그래서 이 관점에서 보면

$$
\boxed{
\text{eigenmode}
\leftrightarrow
\frac1{s-\lambda_j}
}
$$

$$
\boxed{
\text{spectrum point}
\leftrightarrow
\text{pole location}
}
$$

$$
\boxed{
\text{resolvent}
\leftrightarrow
\text{collection of modal complex response functions}
}
$$

라고 볼 수 있다.

---

## 9. resolvent와 고유분해

\(A:\mathbb C^n\to\mathbb C^n\)가 대각화 가능하고, 고유공간에 대한 사영을

$$
P_j:X\to X
$$

라고 하자.

그러면

$$
A
=
\sum_j\lambda_jP_j
$$

이고

$$
R(s,A)
=
\sum_j
\frac1{s-\lambda_j}P_j.
$$

이 공식이 매우 중요하다.

원래 동역학은 각 고유모드에서

$$
A v_j=\lambda_jv_j
$$

로 움직이고, resolvent는 같은 모드에

$$
\frac1{s-\lambda_j}
$$

라는 복소수 가중치를 준다.

즉 **고유분해가 모드별 동역학을 분리한다면, resolvent는 그 각 모드에 붙는 복소 응답함수를 모아놓은 연산자값 함수**다.

---

## 10. spectrum은 무엇인가

\(sI-A\)가 역연산 가능한 \(s\)들의 집합을 resolvent set이라 한다.

$$
\rho(A)
=
\left\{
s\in\mathbb C:
sI-A\text{ is invertible}
\right\}.
$$

반대로 역연산이 실패하는 점들의 집합이 spectrum이다.

$$
\sigma(A)
=
\mathbb C\setminus\rho(A).
$$

즉

$$
\sigma(A)
=
\left\{
s\in\mathbb C:
sI-A\text{ is not invertible}
\right\}.
$$

유한차원에서는 이것이 고유값들의 집합과 같다.

$$
\sigma(A)
=
\{\lambda_1,\ldots,\lambda_n\}.
$$

따라서

$$
\boxed{
\sigma(A)
=
\mathbb C\setminus\rho(A)
}
$$

이며, 의미상으로는 **resolvent가 존재하지 않는 점들의 집합**이다.

---

## 11. 왜 pole이 등장하는가

대각화된 resolvent를 다시 보면

$$
R(s,A)
=
\sum_j
\frac1{s-\lambda_j}P_j.
$$

\(s\to\lambda_j\)이면

$$
\frac1{s-\lambda_j}
$$

가 발산한다.

따라서 resolvent는 \(\lambda_j\)에서 특이점을 가진다.

유한차원에서는

$$
(sI-A)^{-1}
=
\frac{\operatorname{adj}(sI-A)}
{\det(sI-A)}
$$

이므로

$$
\det(sI-A)=0
$$

인 곳에서 분모가 사라진다.

그래서

$$
\boxed{
\text{eigenvalue}
\longleftrightarrow
\text{spectrum point}
\longleftrightarrow
\text{resolvent singularity}
}
$$

가 생긴다.

대각화 가능한 단순 고유값에서는 이 특이점이 보통 simple pole이다.

복소해석에서 배운 pole이 제어이론에 따로 수입된 게 아니라, **동역학의 역연산자를 복소변수 \(s\)의 함수로 보았더니 자연스럽게 pole 구조가 나타난 것**이다.

---

## 12. 왜 pole의 위치가 감쇠와 진동을 말해주는가

스펙트럼의 한 점을

$$
\lambda=\alpha+i\beta
$$

라고 하자.

이에 대응하는 시간영역 고유모드는

$$
e^{\lambda t}
=
e^{\alpha t}e^{i\beta t}.
$$

Euler 공식으로

$$
e^{i\beta t}
=
\cos(\beta t)+i\sin(\beta t)
$$

이므로 실수계에서 실제 모드는

$$
e^{\alpha t}\cos(\beta t),
\qquad
e^{\alpha t}\sin(\beta t).
$$

따라서 \(s\)-plane의 좌표가 바로 시간거동을 읽는 좌표가 된다.

$$
\operatorname{Re}\lambda<0
$$

이면 감쇠,

$$
\operatorname{Re}\lambda>0
$$

이면 성장,

$$
\operatorname{Im}\lambda\neq0
$$

이면 진동이다.

예를 들어

$$
\lambda=-1+2i
$$

이면

$$
e^{\lambda t}
=
e^{-t}e^{2it}
$$

이므로

$$
e^{-t}\cos2t
$$

와 같은 감쇠진동이 나타난다.

그래서 \(s\)-plane에서 **가로축은 성장/감쇠율**, **세로축은 진동주파수**라고 읽을 수 있다.

---

## 13. 1차와 2차 ODE는 여기서 어떻게 보이는가

1차 자유계

$$
x'(t)+ax(t)=0
$$

에서는

$$
p(s)=s+a.
$$

근은

$$
\lambda=-a.
$$

따라서 resolvent는

$$
R(s)=\frac1{s+a}
$$

이고 pole은

$$
s=-a.
$$

시간영역에서는

$$
x(t)=Ce^{-at}.
$$

즉

$$
s=-a
\quad\longleftrightarrow\quad
e^{-at}.
$$

2차계

$$
x''(t)+bx'(t)+cx(t)=0
$$

에서는

$$
p(s)=s^2+bs+c.
$$

근을

$$
\lambda_1,\lambda_2\in\mathbb C
$$

라고 하면

$$
p(s)
=
(s-\lambda_1)(s-\lambda_2)
$$

이고

$$
\frac1{p(s)}
=
\frac1{(s-\lambda_1)(s-\lambda_2)}.
$$

따라서 두 근이 두 pole이고, 시간영역에서는

$$
e^{\lambda_1t},
\qquad
e^{\lambda_2t}
$$

가 기본 모드가 된다.

즉 기존에 ODE의 특성방정식을 풀던 것은 사실 이미 **스펙트럼을 계산하고 있었던 것**이다.

---

## 14. semigroup와 resolvent는 같은 동역학의 두 표현

자유계

$$
x'(t)=Ax(t)
$$

의 시간진화는

$$
T(t)=e^{tA}.
$$

그리고 적절한 \(s\)에 대해

$$
R(s,A)
=
\int_0^\infty
e^{-st}T(t)\,dt.
$$

즉

$$
\boxed{
R(s,A)
=
\mathcal L[T](s)
}
$$

이다.

그래서

$$
A
\longrightarrow
T(t)=e^{tA}
\longrightarrow
R(s,A)
$$

라는 연결이 있다.

\(A\)는 infinitesimal generator,

\(T(t)\)는 실제 시간 evolution,

\(R(s,A)\)는 그 evolution의 Laplace-domain representation이다.

그래서 semigroup theory와 spectral theory가 자연스럽게 만난다.

---

## 15. 전달함수는 왜 별도로 필요한가

resolvent는 상태공간 전체를 본다.

$$
R(s,A):X\to X.
$$

그런데 제어에서는 보통 시스템 내부 전체보다

$$
\text{input}\to\text{output}
$$

관계가 중요하다.

입력공간 \(U\), 상태공간 \(X\), 출력공간 \(Y\)와

$$
B:U\to X,
\qquad
C:X\to Y
$$

를 두면

$$
U
\xrightarrow{B}
X
\xrightarrow{R(s,A)}
X
\xrightarrow{C}
Y.
$$

따라서 전달함수는

$$
H(s)
=
C(sI-A)^{-1}B.
$$

즉 resolvent가 내부 전체 동역학이라면 전달함수는 **선택된 입력과 출력 사이에서 보이는 resolvent의 일부**다.

---

## 16. 이제 대수적 국소성이 왜 느껴지는가

2차 ODE에서 얻은 특성다항식을 일반화하여

$$
p:\mathbb C\to\mathbb C
$$

라고 하자.

스펙트럼 점 \(\lambda\)는

$$
p(\lambda)=0
$$

을 만족한다.

이제

$$
s=\lambda+\varepsilon
$$

라고 놓으면 \(\lambda\) 주변에서

$$
p(s)
=
p'(\lambda)(s-\lambda)
+
O((s-\lambda)^2)
$$

이다.

따라서 단순근이면

$$
\frac1{p(s)}
\sim
\frac1{p'(\lambda)}
\frac1{s-\lambda}.
$$

즉 **전체 복잡한 함수 \(p\)를 보지 않아도 근 \(\lambda\) 근처에서는 \(s-\lambda\)라는 국소좌표 하나가 지배한다.**

이게 대수기하적 국소성과 정확히 닮은 부분이다.

점 \(\lambda\in\mathbb C\)에 대응하는 maximal ideal은

$$
\mathfrak m_\lambda
=
(s-\lambda)
\subset\mathbb C[s].
$$

그리고

$$
p(s)
=
(s-\lambda)^m q(s),
\qquad
q(\lambda)\neq0
$$

이면 \(p\)가 \(\lambda\)에서 \(m\)차로 사라진다.

역수를 취하면

$$
\frac1{p(s)}
=
\frac1{(s-\lambda)^m q(s)}
$$

가 되어 \(m\)차 pole이 생긴다.

따라서

$$
\boxed{
\operatorname{ord}_\lambda(p)=m
\quad\Longleftrightarrow\quad
\operatorname{ord}_\lambda(1/p)=-m
}
$$

이다.

이건 정말 localization과 가까운 생각이다. \(\lambda\) 근처에서 \(q(\lambda)\neq0\)인 함수들은 invertible한 것으로 취급하고, 실제 중요한 부분인

$$
(s-\lambda)^m
$$

만 남기는 셈이다.

---

## 17. 선형대수와 가환대수의 연결

\(A:X\to X\)라는 하나의 연산자가 있으면 다항식환

$$
\mathbb C[s]
$$

이 \(X\)에 작용하도록

$$
p(s)\cdot x
:=
p(A)x
$$

를 정의할 수 있다.

그러면 \(X\)는 \(\mathbb C[s]\)-module처럼 볼 수 있다.

특히 최소다항식

$$
m_A\in\mathbb C[s]
$$

는

$$
m_A(A)=0
$$

을 만족하고,

$$
\mathbb C[A]
\cong
\mathbb C[s]/(m_A)
$$

라는 가환대수가 생긴다.

그 최소다항식의 근들은 \(A\)의 스펙트럼과 연결되고, 각 근 주변의 factor

$$
(s-\lambda)^m
$$

은 그 고유값 주변의 Jordan 구조와 연결된다.

즉

$$
\text{operator}
\to
\text{polynomial algebra}
\to
\text{roots}
\to
\text{local factors}
$$

라는 대수적 해석도 가능하다.

이 점 때문에 스펙트럼 이론에는 선형대수, 함수해석, 복소해석, 가환대수의 냄새가 동시에 난다.

---

## 18. 전체 목적과 필요의 연쇄

전체를 가장 압축하면 다음 하나의 흐름이다.

$$
\boxed{
\begin{array}{c}
\text{time translation}
\\[4pt]
\downarrow
\\[4pt]
\text{generator }D\text{ or }A
\\[4pt]
\downarrow
\\[4pt]
De^{st}=se^{st}
\\[4pt]
\downarrow
\\[4pt]
\text{exponential modes diagonalize differentiation}
\\[4pt]
\downarrow
\\[4pt]
\text{Laplace transform}
\\[4pt]
\downarrow
\\[4pt]
D-A
\;\longmapsto\;
sI-A
\\[4pt]
\downarrow
\\[4pt]
\text{solve by inversion}
\\[4pt]
\downarrow
\\[4pt]
R(s,A)=(sI-A)^{-1}
\\[4pt]
\downarrow
\\[4pt]
R(s,A)
=
\sum_j\frac1{s-\lambda_j}P_j
\\[4pt]
\downarrow
\\[4pt]
\sigma(A)
=
\mathbb C\setminus\rho(A)
\\[4pt]
\downarrow
\\[4pt]
\text{poles and singularities}
\\[4pt]
\downarrow
\\[4pt]
\lambda=\alpha+i\beta
\Longleftrightarrow
e^{\alpha t}e^{i\beta t}
\\[4pt]
\downarrow
\\[4pt]
\text{decay / oscillation / growth}
\end{array}
}
$$

그리고 이 흐름 옆에 두 갈래가 붙는다.

$$
A
\longrightarrow
e^{tA}
$$

는 **시간영역의 semigroup 관점**이고,

$$
A
\longrightarrow
\mathbb C[s]/(m_A)
\longrightarrow
(s-\lambda)\text{ 주변의 local structure}
$$

는 **대수적 관점**이다.

결국 이 모든 것은 하나의 아이디어다.

> **시간 전체의 복잡한 동역학을 직접 추적하지 말고, 그것을 생성하는 연산자를 지수 고유모드로 분해하고, Laplace transform으로 복소 \(s\)-plane에 옮긴 뒤, 역연산이 실패하는 특수점과 그 주변의 국소 구조를 읽어서 시간거동을 이해한다.**

이게 **평행이동 → 생성자 → 지수 고유모드 → Laplace → \(sI-A\) → resolvent → spectrum → pole → semigroup → algebraic locality**의 한 줄짜리 골격이다.
