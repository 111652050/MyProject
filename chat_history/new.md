請問這樣的證明方式有甚麼研究的價值
我認為這篇論文的證明方式具有研究價值，而且對你目前考慮的碩論方向 Cycle-Joining Trees on Necklace Orbits 有一定的啟發。

不過，要區分兩件事：

這個證明本身的價值： 它提供了一種理解 FKM Construction 為什麼成功的方式。

這個證明能否衍生新研究： 關鍵不在於重新證明 FKM theorem，而在於能不能將證明中的結構推廣到其他 De Bruijn sequence constructions。

我認為其中最有潛力的，是 Step 3、Step 4 所呈現的「利用相鄰 Lyndon words 的邊界來產生 rotations」這個想法。

一、Step 3 和 Step 4 真正有價值的地方
FKM Construction 是將長度整除 
n
n 的 Lyndon words，依字典序串接：

B=L1L2⋯Lm.B=L1L2⋯Lm.
傳統上，我們知道這樣可以得到 De Bruijn sequence。

但這篇證明關心的是更深入的問題：

為什麼單純把這些 Lyndon words 串在一起，就能讓所有長度為 
n
n 的字串恰好出現一次？

Step 3 和 Step 4 提供了一個很有意思的觀察：

一個 necklace 的 rotations，不一定出現在代表它的 Lyndon word 附近，而可能出現在其他 necklaces 的串接邊界。

例如 
n=4：
B=0⋅0001⋅0011⋅01⋅0111⋅1.
B=0⋅0001⋅0011⋅01⋅0111⋅1.
考慮 necklace

[
0011
]
=
{
0011
,
0110
,
1100
,
1001
}
.
[0011]={0011,0110,1100,1001}.
這四個 rotations 分別出現在不同位置：

Rotation

在 FKM sequence 中的來源

0011
0011

Lyndon word 0011 本身

0110
0110

0011 與 01 的邊界

1001
1001

0001 與 0011 的邊界

1100
1100

整個循環序列的尾端與開頭

這代表 FKM 的正確性不只是 Lyndon words 的排列問題，還涉及不同 necklaces 之間的局部相容性。

而這種相容性，正是可能進一步研究的數學結構。

二、這種證明方式可以往哪些方向推廣？
我整理出四個方向，並根據「數學研究價值」與「兩年碩論的可行性」給出初步評估。

研究方向

核心問題

研究潛力

碩論難度

A. 推廣字典序

改變 Lyndon words 的排列順序，能否仍得到 De Bruijn sequence？

中

中

B. 推廣邊界條件

找出保證所有 rotations 出現的充分條件

中高

中高

C. Restricted necklaces

只選部分 necklaces，能否構造 universal cycle？

中高

中

D. 結合 Cycle Joining

將 Step 3、4 的證明轉換成 spanning tree 的條件

中高

中高

這裡的研究潛力是我對「值得探索的程度」的判斷，不代表這些問題尚未被解決。

方向 A：改變 Lyndon words 的排列方式
FKM 使用字典序：

L
1
<
L
2
<
⋯
<
L
m
.
L 
1
​
 <L 
2
​
 <⋯<L 
m
​
 .
但我們可以問：

是否存在其他排列 
π
π，使得

B
π
=
L
π
(
1
)
L
π
(
2
)
⋯
L
π
(
m
)
B 
π
​
 =L 
π(1)
​
 L 
π(2)
​
 ⋯L 
π(m)
​
 
仍然是 De Bruijn sequence？

Step 3 和 Step 4 可能提供一種研究方式：

Step 3 告訴我們後面的 Lyndon words 必須提供哪些 prefix。

Step 4 告訴我們前面的 Lyndon words 必須提供哪些 suffix。

因此可以研究排列順序需要滿足哪些條件。

例如 
n
=
4
n=4，原本有

B
=
0
⋅
0001
⋅
0011
⋅
01
⋅
0111
⋅
1.
B=0⋅0001⋅0011⋅01⋅0111⋅1.
我們可以嘗試交換其中兩個 Lyndon words，再檢查哪些 rotations 消失、哪些重複。

這個方向的優點是容易從小例子開始。

不過，一般化的 concatenation conditions 已經有相關研究。例如 2018 年的 Constructing de Bruijn Sequences by Concatenating Smaller Universal Cycles，就提出了串接不同 universal cycles 的充分條件，並用來建立新的構造。

sciencedirect.com

因此，單純研究「哪些排列有效」可能不足以形成有新意的碩論；最好找出某一類具有代數或組合結構的排列。

方向 B：將 Step 3、Step 4 抽象成一般定理
這是我覺得最直接繼承該證明思想的方向。

Moreno–Perrin 的證明大量使用字典序中的相鄰 minimal words，來保證所需的 rotations 會出現。

www-igm.univ-mlv.fr

我們可以嘗試不依賴字典序，改問：

給定一組 necklace representatives 與其排列，能不能只檢查某些局部條件，就保證串接結果是 De Bruijn sequence？

例如，對每個 necklace 
[
w
]
[w]，考慮它的所有不同 rotations：

R
(
w
)
=
{
σ
i
(
w
)
:
0
≤
i
<
n
}
.
R(w)={σ 
i
 (w):0≤i<n}.
假設我們能定義一組容易驗證的局部條件 
C
C，使得

C
⟹
每個 
R
(
w
)
 的所有元素都出現在串接序列中
C⟹每個 R(w) 的所有元素都出現在串接序列中
​
 
那麼，由於不同 necklaces 的 rotations 互不重複，再搭配序列長度為 
2
n
2 
n
 ，便能證明結果是 De Bruijn sequence。

這可能形成一個新的充分條件定理。

