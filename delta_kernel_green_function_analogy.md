https://chatgpt.com/share/6aa1e958-b4e4-83ee-ac11-cb276f301a7d?ogimg=plain

# 유한차원 선형대수에서 함수공간의 kernel, Green function, distribution까지

이 글의 목적은 함수공간에서 등장하는 kernel, Dirac delta, Green function, convolution, distribution을 처음부터 별개의 개념으로 배우는 것이 아니다.

각 개념마다 다음 순서를 반복한다.

1. 유한차원에서 실제 숫자로 계산한다.
2. 그 계산의 각 숫자와 벡터가 어떤 기호에 해당하는지 표시한다.
3. 같은 구조를 함수공간으로 옮긴다.
4. 함수공간에서 필요한 정의와 기호를 적는다.

이미 한 번 연결한 기호는 뒤에서 같은 설명을 반복하지 않는다.

---

## 1. 좌표를 뽑고 다시 복원하기: dual basis에서 Dirac delta까지

### 1.1 수치 예시

벡터

```math
\begin{pmatrix}
3\\
5
\end{pmatrix}
```

는

```math
\begin{pmatrix}
3\\
5
\end{pmatrix}
=
3
\begin{pmatrix}
1\\
0
\end{pmatrix}
+
5
\begin{pmatrix}
0\\
1
\end{pmatrix}
```

로 쓸 수 있다.

여기서

```math
e_1=
\begin{pmatrix}
1\\
0
\end{pmatrix},
\qquad
e_2=
\begin{pmatrix}
0\\
1
\end{pmatrix}
```

라고 이름을 붙이고, 벡터를

```math
v=
\begin{pmatrix}
3\\
5
\end{pmatrix}
```

라고 하자.

그러면 위 계산은

```math
\underbrace{
\begin{pmatrix}
3\\
5
\end{pmatrix}
}_{v}
=
\underbrace{3}_{e^1(v)}
\underbrace{
\begin{pmatrix}
1\\
0
\end{pmatrix}
}_{e_1}
+
\underbrace{5}_{e^2(v)}
\underbrace{
\begin{pmatrix}
0\\
1
\end{pmatrix}
}_{e_2}
```

라고 쓸 수 있다.

여기서

```math
e^1(x_1,x_2)=x_1,
\qquad
e^2(x_1,x_2)=x_2
```

는 각각 첫 번째 성분과 두 번째 성분을 뽑는 선형사상이다.

즉

```math
e^1(v)=3,
\qquad
e^2(v)=5.
```

$e_1,e_2$를 기저라고 하고, $e^1,e^2$를 그 기저에 대한 **dual basis**라고 한다.

### 1.2 기호로 일반화

$V$를 유한차원 벡터공간, $\{e_i\}$를 기저, $\{e^i\}$를 dual basis라고 하면

```math
e^i(e_j)=\delta^i{}_j,
```

여기서 $\delta^i{}_j$는 Kronecker delta이다.

```math
\delta^i{}_j
=
\begin{cases}
1,&i=j,\\
0,&i\neq j.
\end{cases}
```

모든 $v\in V$는

```math
v=\sum_i e^i(v)e_i
```

로 복원된다.

즉 dual basis의 역할은 **기저에 대한 좌표를 추출하는 것**이다.

### 1.3 identity와 Kronecker delta

수치적으로

```math
I=
\begin{pmatrix}
1&0\\
0&1
\end{pmatrix}
```

이면

```math
I
\begin{pmatrix}
3\\
5
\end{pmatrix}
=
\begin{pmatrix}
3\\
5
\end{pmatrix}.
```

성분으로 쓰면

```math
v_i=\sum_j\delta_{ij}v_j.
```

따라서 Kronecker delta는 identity map

```math
I:V\to V
```

의 행렬성분이다.

---

### 1.4 함수공간에서는 위치가 연속 index가 된다

이번에는 함수

```math
f:\mathbb R\to\mathbb R,
\qquad
f(x)=x^2+1
```

을 생각하자.

$x=2$에서 함수값은

```math
f(2)=5.
```

이 연산 자체를

