# M4 連立一次方程式と最小二乗法

| 項目 | 内容 |
|---|---|
| 到達目標 | 連立一次方程式 $Ax = b$ に、解が1つある・ない・無数にある場合を区別できる。方程式の数が多すぎるときに、残差の2乗和を最小にする解(最小二乗解)を求め、それが正しいことを確かめられる |
| 前提 | M1(行列とベクトルの積)、M3(偏微分・勾配) |
| 時間の目安 | 本文 1時間、notebook 1.5時間 |
| 使う場面 | 教師あり学習(線形回帰の重み)、強化学習(方策の価値の計算)、ロボット(数値逆運動学の1ステップ) |
| notebook | [`04_linear_systems_least_squares.ipynb`](04_linear_systems_least_squares.ipynb) |

3分野には、「行列とベクトルの積で書いた式から、未知のベクトルを求める」という同じ形の問題が出てくる。この単元では、その解き方と、解けないときの考え方を学ぶ。

## 1. 連立一次方程式

次の連立方程式を考える。

$$
\begin{cases}
2x_1 + x_2 = 5 \\
x_1 - x_2 = 1
\end{cases}
\qquad\Longleftrightarrow\qquad
\underbrace{\begin{pmatrix} 2 & 1 \\ 1 & -1 \end{pmatrix}}_{A}
\underbrace{\begin{pmatrix} x_1 \\ x_2 \end{pmatrix}}_{x}
=
\underbrace{\begin{pmatrix} 5 \\ 1 \end{pmatrix}}_{b}
$$

左の連立方程式と、右の行列の式は同じものである(M1 の行列とベクトルの積)。解は $x = (2, 1)^\top$。

2つの方程式は、平面上の2本の直線と見ることができる。解は2本の直線の交点である。

$2 \times 2$ の場合、$A = \begin{pmatrix} a & b \\ c & d \end{pmatrix}$ の**行列式** $\det A = ad - bc$ が 0 でなければ、解はただ1つに決まり、

$$
x = A^{-1} b, \qquad A^{-1} = \frac{1}{ad - bc} \begin{pmatrix} d & -b \\ -c & a \end{pmatrix}
$$

で求まる。

> [!IMPORTANT]
> **NumPy では `np.linalg.solve(A, b)` を使う**。逆行列を計算してから掛ける `np.linalg.inv(A) @ b` は、計算が多く、誤差も大きくなりやすいので使わない。

## 2. 解がない・無数にあるとき

$\det A = 0$ のときは、2本の直線が平行になる。

- 平行で重ならない(例:$x_1 + x_2 = 1$ と $x_1 + x_2 = 3$):**解がない**
- 同じ直線(例:$x_1 + x_2 = 1$ と $2x_1 + 2x_2 = 2$):**解が無数にある**

どちらの場合も、2つの方程式のうち「本当に独立な方程式」は1つしかない。独立な行(または列)の数を、行列の**ランク**という。$n \times n$ の行列で、ランクが $n$ なら解はただ1つ、$n$ より小さければ、解がないか無数にあるかのどちらかである。NumPy では `np.linalg.matrix_rank(A)` で求まる。

> [!WARNING]
> **ほとんど平行なとき**:$\det A$ が 0 に近いと、$b$ が少し変わるだけで解が大きく変わる。数値の計算では、この「ほとんど解けない」状態に注意が要る。ロボットの特異姿勢(M3 の確認課題、K4)は、この状態に当たる。

## 3. 方程式が多すぎるとき:最小二乗法

データに直線を当てはめるときのように、未知数より方程式の方が多いことがよくある。たとえば、3つの点 $(0, 1)$、$(1, 2)$、$(2, 2)$ に直線 $y = w_0 + w_1 t$ を当てはめたいとすると、

$$
\underbrace{\begin{pmatrix} 1 & 0 \\ 1 & 1 \\ 1 & 2 \end{pmatrix}}_{A\;(3 \times 2)}
\underbrace{\begin{pmatrix} w_0 \\ w_1 \end{pmatrix}}_{w}
\approx
\underbrace{\begin{pmatrix} 1 \\ 2 \\ 2 \end{pmatrix}}_{b}
$$

