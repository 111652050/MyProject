提示詞:能否跟我詳細解釋這篇論文:https://www-igm.univ-mlv.fr/~perrin/Recherche/Publications/Articles/debruijnRevised3.pdf?utm_source=chatgpt.com

這篇論文其實非常適合你目前想研究的方向，因為它研究的是一個很漂亮的組合數學問題：

**為什麼只要把 Lyndon words 按照字典順序串接起來，就能構造出 De Bruijn sequence？**

我們之前已經知道 FKM Construction 的結果，但還沒有真正理解它為什麼成立。這篇論文的目的，就是給出這個定理的嚴格證明。

我會用你熟悉的 Necklaces、Group Actions 和 \\(n=4\\) 的 binary strings 來解釋，並把原文比較抽象的部分拆開。

## **一、這篇論文在研究什麼？**

論文資訊：

- **標題：** *Corrigendum to “On the theorem of Fredricksen and Maiorana about de Bruijn sequences”*
- **作者：** Eduardo Moreno、Dominique Perrin
- **期刊：** *Advances in Applied Mathematics*
- **年份：** 2015
- **頁數：** 184–187
- [閱讀論文 PDF](https://www-igm.univ-mlv.fr/~perrin/Recherche/Publications/Articles/debruijnRevised3.pdf?utm_source=chatgpt.com)

這篇論文修正了 2004 年的一篇證明，補足其中不夠清楚的論證，並且證明 FKM Construction 得到的是字典序最小的 De Bruijn sequence。

[image](https://www.google.com/s2/favicons?domain=https://www.sciencedirect.com\&sz=32)

ScienceDirect



### **論文主要有三個數學結果**

| 結果        | 內容                                       | 重要性      |
| --------- | ---------------------------------------- | -------- |
| Lemma 1   | 相鄰 minimal words 的字典順序性質                 | 主定理證明的工具 |
| Theorem 1 | FKM Construction 一定產生 De Bruijn sequence | 最核心的定理   |
| Theorem 2 | FKM 產生字典序最小的 De Bruijn sequence          | 進一步的性質   |

另外還有一個 Corollary，說明只取某些連續的 Lyndon words，也能構造出 partial De Bruijn sequence。

## **二、先理解論文使用的定義**

這篇論文有幾個容易混淆的名詞。

### **1. Cyclic rotation（循環位移）**

定義：

\\[ \sigma(a_1a_2\cdots a_n) =a_2a_3\cdots a_na_1. \\]

例如：

\\[ w=0011. \\]

它的 rotations 為：

\\[ \begin{aligned} \sigma^0(w)&=0011,\\\ \sigma^1(w)&=0110,\\\ \sigma^2(w)&=1100,\\\ \sigma^3(w)&=1001. \end{aligned} \\]

這四個字串形成一個 necklace。

### **2. Primitive word（非週期字串）**

如果一個長度為 \\(n\\) 的字串具有 \\(n\\) 個不同的 rotations，就稱為 primitive。

例如：

\\[ 0011 \\]

是 primitive，因為它有四個不同的 rotations。

但是

\\[ 0101=(01)^2 \\]

不是 primitive，因為它只有兩個不同的 rotations：

\\[ 0101,\quad1010. \\]

### **3. Minimal word（最小代表元）**

如果一個字串是自己所有 rotations 當中字典序最小的，就稱為 minimal word。

例如：

\\[ 0011 \\]

是 minimal，因為

\\[ 0011<0110<1001<1100. \\]

但是 `0101` 也是 minimal，因為

\\[ 0101<1010. \\]

注意，minimal word 不一定是 primitive。

### **4. Lyndon word**

一個字串同時是：

- Primitive
- Minimal

就稱為 Lyndon word。

因此：

| 字串   | Minimal | Primitive | Lyndon |
| ---- | ------- | --------- | ------ |
| 0000 |         |           |        |
| 0001 |         |           |        |
| 0011 |         |           |        |
| 0101 |         |           |        |
| 0111 |         |           |        |
| 1010 |         |           |        |

**這三個定義的差別非常重要，因為論文的證明主要處理 minimal words，而 FKM Construction 串接的是 Lyndon words。**

## **三、Theorem 1：為什麼 FKM Construction 正確？**

先寫出論文的主定理。

令

\\[ L_n=\\{w:w\text{ 是 Lyndon word，且 }|w|\mid n\\}. \\]

將其中的字串依照字典順序排列並串接：

\\[ B=\operatorname{Concat}\_{\mathrm{lex}}(L_n). \\]

則

\\[ \boxed{B\text{ 是 order }n\text{ 的 De Bruijn sequence}.} \\]

### **以&#x20;**\\(n=4\\)**&#x20;為例**

所有符合條件的 Lyndon words 為：

\\[ 0,\quad0001,\quad0011,\quad01,\quad0111,\quad1. \\]

所以

\\[ \begin{aligned} B &=0\cdot0001\cdot0011\cdot01\cdot0111\cdot1\\\ &=\boxed{0000100110101111}. \end{aligned} \\]

長度剛好是

\\[ 1+4+4+2+4+1=16=2^4. \\]

接下來我們要證明的不是只有長度正確，而是這 16 個位置恰好對應 16 種不同的 4-bit strings。

### **論文採用的核心策略**

它先把問題轉換成：

> 對每一個長度為 \\(n\\) 的 minimal word \\(w\\)，證明 \\(w\\) 的所有 rotations 都能在串接結果中找到。

例如考慮

\\[ w=0011. \\]

我們必須找到：

\\[ 0011,\quad0110,\quad1100,\quad1001. \\]

這些字串不一定都出現在 `0011` 這個 Lyndon word 內。

它們可能跨越其他 Lyndon words 的邊界。

以下是實際的位置：

FKM(4) 的 Lyndon word 分段

0

0001

0011

01

0111

1

0011 所屬 necklace 的四個 rotations

| 0011 | 第 6–9 位  |
| ---- | -------- |
| 0110 | 第 8–11 位 |
| 1100 | 第 9–12 位 |
| 1001 | 第 5–8 位  |

你會發現，這四個 rotations 全部都能在串接序列中找到。

但它們不一定集中在同一個 Lyndon word 附近。

這正是這篇論文要處理的技術困難。

## **四、Lemma 1：整篇論文最重要的技術工具**

接下來進入論文第一頁的 Lemma 1。

我先用白話說明它的意思。

### **1. Lemma 1 想告訴我們什麼？**

考慮所有長度為 \\(n\\) 的 minimal words，並按照字典順序排列。

例如 \\(n=4\\)：

\\[ 0000<0001<0011<0101<0111<1111. \\]

假設我們指定一個 prefix \\(w\\)，然後去找：

- \\(v\\)：以 \\(w\\) 開頭的最小 minimal word。
- \\(u\\)：在字典順序中，緊接在 \\(v\\) 前面的 minimal word。

Lemma 1 告訴我們，在適當條件下，\\(u\\)**&#x20;的尾端一定會是一串最大的字母。**

對 binary alphabet 而言，最大的字母就是 1。

這個性質讓我們能夠在 Lyndon words 串接的邊界，找到某些以連續的 1 開頭的 rotations。

### **2. 用&#x20;**\\(n=4\\)**&#x20;示範**

假設指定 prefix：

\\[ w=01. \\]

它的長度是 2，所以

\\[ n-|w|=2. \\]

在所有 minimal words 中，以 `01` 開頭且字典序最小的是：

\\[ v=0101. \\]

而在 \\(v\\) 前面緊接的 minimal word 是：

\\[ u=0011. \\]

觀察：

\\[ \boxed{u=00\underbrace{11}\_{2\text{ 個 }1}}. \\]

正如 Lemma 1 所說，\\(u\\) 的最後兩個 bits 都是 1。

再看另一個例子，指定 prefix：

\\[ w=001. \\]

這次：

\\[ n-|w|=1. \\]

以 `001` 開頭的最小 minimal word 為：

\\[ v=0011. \\]

它前面緊接的 minimal word 是：

\\[ u=0001. \\]

而

\\[ u=000\underbrace{1}\_{1\text{ 個 }1}. \\]

也符合引理。

### **3. Lemma 1 的正式敘述**

對有序 alphabet \\(A\\)，令 \\(z\\) 為最大的字母。

設 \\(w\\) 是某個長度為 \\(n\\) 的 minimal word 的 prefix，且

\\[ |w|=n-i,\qquad i>0. \\]

在引理所需的非退化條件下，令：

- \\(v\\) 為以 \\(w\\) 開頭的最小 minimal word；
- \\(u\\) 為小於 \\(v\\) 的最大 minimal word。

則

\\[ \boxed{u\text{ 的最後 }i\text{ 個字母都是 }z.} \\]

也就是：

\\[ u=u_1u_2\cdots u\_{n-i}z^i. \\]

### **4. 為什麼成立？**

這個證明使用反證法。

假設 \\(u\\) 的最後 \\(i\\) 個字母並不全部是 \\(z\\)。

現在構造一個新的字串：

\\[ u'=u_1u_2\cdots u\_{n-i}z^i. \\]

也就是保留 \\(u\\) 的前 \\(n-i\\) 個字母，把剩下的全部換成最大的字母。

因為原本 \\(u\\) 的尾端不全是 \\(z\\)，所以

\\[ u\<u'. \\]

另一方面，由於 \\(u\<v\\)，而 \\(v\\) 具有 prefix \\(w\\)，可以得到

\\[ u_1\cdots u\_{n-i}\<w. \\]

因此

\\[ u'\<v. \\]

合併得到：

\\[ \boxed{u\<u'\<v}. \\]

接下來使用 minimal words 的一個性質：

如果 \\(u\\) 是 minimal word，把其尾端某些字母改成最大字母，得到的 \\(u'\\) 在這個構造下仍是 minimal word。

於是 \\(u'\\) 是一個新的 minimal word，且滿足

\\[ u\<u'\<v. \\]

但我們原本定義 \\(u\\) 是小於 \\(v\\) 的最大 minimal word。

這就產生矛盾！

因此 \\(u\\) 的最後 \\(i\\) 個字母必定都是 \\(z\\)。

\\[ \boxed{u\text{ ends with }z^i.} \\]

這就是 Lemma 1 背後的想法。

這裡最需要留意的是「改寫尾端後仍為 minimal」這個性質；它仰賴 minimal word 與 cyclic rotations 的特殊關係，不能任意套用在一般字串上。

## **五、正式證明 Theorem 1：所有 rotations 為什麼都會出現？**

這是論文最重要的部分。

### **Step 1：選擇任意 minimal word**

令 \\(w\\) 是長度為 \\(n\\) 的 minimal word。

對 binary alphabet，可以把它寫成

\\[ w=w_1w_2\cdots w_j1^{n-j}, \\]

其中 \\(w_j=0\\)（先排除全 1 的特殊情況）。

也就是將字串分成兩部分：

\\[ \boxed{w=\underbrace{w_1\cdots w_j}\_{\text{前半段}} \underbrace{11\cdots1}\_{\text{尾端連續的 1}}}. \\]

例如：

\\[ w=00111. \\]

我們可以取

\\[ j=2,\qquad n-j=3. \\]

所以

\\[ w=\underbrace{00}\_{j=2}\underbrace{111}\_{n-j=3}. \\]

### **Step 2：將 rotations 分成兩類**

對 \\(w=00111\\)，所有 rotations 為：

\\[ \begin{aligned} \sigma^0(w)&=00111,\\\ \sigma^1(w)&=01110,\\\ \sigma^2(w)&=11100,\\\ \sigma^3(w)&=11001,\\\ \sigma^4(w)&=10011. \end{aligned} \\]

論文將它們分為：

第一類：從前半段開始

\\[ 00111,\quad01110 \\]

對應 \\(0\le i\<j\\)，共有 \\(j=2\\) 個 rotations。

第二類：從尾端的 1 開始

\\[ 11100,\quad11001,\quad10011 \\]

對應 \\(j\le i\<n\\)，共有 \\(n-j=3\\) 個 rotations。

接下來只要分別證明這兩組都會出現在 FKM sequence 中，就完成了。

### **Step 3：證明第一類 rotations 會出現**

先假設 \\(w\\) 本身是 Lyndon word，也就是 primitive minimal word。

令 \\(x\\) 為字典順序中緊接在 \\(w\\) 後面的長度 \\(n\\) minimal word。

因為 \\(w\\) 的尾端有 \\(n-j\\) 個 1，而字母 1 已經不能再增加，所以下一個 minimal word 必須在更前面的位置，將某個較小的字母增加。

在二元情況下，這代表將某個 0 變成 1。

例如 \\(n=4\\)：

\\[ w=0011. \\]

下一個 minimal word 是

\\[ x=0101. \\]

注意它們有共同的第一個 bit：

\\[ w=\underbrace{0}\_{\text{共同}}011, \qquad x=\underbrace{0}\_{\text{共同}}101. \\]

因此，當這兩個字串出現在適當的串接結構時，從 \\(w\\) 開始、跨越邊界的 windows，就有機會產生 \\(w\\) 的 rotations。

真正的證明還必須區分 \\(x\\) 是否 primitive。

- 如果 \\(x\\) 是 primitive，則 \\(x\\) 本身是 Lyndon word。
- 如果 \\(x\\) 不是 primitive，則要改用它的 primitive root \\(\widehat{x}\\)，以及後續的 Lyndon word，建立所需的連續字串。

這個區分很重要，因為 FKM 並沒有直接串接所有 minimal words。

它只串接 Lyndon words。

例如

\\[ 0101 \\]

是 minimal，但不是 Lyndon word。

它的 primitive root 是

\\[ \widehat{x}=01. \\]

所以實際參與 FKM 串接的是 `01`，而不是 `0101`。

論文的這一段，就是處理「minimal word 的相鄰關係」與「實際 Lyndon word 串接」之間的差異。

對非 primitive 的 \\(w\\)，作者同樣改從它的 primitive root 出發，證明所需的 rotations 可以在相鄰的 Lyndon words 中找到。

### **Step 4：證明第二類 rotations 會出現**

這裡就需要 Lemma 1。

第二類 rotations 的形式是

\\[ \boxed{ 1^iw_1\cdots w_j1^{n-j-i}, \qquad 1\le i\le n-j. } \\]

例如 \\(w=00111\\)，取 \\(i=2\\)，就得到

\\[ 11001. \\]

我們希望找到某個 Lyndon word 串接邊界，使它的左側提供

\\[ 11, \\]

右側提供

\\[ 001. \\]

這樣跨越邊界的長度 5 window 就會是

\\[ \underbrace{11}\_{\text{左側}} \underbrace{001}\_{\text{右側}} =11001. \\]

Lemma 1 的用途就在這裡。

它讓我們知道，在適當的字典順序位置，前一個 minimal word 的尾端必定有足夠多的 1。

因此可以用這個尾端，接上後面 Lyndon word 所提供的 prefix，產生需要的 rotation。

當前一個 minimal word 並非 primitive 時，還要進一步追蹤它的 primitive root，才能確定這段尾端真的會出現在 FKM 的串接結果中。

對於跨越整個序列終點與起點的情形，則另外利用 FKM sequence 的最後一段全 1 與最前面一段全 0 來處理。

### **Step 5：完成證明**

經過前面兩部分：

- 第一類 rotations 會出現。
- 第二類 rotations 也會出現。

所以每個 minimal word \\(w\\) 的所有 rotations 都會出現在 \\(B\\) 中。

而每個長度為 \\(n\\) 的字串都屬於某個 minimal word 的 necklace。

因此

\\[ \boxed{\text{所有長度為 }n\text{ 的字串都出現在 }B.} \\]

最後再利用

\\[ |B|=k^n \\]

便得到每種長度 \\(n\\) 的字串都恰好出現一次。

這樣就完成了 FKM theorem 的證明。

需要坦白說明：上面是將論文證明拆解後的主要邏輯。要做到逐行的完全形式化證明，還需要補齊相鄰 Lyndon words 的精確字串等式，尤其是非 primitive 的情況；不能只靠「有機會跨越邊界」就視為證明完成。

## **六、Corollary 1：只串接部分 Lyndon words 也有特殊性質**

這是我認為對你碩論方向很有研究價值的一個結果。

假設所有符合條件的 Lyndon words 依字典順序為

\\[ \ell_1<\ell_2<\cdots<\ell_m. \\]

一般 FKM Construction 使用全部：

\\[ B=\ell_1\ell_2\cdots\ell_m. \\]

但論文發現，如果我們從中間某個位置開始，取到最後：

\\[ \boxed{B_s=\ell_s\ell\_{s+1}\cdots\ell_m,} \\]

這個序列仍然具有特殊性質。

它是一個 *partial De Bruijn sequence*。

### **什麼是 Partial De Bruijn Sequence？**

在這篇論文中，partial De Bruijn sequence of span \\(n\\) 指的是一個循環序列，滿足：

1. 所有長度為 \\(n\\) 的 cyclic substrings 互不重複。
2. 這些 substrings 的集合對 cyclic rotation 封閉。

第二點很重要。

例如，如果包含

\\[ 0011, \\]

就必須同時包含

\\[ 0110,\quad1100,\quad1001. \\]

也就是包含整個 necklace。

### **以&#x20;**\\(n=4\\)**&#x20;為例**

原本的 Lyndon words 是

\\[ 0,\quad0001,\quad0011,\quad01,\quad0111,\quad1. \\]

現在只取最後四個：

\\[ 0011,\quad01,\quad0111,\quad1. \\]

得到

\\[ \boxed{B'=00110101111}. \\]

這是一個長度 11 的循環序列。

檢查其 4-bit cyclic substrings：

| Necklace   | 出現的 rotations       |
| ---------- | ------------------- |
| \\(0011\\) | 0011、0110、1100、1001 |
| \\(01\\)   | 0101、1010           |
| \\(0111\\) | 0111、1110、1101、1011 |
| \\(1\\)    | 1111                |

這些字串一共有

\\[ 4+2+4+1=11 \\]

種，而且全部互不重複。

因此 \\(B'\\) 是 partial De Bruijn sequence。

這件事相當有趣，因為它表示：

**FKM 的字典順序不只能正確串接全部 necklaces，也能讓某些 necklaces 的子集合形成合法的循環序列。**

## **七、Theorem 2：為什麼 FKM 得到字典序最小的 De Bruijn sequence？**

這是論文最後一個結果。

我們已經知道：

\\[ B=0000100110101111 \\]

是 order 4 的 De Bruijn sequence。

但是 order 4 的 binary De Bruijn sequence 並不只有這一個。

例如：

\\[ B'=0000111101100101 \\]

也是合法的。

比較兩者：

\\[ \begin{aligned} B&=0000100110101111,\\\ B'&=0000111101100101. \end{aligned} \\]

在第一個不同的位置，\\(B\\) 的 bit 是 0，而 \\(B'\\) 的 bit 是 1。

所以

\\[ B\<B'. \\]

Theorem 2 證明，這不是巧合。

對任意 \\(n\\)，FKM Construction 得到的都是字典序最小的 De Bruijn sequence（將循環序列以其字典序最小的 rotation 表示）。

### **論文的證明想法**

作者使用反證法。

假設存在一個比 FKM sequence \\(B\\) 更小的 De Bruijn sequence \\(B'\\)。

考慮兩者第一次出現不同的地方。

假設它們在此之前的共同部分為 \\(w\\)，下一個字母分別為

\\[ a\<b, \\]

其中 \\(B'\\) 選擇 \\(a\\)，而 \\(B\\) 選擇 \\(b\\)。

因此：

\\[ wa\<wb. \\]

現在將 \\(wa\\) 和 \\(wb\\) 各自對應到所屬 necklace 的 minimal representative。

記為

\\[ M(wa),\qquad M(wb). \\]

可以證明：

\\[ \boxed{M(wa)\<M(wb).} \\]

另一方面，利用前面的 Corollary 1，可以推導出 FKM sequence 中與這兩個 necklaces 相關的出現順序。

這會與「\\(B'\\) 在第一次分歧時可以選擇更小字母」的假設矛盾。

因此不存在比 \\(B\\) 更小的 De Bruijn sequence。

這裡的細節依賴 Corollary 1，所以不是單純由「Lyndon words 按字典序排列」就能立即推出的。

## **八、整篇論文的數學架構**

\#chatgpt-mermaid-\_r_1bp\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_1bp\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_1bp\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_1bp\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_1bp\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_1bp\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_1bp\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_1bp\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_1bp\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_1bp\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_1bp\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_1bp\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_1bp\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_1bp\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_1bp\_ p{margin:0;}#chatgpt-mermaid-\_r_1bp\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_1bp\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_1bp\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_1bp\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_1bp\_ .label text,#chatgpt-mermaid-\_r_1bp\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_1bp\_ .node rect,#chatgpt-mermaid-\_r_1bp\_ .node circle,#chatgpt-mermaid-\_r_1bp\_ .node ellipse,#chatgpt-mermaid-\_r_1bp\_ .node polygon,#chatgpt-mermaid-\_r_1bp\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_1bp\_ .rough-node .label text,#chatgpt-mermaid-\_r_1bp\_ .node .label text,#chatgpt-mermaid-\_r_1bp\_ .image-shape .label,#chatgpt-mermaid-\_r_1bp\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_1bp\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_1bp\_ .rough-node .label,#chatgpt-mermaid-\_r_1bp\_ .node .label,#chatgpt-mermaid-\_r_1bp\_ .image-shape .label,#chatgpt-mermaid-\_r_1bp\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_1bp\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_1bp\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_1bp\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_1bp\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_1bp\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_1bp\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_1bp\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_1bp\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_1bp\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_1bp\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_1bp\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_1bp\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_1bp\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_1bp\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_1bp\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_1bp\_ .icon-shape,#chatgpt-mermaid-\_r_1bp\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_1bp\_ .icon-shape p,#chatgpt-mermaid-\_r_1bp\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_1bp\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_1bp\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_1bp\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_1bp\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_1bp\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_1bp\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_1bp\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_1bp\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_1bp\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_1bp\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_1bp\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_1bp\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_1bp\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_1bp\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_1bp\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_1bp\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_1bp\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_1bp\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_1bp\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_1bp\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_1bp\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_1bp\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_1bp\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_1bp\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_1bp\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_1bp\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_1bp\_ .node rect,#chatgpt-mermaid-\_r_1bp\_ .node circle,#chatgpt-mermaid-\_r_1bp\_ .node ellipse,#chatgpt-mermaid-\_r_1bp\_ .node polygon,#chatgpt-mermaid-\_r_1bp\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_1bp\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_1bp\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_1bp\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_1bp\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_1bp\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Lyndon words 與 minimalwordsLemma 1相鄰 minimal words的尾端性質Theorem 1所有 rotations 都會出現FKM 產生 De Bruijn sequenceCorollary 1尾段串接形成 partial DBTheorem 2FKM 是字典序最小的 DB

這篇文章的主要貢獻是證明已有的 FKM 定理、修正早期證明的細節，以及建立字典序最小性；它並不是提出一種全新的 De Bruijn construction。

## **九、對你的碩論研究有什麼啟發？**

你原本想研究的是：

*Cycle-Joining Trees on Necklace Orbits*

我認為這篇論文有三個值得你特別思考的地方。

**第一，FKM Construction 與 Cycle Joining 都利用 necklace decomposition。**

Cycle Joining 透過交換 successors，把不同 necklaces 對應的小 cycles 合併。

FKM 則利用 Lyndon words 的字典順序，直接完成串接。

它們背後是否能用統一的 tree structure 描述，是很自然的研究問題。

**第二，字典順序是 FKM Construction 成功的關鍵。**

如果換成其他 ordering，未必還能得到 De Bruijn sequence。

因此可以問：

> 除了 lexicographic order，還有哪些 necklace orderings 可以保證串接後得到 De Bruijn sequence？

不過這類問題已經有不少後續研究，若要當作論文題目，需要先確認既有結果。

**第三，Corollary 1 表示部分 necklaces 的串接也能保有完整的 orbit 結構。**

這讓我們可以考慮：

> 對一組指定的 necklaces，什麼條件能保證它們的 Lyndon representatives 可以串接成 partial De Bruijn sequence？

這與 restricted universal cycles、concatenation trees 等研究方向都有關係。

### **我建議你的下一個學習重點**

如果希望真正看懂這篇論文的證明，我最推薦先專攻 **Lemma 1 如何被用在 Theorem 1 的第二類 rotations**。

因為第一類 rotations 主要運用字典序中下一個 Lyndon word 的結構；第二類則要反過來利用前面的字串結構，這也是作者需要 Lemma 1 的原因。

只要掌握這兩種 rotations 分別如何跨越 Lyndon word 的邊界，就能理解 FKM Construction 最核心的證明思想。