```math
\delta_2(f)=f(2)=5
```

라고 쓸 수 있다.

유한차원에서

```math
e^j(v)=v_j
```

가 $j$번째 좌표를 추출했다면, 함수공간에서는

```math
\delta_y(f)=f(y)
```

가 위치 $y$의 값을 추출한다.

즉 처음 한 번만 대응을 적으면

```math
\boxed{
j\longleftrightarrow y,
\qquad
e^j\longleftrightarrow \delta_y
}
```

이다.

여기서 $j$는 이산 index이고 $y$는 연속 index이다.

### 1.5 Dirac delta와 distribution

유한차원에서는 $e^j\in V^*$가 평범한 선형범함수였지만, 연속 index를 다룰 때 등장하는 $\delta_y$는 일반적인 함수가 아니다.

시험함수 공간을

```math
\mathcal D(\Omega)=C_c^\infty(\Omega)
```

라고 하자.

Dirac distribution은 연속선형범함수

```math
\delta_y:\mathcal D(\Omega)\to\mathbb R
```

로 정의되고,

```math
\langle\delta_y,\varphi\rangle=\varphi(y)
```

를 만족한다.

$\mathcal D(\Omega)$ 위의 연속선형범함수들의 공간

```math
\mathcal D'(\Omega)
```

를 **distribution space**라고 한다.

따라서

```math
\delta_y\in\mathcal D'(\Omega).
```

identity의 유한차원 표현

```math
v_i=\sum_j\delta_{ij}v_j
```

은 연속 index에서는 형식적으로

```math
f(x)
=
\int_{\mathbb R}
\delta(x-y)f(y)\,dy
```

가 된다.

여기서

```math
\delta_{ij}
\longleftrightarrow
\delta(x-y),
\qquad
\sum_j
\longleftrightarrow
\int dy
```

라는 대응이 생긴다.

---

## 2. 행렬에서 kernel로

### 2.1 수치 예시

행렬

```math
A=
\begin{pmatrix}
2&1\\
4&3
\end{pmatrix},
\qquad
v=
\begin{pmatrix}
3\\
5
\end{pmatrix}
```

를 생각하자.

그러면

```math
Av
=
\begin{pmatrix}
2\cdot3+1\cdot5\\
4\cdot3+3\cdot5
\end{pmatrix}
=
\begin{pmatrix}
11\\
27
\end{pmatrix}.
```

첫 번째 출력 성분만 보면

```math
11
=
\underbrace{2}_{A_{11}}
\underbrace{3}_{v_1}
+
\underbrace{1}_{A_{12}}
\underbrace{5}_{v_2}.
```

두 번째 출력 성분은

```math
27
=
\underbrace{4}_{A_{21}}
\underbrace{3}_{v_1}
+
\underbrace{3}_{A_{22}}
\underbrace{5}_{v_2}.
```

따라서 일반적으로

```math
(Av)_i=\sum_j A_{ij}v_j.
```

여기서

- $j$는 입력 좌표의 index,
- $i$는 출력 좌표의 index,
- $A_{ij}$는 입력의 $j$번째 성분이 출력의 $i$번째 성분에 기여하는 계수이다.

### 2.2 행렬의 열

기저벡터를 하나씩 넣으면

```math
Ae_1
=
A
\begin{pmatrix}
1\\
0
\end{pmatrix}
=
\begin{pmatrix}
2\\
4
\end{pmatrix},
```

```math
Ae_2
=
A
\begin{pmatrix}
0\\
1
\end{pmatrix}
=
\begin{pmatrix}
1\\
3
\end{pmatrix}.
```

즉

```math
\underbrace{Ae_1}_{\text{첫 번째 열}}
=
\begin{pmatrix}
\underbrace{2}_{e^1(Ae_1)=A_{11}}\\
\underbrace{4}_{e^2(Ae_1)=A_{21}}
\end{pmatrix}.
```

따라서

```math
A_{ij}=e^i(Ae_j).
```

행렬 전체는 각 기저입력 $e_j$에 대한 반응 $Ae_j$를 모은 것이다.

---