但要注意，不能只是把「每個 rotation 都出現」重新寫成條件 
C
C。真正有價值的是讓 
C
C 比逐一檢查所有 rotations 更簡單，例如只依賴相鄰 representatives 的 prefix、suffix 或某種偏序關係。

而且必須與既有的 concatenation theorems 比較，確認不是已知結果的改寫。

方向 C：只使用部分 necklaces
這個方向很值得考慮，因為它可以把 FKM theorem 變成更一般的問題。

原本 FKM 使用所有 necklaces：

N
n
=
{
[
w
]
:
w
∈
{
0
,
1
}
n
}
.
N 
n
​
 ={[w]:w∈{0,1} 
n
 }.
但假設我們只選擇其中一部分：

S
⊆
N
n
.
S⊆N 
n
​
 .
令

L
(
S
)
=
{
ℓ
(
[
w
]
)
:
[
w
]
∈
S
}
,
L(S)={ℓ([w]):[w]∈S},
其中 
ℓ
(
[
w
]
)
ℓ([w]) 是 necklace 的 Lyndon representative。

我們希望把這些 Lyndon words 串接後，得到一個循環序列，其中恰好包含選定 necklaces 的全部 rotations。

例如可以限制：

字串中的 1 至少有 
k
k 個。

字串不包含某個禁止的 cyclic pattern。

字串符合某個特定的週期條件。

2016 年 Sawada、Williams、Wong 已研究一大類滿足特定 suffix closure 條件的語言，證明 greedy algorithm 與 necklace concatenation 都能產生其字典序最小的 universal cycle。

combinatorics.org

因此真正可能有研究價值的是：

能否找出不屬於既有充分條件、但仍能利用 Step 3、Step 4 類似方法證明的新字串集合？

這比完全重新建立一套構造理論更容易控制研究範圍。

三、我最在意的是方向 D：能不能連結 Cycle Joining？
這個方向最符合你原本的興趣。

回憶兩種方法：

FKM：透過 Lyndon word concatenation 產生 De Bruijn sequence。

Cycle Joining：將 PCR 產生的 necklace cycles，透過適當的 successor 交換合併。

表面上兩者的操作不同，但最後都在處理同一批長度 
n
n 的字串。

我認為可以考慮以下問題：

Step 3、Step 4 中保證 rotations 出現的邊界條件，是否能轉換為 Cycle-Joining Tree 的結構條件？

例如，FKM 中的某個 rotation

1001
1001
出現在

0001
∣
0011
0001∣0011
的邊界。

我們可以研究這個邊界所反映的關係，是否對應到某種 cycle-joining 操作。

不過，這裡有個重要的數學差別：

串接邊界不一定直接對應 Cycle-Joining Tree 的一條邊。

前者是輸出字串中相鄰片段的關係，後者是 successor rule 在狀態圖中修改連接方式的關係。要建立對應，必須額外證明。

而且這個大方向已經有重大進展。

2026 年的論文 Concatenation Trees: A Framework for Efficient Universal Cycle and de Bruijn Sequence Constructions，已建立 cycle-joining trees 與 concatenation trees 之間的系統性關係，並特別解釋經典 Lyndon word concatenation 與相應 cycle-joining construction 的連結。

sciencedirect.com

所以我不建議把「證明 FKM 可以用 Cycle Joining 表示」當成新的碩論主題。

比較有意思的是：

找出某一類新的 cycle-joining trees。

研究這些 trees 對應的 concatenation order。

嘗試利用 Step 3、Step 4 的想法，給出簡潔的正確性證明。

進一步研究它們是否有特殊性質，例如字典序、有效生成或局部 successor rules。

四、如果以碩論為目標，我會怎麼選？
我最推薦的切入點

Necklace Concatenation 的局部充分條件
研究問題：

對一組指定的 necklaces，是否能利用相鄰 representatives 的 prefix–suffix 結構，建立容易驗證的條件，保證它們的串接形成 universal cycle？

與 Moreno–Perrin 證明的關聯

直接
與你的代數、組合背景

相符
兩年碩論可行性

需縮小範圍
我會建議你先做一個小規模的研究練習：

對 
n
=
4
,
5
,
6
n=4,5,6 列出所有 necklaces 及其 Lyndon representatives。

選擇幾種有規律的排列或 necklace 子集合。

找出哪些串接成功，哪些失敗。

對失敗案例，分析是 Step 3 還是 Step 4 所需的 rotations 沒有出現。

嘗試從成功案例中歸納一個比直接檢查所有 rotations 更簡單的充分條件。

如果能得到一個明確猜想，就有機會進一步發展為定理。

五、最後，我對這篇證明的評價
我會把它的價值分成三個層次：

層次

我的評價

作為 FKM theorem 的另一種證明

有數學價值，但不能單靠這點當成新研究

作為理解 necklace concatenation 的工具

很有價值，尤其是 rotations 與串接邊界的關係

作為新碩論的起點

有潛力，但必須避開已有的 concatenation 與 cycle-joining 一般化定理

另外值得注意的是，2025 年的論文 De Bruijn Sequences: from Games to Shift-Rules to a Proof of the Fredricksen-Kessler-Maiorana Theorem，又提出了利用 shift rules 證明 FKM theorem 的新方法。這表示即使是經典定理，不同證明方式之間的結構關係仍然是研究者關心的問題。

combinatorics.org

我的結論是：Moreno–Perrin 的證明值得你學，但真正有研究價值的不是延長它的技術細節，而是將它的「局部邊界保證全域覆蓋」思想抽象成新的構造定理。

如果是我在你的情況下選題，我會先研究方向 B，再觀察能不能與方向 D 連結。這樣既能延續你正在學的證明，也保留你原本喜歡的 Necklace、Group Actions 和 Cycle-Joining Trees 等離散代數結構。
