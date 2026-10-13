# cpai-foundations — 研究の基礎コース(学習マップ)

研究室に配属された人が、**強化学習(離散)・教師あり学習(深層学習なし)・ロボットの運動学**の3分野と、それを支える数学を、手計算とプログラムを対応させながら身につけるためのコース。とくに、3年生の早期配属(2026年10月末〜)で最初に使うことを想定している。

大阪工業大学 Cyber Physical AI 研究室(CPAI)の学生向けに作っているが、誰でも自由に使ってよい([ライセンス](#ライセンス))。

このページは、コース全体の**地図**である。何ができれば「分かった」とするか(到達目標)、どの順で学ぶか、どの教材を使うかを示す。

## 0. 何ができれば「分かった」とするか

コース全体の目標は次のとおり。

> **小さな問題について、数式の意味を説明し、手計算とプログラムを対応させ、条件を変えた結果を確かめられる。**

プログラムが動くことよりも、次のような質問に答えられることを重視する。

- なぜ、この計算で期待値が求まるのか
- この行列の行と列は、それぞれ何を表すのか
- 学習用のデータでの誤差が小さくても、新しいデータで失敗するのはなぜか
- 逆運動学で得た関節角が正しいことを、どう確かめるのか

3分野それぞれの到達目標は次のとおり。

| 分野 | 標準の到達目標(コース全体) | 最初の到達点(全員) |
|---|---|---|
| 強化学習(離散) | 小さなMDPを定義し、モデルが既知のときの価値反復、経験からのモデルの推定、Q学習などを実装して比べられる | 2〜3状態の例で価値を手計算し、コードで確かめられる |
| 教師あり学習 | 回帰と分類について、入力・正解・損失を説明し、学習用と評価用のデータを分けてモデルを比べられる | 線形回帰で、予測・残差・損失の関係を説明できる |
| ロボットの運動学 | 平面アームの順・逆運動学を理解し、座標変換とヤコビ行列を使って、空間アームの順運動学・数値逆運動学へ広げられる | 2リンク平面アームの順運動学と解析的な逆運動学を説明できる |

3年生の最初の履修では、**全員が3分野の入口(最初の到達点)を経験し、そのあと1分野を選んで標準の到達目標まで仕上げる**。

## 1. 学び方

### 1.1 最初にやること

1. [診断課題](diagnostic.md)を解く(30〜45分)。点数をつけるものではない。苦手なところを見つけ、どの単元から始めるかを決めるために使う
2. このページの「3. 学ぶ順番」に沿って、単元を進める

### 1.2 1つの単元の進め方

各単元は、**Markdownの本文**と**Colabで開くnotebook**の組でできている。本文で考え方を読み、notebookで手を動かす。notebookは、毎回次の順に進む。

1. **実行する前に予想する**(結果がどうなるかを先に書く)
2. **小さな例を手計算する**
3. **コードで確かめる**(手計算と一致するか)
4. **中心になる部分を自分で実装する**(`TODO` の部分)
5. **条件を変えて比べる**
6. **結果を自分の言葉で説明する**

notebookには、自分の実装が正しいかを確かめる `check_...()` 関数が入っている。`OK` と出るまで直してから先に進む。

notebookは、新しいランタイムで上から順に実行すれば動くように作ってある(必要なライブラリは NumPy と Matplotlib だけ)。各notebookの先頭の「Open In Colab」ボタンから開く。

### 1.3 生成AIの使い方

自習では、ChatGPT・Claude などの生成AIを使ってよい。分からない言葉を聞く、エラーの意味を聞く、別の説明を求める、といった使い方を勧める。

ただし、**理解したかどうかは、自分で説明できるかで確かめる**。各単元の終わりに、次の3つを行う。

- notebookの「予想」と「説明」の欄を、自分の言葉で書く
- 教員と会う時間(週1回程度)に、notebookを見せながら「ここを変えると何が起きるか」を2〜3分で説明する
- その場で、ごく小さな別の問題を解く

### 1.4 時間の目安

1週間に3〜4時間の自習と、週1回30〜60分の確認を想定している。最初の2単元にかかった時間を記録し、教員に伝える(分量の調整に使う)。

## 2. 単元の一覧

状態:**✓** = このリポジトリに用意済み(2026-10-13 時点:M1〜M4、R5、S1)、**既存** = 既存の教材の該当する節を読む、**予定** = これから作る

「既存」の教材のうち、Markdown の本文は研究室の [research-handbook](https://github.com/oit-cpai/research-handbook)(研究室のメンバー向け)、notebook は [lab-core](https://github.com/oit-cpai/lab-core)(公開)にある。

### 2.1 共通基礎(数学と計算)

| # | 単元 | 主な内容 | 教材 | 状態 |
|---|---|---|---|---|
| M1 | 数式・ベクトル・配列 | 添字・総和・最大値、ベクトル・内積・ノルム、行列積とサイズ、配列の形と軸 | [math/01-vectors-arrays.md](math/01-vectors-arrays.md) | ✓ |
| M2 | 確率・期待値・標本平均 | 確率変数、期待値と標本平均の違い、分散、条件付き確率、数え上げによる確率の推定、マルコフ連鎖の入口 | [math/02-probability-expectation.md](math/02-probability-expectation.md) | ✓ |
| M3 | 微分・一次近似 | 微分と数値微分、偏微分・勾配、一次近似、ヤコビ行列、勾配法 | [math/03-derivative-linear-approx.md](math/03-derivative-linear-approx.md) | ✓ |
| M4 | 連立一次方程式と最小二乗法 | 解の存在と一意性、ランクの直観、最小二乗法と正規方程式、`solve` と `lstsq`、マルコフ連鎖の価値 | [math/04-linear-systems-least-squares.md](math/04-linear-systems-least-squares.md) | ✓ |
| M5 | 積分と確率密度 | 定積分と面積、確率密度と確率、連続変数の期待値、ヒストグラム | — | 予定 |
| M6 | マルコフ連鎖 | 遷移行列、状態分布の変化、定常分布 | M2 の §6 で入口のみ | 予定 |
| M7 | 数値計算と実験の作法 | 浮動小数点、反復計算と停止条件、乱数と seed、再現性、複数 seed での比較 | [`reinforcement-learning/hyperparameter.md`](https://github.com/oit-cpai/research-handbook/blob/main/reinforcement-learning/hyperparameter.md) を一部 | 予定 |

固有値・特異値分解(SVD)は、最初の共通基礎には入れない。数値逆運動学(K6)で「動きにくい方向がある」ことを見てから導入する。

### 2.2 強化学習(離散)

| # | 単元 | 前提 | 教材 | 状態 |
|---|---|---|---|---|
| R1 | 探索と活用(バンディット) | M2 | [`reinforcement-learning/bandit.md`](https://github.com/oit-cpai/research-handbook/blob/main/reinforcement-learning/bandit.md)、notebook [`bandit_lecture`](https://github.com/oit-cpai/lab-core/blob/main/examples/notebooks/bandit_lecture.ipynb) | 既存 |
| R2 | 環境を作る(`step()`) | M1 | [`reinforcement-learning/gridworld-step.md`](https://github.com/oit-cpai/research-handbook/blob/main/reinforcement-learning/gridworld-step.md)、notebook [`gridworld_step_exercise`](https://github.com/oit-cpai/lab-core/blob/main/examples/notebooks/gridworld_step_exercise.ipynb) | 既存 |
| R3 | MDPとベルマン方程式 | M2 | [`reinforcement-learning/mdp.md`](https://github.com/oit-cpai/research-handbook/blob/main/reinforcement-learning/mdp.md)(§1〜6 を先に。§7 は R4 のあとでよい) | 既存 |
| R4 | 動的計画法(方策評価・価値反復) | R3、M1 | [`reinforcement-learning/dynamic-programming.md`](https://github.com/oit-cpai/research-handbook/blob/main/reinforcement-learning/dynamic-programming.md) §1〜5、notebook [`dp_gridworld`](https://github.com/oit-cpai/lab-core/blob/main/examples/notebooks/dp_gridworld.ipynb) | 既存 |
| R5 | 経験からモデルを推定する | M2 §5、M4 §4、R4 | [rl/05-model-estimation.md](rl/05-model-estimation.md)(数え上げで $\hat P$・$\hat R$ を推定し、価値反復で計画して、本当のモデルで評価する) | ✓ |
| R6 | モンテカルロ法 | R4 | [`reinforcement-learning/monte-carlo.md`](https://github.com/oit-cpai/research-handbook/blob/main/reinforcement-learning/monte-carlo.md) §1〜4 | 既存 |
| R7 | TD学習・Sarsa・Q学習 | R6 | [`reinforcement-learning/td-learning.md`](https://github.com/oit-cpai/research-handbook/blob/main/reinforcement-learning/td-learning.md)、`cliff-walking.md`、notebook [`cliff_walking_lecture`](https://github.com/oit-cpai/lab-core/blob/main/examples/notebooks/cliff_walking_lecture.ipynb) | 既存 |
| R8 | Dyna-Q(発展) | R5、R7 | [`reinforcement-learning/model-based.md`](https://github.com/oit-cpai/research-handbook/blob/main/reinforcement-learning/model-based.md) §1〜2 | 既存 |

R4 で求めた最適価値を「正解」として、R5〜R8 の結果を確かめる。比べるときは、**環境から得たサンプル数をそろえる**。

### 2.3 教師あり学習(深層学習なし)

| # | 単元 | 前提 | 教材 | 状態 |
|---|---|---|---|---|
| S1 | 1変数の線形回帰 | M1、M2、M3 | [supervised/01-linear-regression-1d.md](supervised/01-linear-regression-1d.md)(入力・正解・予測・残差・損失、推定のばらつき、学習用と評価用の分割) | ✓ |
| S2 | 複数入力の線形回帰と最小二乗法 | M1、M4 | [`machine-learning/linear-regression.md`](https://github.com/oit-cpai/research-handbook/blob/main/machine-learning/linear-regression.md) §1〜2 | 既存 |
| S3 | 勾配法 | M3 | M3 の §5、新しく作る(同じ損失を最小二乗と勾配法で解く) | 予定 |
| S4 | 多項式回帰・リッジ回帰と過学習 | S2 | [`machine-learning/ml-basics.md`](https://github.com/oit-cpai/research-handbook/blob/main/machine-learning/ml-basics.md)、`linear-regression.md` §4、notebook [`polynomial_regression`](https://github.com/oit-cpai/lab-core/blob/main/examples/notebooks/polynomial_regression.ipynb) | 既存 |
| S5 | ロジスティック回帰と分類 | S3、M2 | [`machine-learning/classification.md`](https://github.com/oit-cpai/research-handbook/blob/main/machine-learning/classification.md)(ロジスティック回帰の節)、notebook [`logistic_regression`](https://github.com/oit-cpai/lab-core/blob/main/examples/notebooks/logistic_regression.ipynb) | 既存 |
| S6 | 評価:データの分け方と指標 | S4 | [`machine-learning/model-evaluation.md`](https://github.com/oit-cpai/research-handbook/blob/main/machine-learning/model-evaluation.md) §1・§5・§6 | 既存 |

モデルの数を増やすことより、**評価を正しく行うこと**(学習用・検証用・テスト用のデータの役割、前処理を学習用のデータだけで決めること)を重視する。

### 2.4 ロボットの運動学

| # | 単元 | 前提 | 教材 | 状態 |
|---|---|---|---|---|
| K1 | 2リンク平面アームの順運動学 | M1(三角関数) | [`robotics/kinematics.md`](https://github.com/oit-cpai/research-handbook/blob/main/robotics/kinematics.md) §5、notebook [`arm_kinematics`](https://github.com/oit-cpai/lab-core/blob/main/examples/notebooks/arm_kinematics.ipynb) 課題1 | 既存 |
| K2 | 解析的な逆運動学 | K1 | [`robotics/kinematics.md`](https://github.com/oit-cpai/research-handbook/blob/main/robotics/kinematics.md) §6、notebook [`arm_kinematics`](https://github.com/oit-cpai/lab-core/blob/main/examples/notebooks/arm_kinematics.ipynb) 課題2 | 既存 |
| K3 | 座標変換(回転行列・同次変換) | M1 | [`robotics/kinematics.md`](https://github.com/oit-cpai/research-handbook/blob/main/robotics/kinematics.md) §2〜3 | 既存 |
| K4 | 平面アームの数値逆運動学 | M3、K1 | [`robotics/kinematics.md`](https://github.com/oit-cpai/research-handbook/blob/main/robotics/kinematics.md) §7〜8、notebook [`arm_kinematics`](https://github.com/oit-cpai/lab-core/blob/main/examples/notebooks/arm_kinematics.ipynb) 課題3・応用 | 既存 |
| K5 | 空間アーム(4〜6自由度)の順運動学 | K3 | [`robotics/kinematics.md`](https://github.com/oit-cpai/research-handbook/blob/main/robotics/kinematics.md) §4(DH記法)、notebook は新しく作る | 予定 |
| K6 | 空間アームの数値逆運動学(発展) | K4、K5 | 新しく作る(位置・姿勢の誤差、疑似逆行列、減衰、特異姿勢) | 予定 |

最初に次の3つを区別しておく:**関節の自由度**(関節変数の数)、**手先の自由度**(位置3+姿勢3 = 最大6)、**座標変換の行列の大きさ**(3次元の同次変換は 4×4。「4」は自由度の数ではない)。

## 3. 学ぶ順番(3年生の早期配属)

| 段階 | 週の目安 | 単元 | 到達点 |
|---|---|---|---|
| 導入・診断 | 1〜2週 | 診断課題、M1 | Colab で notebook を実行・保存できる。自分の苦手なところが分かる |
| 共通基礎+3分野の入口 | 5〜6週 | M2、M3、R2〜R4、S1〜S2、K1〜K2 | 小さな価値の計算、線形回帰、平面アームを説明できる |
| 分野別の標準課題 | 4〜6週 | 選んだ1分野の残りの単元 | 実装と比べる実験を一通り行える |
| 小課題の仕上げと発表 | 2週 | 選んだ分野の小課題 | 条件を変えた結果と考察をまとめ、もう一度実行できる形で提出する |

全体で12〜16週を想定している。最初の2単元の実際の所要時間を見て、分量を調整する。

**同じ題材を繰り返し使う**:3分野を通して、次の3つの題材を何度も使う。初めは図で見て、次に手計算し、その次に推定や最適化をする。

- 小さな確率的グリッドの環境(強化学習)
- 自分で作った回帰・分類のデータ(教師あり学習)
- 2リンク平面アーム(運動学)

## 4. 3分野に共通する計算

同じ行列の計算が、3分野で違う意味で使われる。単元を進めながら、この表に戻ってくるとよい。

| 応用 | 計算の形 | 求めたいもの | 単元 |
|---|---|---|---|
| 線形回帰 | $Xw \approx y$ | データに合う重み $w$ | S2 |
| 固定した方策の価値 | $(I-\gamma P_\pi)\,v_\pi = r_\pi$ | 各状態の価値 $v_\pi$ | R4 |
| 数値逆運動学の1ステップ | $J(q)\,\Delta q \approx e$ | 手先の誤差を減らす関節角の修正 $\Delta q$ | K4 |

配列の各方向(軸)が何を表すかも、3分野で比べておく。

| 対象 | 配列の形 | 各方向が表すもの |
|---|---|---|
| 教師あり学習のデータ行列 $X$ | $N \times D$ | サンプル × 特徴量 |
| 強化学習の遷移確率 $P$ | $\lvert S\rvert \times \lvert A\rvert \times \lvert S\rvert$ | 今の状態 × 行動 × 次の状態 |
| ロボットのヤコビ行列 $J$ | $m \times n$ | 手先の変化の成分 × 関節変数 |

## 5. 言葉から探す(索引)

| 言葉 | 単元 |
|---|---|
| 内積、行列積、転置、ノルム | M1 |
| 配列の形(shape)・軸(axis) | M1 |
| 期待値、標本平均、分散、大数の法則 | M2、R1 |
| 条件付き確率 | M2、R3 |
| マルコフ性、マルコフ連鎖、遷移行列 | M2 §6、M6、R3 |
| 数え上げによる確率の推定 | M2 §5、R5 |
| 微分、数値微分、偏微分、勾配 | M3、S3 |
| 一次近似、ヤコビ行列 | M3、K4 |
| 最小二乗法 | M4、S2、K4 |
| 過学習、正則化 | S4 |
| データの分割、データリーク | S6 |
| ベルマン方程式、価値反復 | R3、R4 |
| Q学習、ε-greedy | R7、R1 |
| 回転行列、同次変換 | K3、K5 |
| 特異姿勢、疑似逆行列 | K4、K6 |

## 6. 大学院進学を考えている人へ(発展課題)

各分野の標準課題が終わったら、次に挑戦するとよい(誰が取り組んでもよい)。

- ベルマン作用素の縮小性と、価値反復が収束することの証明(R4 のあと)
- リッジ回帰の解の導出と、正則化の効果の解析(S4 のあと)
- 特異値と数値逆運動学の関係(K6 のあと)

## 7. 参考書

このコースの中心は、このフォルダの日本語の本文と notebook である。次の本は、もっと詳しく知りたいとき、または教員が範囲と記法を照らし合わせるときに使う。

| 資料 | 使い方 |
|---|---|
| M. P. Deisenroth, A. A. Faisal, C. S. Ong, *Mathematics for Machine Learning*(無料で読める:<https://mml-book.github.io/>) | 線形代数・微積分・確率・最適化の範囲と記法の確認 |
| R. S. Sutton, A. G. Barto『強化学習(第2版)』(森北出版) | 強化学習の単元(主に第2〜6章・第8章)の参照先 |
| K. M. Lynch, F. C. Park, *Modern Robotics*(無料で読める:<https://modernrobotics.northwestern.edu/>) | 座標系、剛体運動、順運動学、ヤコビ行列、逆運動学の参照先 |
| scikit-learn の公式ドキュメント「Common pitfalls and recommended practices」 | データの分割、前処理、評価の手順の確認 |

## 8. 教材を作る人へ(単元の形)

新しい単元は、次の形にそろえる。

| 部分 | 内容 |
|---|---|
| 学習の入口(Markdown の冒頭) | 到達目標、前提となる単元、所要時間の目安、どこで使うか |
| 本文(Markdown) | 定義、記号、図、小さな数値例、必要な導出 |
| notebook | 予想 → 手計算 → コードで確認 → 実装(`TODO`)→ 条件を変える → 説明。`check_...()` で自分で確かめられる。1冊の主な目標は1〜2個 |
| 確認課題(Markdown の最後) | 新しい条件での計算と説明 |
| 補足 | 発展課題、参考資料 |

notebook は、新しいランタイムで上から実行すれば動くこと(必要なデータは notebook の中で作る)。CPU で数分以内に終わること。演習の版は `math/` などの単元のフォルダに、解答つきの版は `solutions/` に置く。

## リポジトリの構成

```text
cpai-foundations/
├── README.md               # このページ(学習マップ)
├── diagnostic.md           # 診断課題
├── diagnostic-answers.md   # 診断課題の解答と、次に進む単元
├── math/                   # 共通基礎(数学)の単元:本文(.md)と演習の notebook(.ipynb)
├── rl/                     # 強化学習の単元(既存の教材にない部分)
├── supervised/             # 教師あり学習の単元(既存の教材にない部分)
└── solutions/              # notebook の解答つきの版
```

誤りや分かりにくいところを見つけたら、Issue で知らせてほしい。

## ライセンス

[MIT License](LICENSE)。著作権表示とライセンス文を残せば、授業・自習・改変・再配布などに自由に使ってよい。