### 2.3 함수공간으로 옮기기

함수공간에서 입력 index $j$가 연속변수 $y$가 되고 출력 index $i$가 연속변수 $x$가 되면, 행렬성분 $A_{ij}$에 대응하는 것이 두 변수의 함수 또는 distribution인 kernel

```math
K(x,y)
```

이다.

적분 kernel로 표현되는 선형연산자 $T$는

```math
(Tf)(x)
=
\int K(x,y)f(y)\,dy
```

로 작용한다.

앞 절의 대응을 그대로 사용하면

```math
\boxed{
A_{ij}
\longleftrightarrow
K(x,y)
}
```

이고,

```math
(Av)_i=\sum_jA_{ij}v_j
```

가

```math
(Tf)(x)
=
\int K(x,y)f(y)\,dy
```

로 바뀐다.

또 행렬의 $j$번째 열이 $Ae_j$였으므로, 함수공간에서는 점입력 $\delta_y$에 대한 반응

```math
T\delta_y
```

가 kernel의 $y$에 해당하는 열 역할을 한다.

형식적으로

```math
K(x,y)=(T\delta_y)(x).
```

따라서 **kernel은 행렬을 연속 index로 확장한 것**이고, $K(\cdot,y)$는 행렬의 한 열에 대응한다.

---

## 3. 역행렬에서 Green matrix와 Green function으로

### 3.1 수치 예시

선형방정식

```math
Lu=f
```

를 생각하자.

구체적으로

```math
L=
\begin{pmatrix}
2&1\\
1&1
\end{pmatrix}
```

를 잡으면

```math
L^{-1}
=
\begin{pmatrix}
1&-1\\
-1&2
\end{pmatrix}.
```

예를 들어

```math
f=
\begin{pmatrix}
7\\
4
\end{pmatrix}
```

이면

```math
u
=
L^{-1}f
=
\begin{pmatrix}
1&-1\\
-1&2
\end{pmatrix}
\begin{pmatrix}
7\\
4
\end{pmatrix}
=
\begin{pmatrix}
3\\
1
\end{pmatrix}.
```

실제로

```math
L
\begin{pmatrix}
3\\
1
\end{pmatrix}
=
\begin{pmatrix}
7\\
4
\end{pmatrix}.
```

### 3.2 Green matrix

$L^{-1}$의 열을 하나씩 보자.

```math
L^{-1}e_1
=
\begin{pmatrix}
1\\
-1
\end{pmatrix},
\qquad
L^{-1}e_2
=
\begin{pmatrix}
-1\\
2
\end{pmatrix}.
```

첫 번째 열은

```math
L
\begin{pmatrix}
1\\
-1
\end{pmatrix}
=
\begin{pmatrix}
1\\
0
\end{pmatrix}
=e_1
```

을 만족하고, 두 번째 열은

```math
L
\begin{pmatrix}
-1\\
2
\end{pmatrix}
=
\begin{pmatrix}
0\\
1
\end{pmatrix}
=e_2
```

를 만족한다.

$G=L^{-1}$라고 쓰면

```math
LG=I
```

이고, 열별로

```math
LG_{\cdot j}=e_j.
```

이 $G$를 유한차원에서 **Green matrix**라고 볼 수 있다.

핵심은 각 열 $G_{\cdot j}$가 **단위입력 $e_j$를 만들기 위한 해**라는 점이다.

---

### 3.3 함수공간의 Green function

이제 미분연산자

```math
L:D(L)\subset X\to Y
```

에 대해

```math
Lu=f
```

를 푼다고 하자.

역연산자 $L^{-1}$가 적절히 존재하고 kernel로 표현될 수 있다면

```math
u=L^{-1}f
```

이고,

```math
u(x)
=
\int G(x,y)f(y)\,dy.
```

여기서 $G(x,y)$가 $L^{-1}$의 kernel인 **Green function**이다.

유한차원에서

```math
LG_{\cdot j}=e_j
```

였으므로 연속 index에서는

```math
G(\cdot,y)=L^{-1}\delta_y
```

이고,

```math
L_xG(x,y)=\delta(x-y)
```