となる。3つの点は一直線に並んでいないので、すべての方程式をちょうど満たす $w$ はない。

そこで、ずれ(**残差**)$r = b - Aw$ の2乗和 $\lVert b - Aw \rVert^2$ を最も小さくする $w$ を求める。これを**最小二乗法**という。

**正規方程式**:$L(w) = \lVert b - Aw \rVert^2$ の勾配(M3)は $\nabla L = -2A^\top (b - Aw)$ である。これを 0 とおくと、

$$
A^\top A\, w = A^\top b
$$

が得られる。$A^\top A$ は $2 \times 2$ の正方行列なので、§1 の方法で解ける。上の例では $w = (7/6,\ 1/2)^\top$ になる。

> [!TIP]
> **最小二乗解の確かめ方**:正規方程式は $A^\top r = 0$ と同じである。つまり、**残差 $r$ は $A$ のすべての列と直交する**。求めた解について $A^\top r$ がほぼ 0 になるかを確かめればよい。

NumPy では `np.linalg.lstsq(A, b, rcond=None)` で最小二乗解が求まる。正規方程式を `solve` で解くより、数値的に安定している。

## 4. 3分野での例

| 応用 | 式 | 解き方 |
|---|---|---|
| 線形回帰(S1・S2) | $Xw \approx y$($X$ はサンプル数 × 特徴量で、縦長) | 最小二乗法 |
| 固定した方策の価値(R4) | $(I - \gamma P_\pi)\, v = r_\pi$(状態数 × 状態数の正方行列) | `solve`。$0 \le \gamma < 1$ なら解はただ1つ |
| 数値逆運動学の1ステップ(K4) | $J(q)\, \Delta q \approx e$ | 正方で $\det J \neq 0$ なら `solve`。正方でない、または特異に近いときは最小二乗法(疑似逆行列) |

**強化学習の例**:状態が3つのマルコフ連鎖で、状態 $s$ にいるときにもらえる報酬を $r_s$、割引率を $\gamma$ とすると、各状態の価値 $v_s$(将来もらえる報酬の割引和の期待値)は

$$
v = r + \gamma P v \quad\Longleftrightarrow\quad (I - \gamma P)\, v = r
$$

を満たす。$P$ はM2の遷移行列である。これは連立一次方程式なので、`solve` で一度に解ける。R4 の「方策評価」は、同じ式を反復で解く方法である。

## 5. 確認課題

1. $\begin{pmatrix} 1 & 2 \\ 2 & 4 \end{pmatrix} x = \begin{pmatrix} 3 \\ 6 \end{pmatrix}$ と $\begin{pmatrix} 1 & 2 \\ 2 & 4 \end{pmatrix} x = \begin{pmatrix} 3 \\ 5 \end{pmatrix}$ は、それぞれ解がいくつあるか。行列のランクはいくつか
2. §3 の例で、正規方程式を手で解いて $w = (7/6, 1/2)^\top$ を確かめよ。残差 $r$ を求め、$A^\top r = 0$ を確かめよ
3. 2状態のマルコフ連鎖 $P = \begin{pmatrix} 0.9 & 0.1 \\ 0.5 & 0.5 \end{pmatrix}$、報酬 $r = (0, 1)^\top$、$\gamma = 0.9$ のとき、価値 $v$ を求めよ(notebook で確かめる)

## 6. 補足

- *Mathematics for Machine Learning*(<https://mml-book.github.io/>)の第2章(連立一次方程式)と第3章(射影)。最小二乗解は「$b$ を $A$ の列が張る空間へ正射影したもの」として理解できる
- 線形回帰としての最小二乗法は [`machine-learning/linear-regression.md`](https://github.com/oit-cpai/research-handbook/blob/main/machine-learning/linear-regression.md) §2