가 된다.

즉 Green function은 별개의 신비한 함수가 아니라 **inverse operator의 kernel**이며,

```math
G(\cdot,y)
```

는 역행렬의 한 열 $G_{\cdot j}$에 대응한다.

---

## 4. 차이에만 의존하는 행렬에서 convolution으로

### 4.1 수치 예시: 같은 상대위치에는 같은 계수

이번에는

```math
A=
\begin{pmatrix}
2&1&3\\
3&2&1\\
1&3&2
\end{pmatrix},
\qquad
v=
\begin{pmatrix}
1\\
2\\
4
\end{pmatrix}
```

를 생각하자.

그러면

```math
Av
=
\begin{pmatrix}
2\cdot1+1\cdot2+3\cdot4\\
3\cdot1+2\cdot2+1\cdot4\\
1\cdot1+3\cdot2+2\cdot4
\end{pmatrix}
=
\begin{pmatrix}
16\\
11\\
15
\end{pmatrix}.
```

이 행렬에서는 계수가 절대적인 $i,j$ 각각보다 두 index의 상대적 차이에 의해 반복된다. 주기적 index를 사용하면

```math
A_{ij}=a_{i-j\;\mathrm{mod}\;3}
```

꼴이다.

따라서

```math
(Av)_i
=
\sum_j a_{i-j}v_j.
```

이 식은 유한한 주기 격자에서의 **discrete convolution**이다.

### 4.2 함수공간으로 옮기기

함수공간에서도 kernel이 두 위치 $x,y$ 각각에 독립적으로 의존하지 않고 차이

```math
x-y
```

에만 의존한다고 하자.

즉

```math
K(x,y)=k(x-y).
```

그러면

```math
(Tf)(x)
=
\int k(x-y)f(y)\,dy.
```

오른쪽을 convolution으로 정의하면

```math
(k*f)(x)
=
\int k(x-y)f(y)\,dy
```

이므로

```math
Tf=k*f.
```

이 구조가 나타나는 대표적인 조건이 translation invariance이다.

평행이동 연산자

```math
\tau_a f(x)=f(x-a)
```

에 대해

```math
T\tau_a=\tau_aT
```

가 성립하면, 적절한 조건 아래 kernel이 $x-y$에만 의존하는 convolution kernel로 나타난다.

즉

```math
\boxed{
\text{general kernel }K(x,y)
\xrightarrow{\text{translation invariance}}
k(x-y)
\xrightarrow{}
\text{convolution}
}
```

이다.

---

## 5. 가장 단순한 Green function: 미분연산자와 Heaviside 함수

미분연산자

```math
D=\frac{d}{dt}
```

를 생각하자.

문제는

```math
Du=f
```

를 푸는 것이다.

앞 절의 Green function 정의에 따르면 $D^{-1}$의 kernel $G$는

```math
DG=\delta
```

를 만족해야 한다.

Heaviside 함수

```math
H(t)
=
\begin{cases}
0,&t<0,\\
1,&t>0
\end{cases}
```

는 고전적인 의미에서는 $t=0$에서 미분할 수 없다.

그러나 distributional derivative를 사용하면

```math
DH=\delta.
```

따라서 $H$가 $D^{-1}$의 Green function 역할을 한다.

실제로

```math
u=H*f
```

라고 두면

```math
D(H*f)
=
(DH)*f
=
\delta*f
=
f.
```

즉

```math
Du=f.
```

여기서 distribution이 필요한 이유가 다시 나타난다. Green function을 다루기 위해서는 $\delta$뿐 아니라 고전적으로 미분할 수 없는 $H$의 미분도 다룰 수 있어야 한다.

---

## 6. distribution에서 미분을 정의하기

함수 $f$가 충분히 매끄럽고 시험함수 $\varphi\in C_c^\infty(\Omega)$라면 부분적분으로

```math
\int f'(x)\varphi(x)\,dx
=
-
\int f(x)\varphi'(x)\,dx
```

를 얻는다.

distribution에서는 이 식의 오른쪽을 미분의 정의로 사용한다.

$T\in\mathcal D'(\Omega)$의 distributional derivative $DT\in\mathcal D'(\Omega)$를

```math
\langle DT,\varphi\rangle
=
-
\langle T,D\varphi\rangle
```

로 정의한다.

이 정의 때문에 고전적 미분이 존재하지 않는 Heaviside 함수도

```math
DH=\delta
```

라는 의미를 갖는다.

---

## 7. 고전해에서 weak solution으로

미분연산자

```math
L:D(L)\subset X\to Y
```

는 일반적으로 모든 함수에 정의되는 bounded operator가 아니다.

또

```math
LG=\delta
```

에서 오른쪽의 $\delta$도 일반적인 함수가 아니다.

따라서 미분방정식을 항상 점별 등식

```math
Lu(x)=f(x)
```

으로 요구하면 다룰 수 있는 해가 너무 제한된다.

distribution의 언어에서는 시험함수 $\varphi$에 대해

```math
\langle Lu,\varphi\rangle
=
\langle f,\varphi\rangle
```

가 성립하는 방식으로 방정식을 해석할 수 있다.

미분을 부분적분을 통해 $u$에서 시험함수 $\varphi$ 쪽으로 옮기면, $u$가 고전적 의미에서 충분히 미분 가능하지 않아도 방정식을 정의할 수 있다.

이 관점이 **weak solution**으로 이어진다.

약한 미분을 가진 함수들을 다루기 위해 대표적으로 Sobolev 공간

```math
W^{k,p}(\Omega)
```

를 사용하고,

```math
H^k(\Omega)=W^{k,2}(\Omega)
```

로 쓴다.

---

## 8. convolution을 군으로 확장하기

$\mathbb R^n$에서는 두 점의 상대위치를

```math
x-y
```

로 표현했다.

더 일반적으로 국소콤팩트 군 $G$와 Haar 측도 $dg$가 있으면, 함수

```math
f,k:G\to\mathbb C
```

에 대해 convolution을

```math
(f*k)(x)
=
\int_G f(g)k(g^{-1}x)\,dg
```

로 정의할 수 있다.

$\mathbb R^n$의 덧셈군에서는

```math
g^{-1}x=x-g
```

이므로 앞에서 사용한

```math
\int k(x-y)f(y)\,dy
```

형태가 다시 나온다.

따라서 convolution의 핵심은 단순히 $x-y$라는 식 자체가 아니라 **대칭군에서 상대위치를 사용해 입력을 합성하는 구조**이다.

---

# 전체 연결

이 글의 흐름을 한 줄로 쓰면

```math
\boxed{
\begin{array}{c}
\text{coordinate extraction by dual basis}\\
\downarrow\\
\text{Kronecker delta and identity matrix}\\
\downarrow\\
\text{Dirac distribution and continuous index}\\
\downarrow\\
\text{matrix }A_{ij}\;\longrightarrow\;\text{kernel }K(x,y)\\
\downarrow\\
\text{matrix column }Ae_j\;\longrightarrow\;K(\cdot,y)\\
\downarrow\\
\text{inverse matrix / Green matrix}\\
\downarrow\\
\text{Green function }G(x,y)\\
\downarrow\\
\text{translation invariance}\\
\downarrow\\
\text{convolution}\\
\downarrow\\
\text{distributional derivative}\\
\downarrow\\
\text{weak solution and Sobolev space}
\end{array}
}
```

핵심은 유한차원의 구조를 버리고 새로운 개념으로 넘어가는 것이 아니다.

- dual basis의 좌표 추출은 연속 index에서 evaluation functional과 Dirac distribution으로 이어지고,
- 행렬은 kernel로,
- 행렬의 열은 점입력에 대한 kernel의 반응으로,
- 역행렬은 inverse operator의 kernel인 Green function으로,
- 상대 index에만 의존하는 행렬 구조는 translation-invariant convolution으로 이어진다.

함수공간에서는 이 구조를 그대로 유지하려 할 때 Dirac delta나 미분 불가능한 함수가 등장하기 때문에 distribution, distributional derivative, weak solution 같은 추가적인 수학적 구조가 필요해진다.
