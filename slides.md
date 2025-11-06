---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: GLAD & GOLD Research Papers
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply UnoCSS classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# duration of the presentation
duration: 35min
---

# GLAD & GOLD Research Papers

刘元铭<br><br>2025.11.6

<div @click="$slidev.nav.next" class="mt-12 py-1" hover:bg="white op-10">
  Contents <carbon:arrow-right />
</div>

<div class="abs-br m-6 text-xl">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="slidev-icon-btn">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->


---
transition: fade-out
---

# CVTGAD: Simplified Transformer with Cross-View Attention for Unsupervised Graph-level Anomaly Detection

ECML PKDD'2023/CVTGAD

📝 Keywords:

* Graph-level Anomaly Detection; Contrastive Learning


<img
  class="absolute bottom-5 left-50 w-150 "
  src="/1-1.png"
  alt=""
/>

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>




---
transition: fade-out
---

# Motivations & Challenges

CVTGAD: Simplified Transformer with Cross-View Attention for Unsupervised Graph-level Anomaly Detection

#### Challenges 1

现有方法严重依赖 GNN 来提取图的特征，GNN 的感受野 (Receptive Field) 有限

主要关注节点的局部信息

* 忽略全局结构模式（intra-graph）
* 忽略图与图之间的关系 (inter-graph)

直觉方法：

* 堆叠更多 GNN 层? (Over-smoothing)

<img
  class="absolute bottom-5 right-10 w-130 "
  src="/1-2.png"
  alt=""
/>



<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>



---
transition: fade-out
---

# Motivations & Challenges

CVTGAD: Simplified Transformer with Cross-View Attention for Unsupervised Graph-level Anomaly Detection

#### Challenges 2

现有方法常用数据增强来构建多个视图 (e.g., 特征视图, 结构视图)。

但处理方式是<span v-mark.circle.orange="1">“并行且分离” (parallel and separate) </span>的。

* 各自处理不同视图
* 整个过程中它们**互不通信**
* 直到最后一步才计算一致性

<div
  class="absolute bottom-30 left-15 w-75"
>
  这种方式<b>无法直接探索</b>不同视图之间的相互关系，进而忽略了关键的<b>“视图共现性”</b>
</div>

<img
  class="absolute bottom-0 right-10 w-130"
  src="/1-2.png"
  alt=""
/>

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>




---
transition: fade-out
---

# Motivations & Challenges

CVTGAD: Simplified Transformer with Cross-View Attention for Unsupervised Graph-level Anomaly Detection

#### view co-occurrence

图的特征和结构是<span v-mark.red="1">相互影响、相互纠缠</span>的。

<div
  class="absolute top-50 left-15 w-80"
>
  <ul>
  <li>特征 &rarr; 结构：具有特定特征的节点，更容易形成异常的链接</li>
  <li>结构 &rarr; 特征: 被异常链接所连接的节点，其特征也可能随之改变。</li>
  </ul>

<br>

现有方法是<b>“先分离、后对比”</b>

丢失了过程中<b>“共现”</b>的异常信号。
</div>


<img
  class="absolute bottom-10 right-10 w-130 "
  src="/1-2.png"
  alt=""
/>

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>


---
transition: fade-out
---

# Contributions

CVTGAD: Simplified Transformer with Cross-View Attention for Unsupervised Graph-level Anomaly Detection

 针对挑战提出两个核心模块

**Challenge 1 (感受野受限):**

* 采用一个 <span v-mark.blue="1">Simplified Transformer</span>

$\rightarrow$ 利用 Transformer 的自注意力机制，获得**全局感受野**，捕捉图内和图间的复杂关系（intra and inter）

**Challenge 2 (视图分离处理):**

* 设计一种 <span v-mark.red="1">跨视图注意力 (Cross-View Attention)</span>

$\rightarrow$ 直接捕获视图间的“共现性”，**显式地在编码过程中桥接不同视图的鸿沟**

<span v-mark.circle.orange="1">首次将 Transformer 和 跨视图注意力 引入 UGAD 任务。</span>


<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>


---
transition: fade-out
---

# Methodology

CVTGAD: Simplified Transformer with Cross-View Attention for Unsupervised Graph-level Anomaly Detection

基本框架

<img
  class="absolute bottom-25 left-65 w-120 "
  src="/1-3.png"
  alt=""
/>

<img
  class="absolute bottom-5 left-60 w-130 "
  src="/1-5.png"
  alt=""
/>

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>



---
transition: fade-out
---

# Methodology

CVTGAD: Simplified Transformer with Cross-View Attention for Unsupervised Graph-level Anomaly Detection

Transformer 细节

<img
  class="absolute bottom-30 left-55 w-140 "
  src="/1-4.png"
  alt=""
/>

<img
  class="absolute bottom-5 left-60 w-130 "
  src="/1-5.png"
  alt=""
/>

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>


---
transition: fade-out
---

# Methodology

CVTGAD: Simplified Transformer with Cross-View Attention for Unsupervised Graph-level Anomaly Detection

**1.Graph Pre-processing Module**

<br>
<br>

<span v-mark.red="1">使用无扰动数据增强</span>得到**特征视图和结构视图**

* 使用 GNN（如 GIN, GCN）作为 encoder
* 然后做典中典 **READOUT**，获得图 Embedding

特征和结构计算方式一样，这里只给出特征的计算


<img
  class="absolute top-40 right-10 w-120 "
  src="/1-6.png"
  alt=""
/>

<img
  class="absolute top-70 right-10 w-120 "
  src="/1-7.png"
  alt=""
/>


<img
  class="absolute bottom-30 right-10 w-120 "
  src="/1-8.png"
  alt=""
/>


<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>



---
transition: fade-out
---

# Methodology

CVTGAD: Simplified Transformer with Cross-View Attention for Unsupervised Graph-level Anomaly Detection

**2.Simplified Transformer-based Embedding Module**

<br>

将两个视图的**初步嵌入**<span v-mark.circle.blue="1">输入</span>到该模块
* Simplified Transformer 负责**扩大感受野**
* Cross-View Attention 负责**视图共现**

<br>

<span v-mark.circle.blue="1">输出</span>融合了**全局信息**和**跨视图信息**的最终嵌入
* intra 全局信息：靠 self-attention
* inter 全局信息：<span v-mark.red="1">考虑一个batch $\mathcal{B}$中的样本</span>
* Cross-View Attention 本质上是一种 self-attention

<img
  class="absolute top-40 right-10 w-120 "
  src="/1-9.png"
  alt=""
/>

<img
  class="absolute top-60 right-10 w-120 "
  src="/1-10.png"
  alt=""
/>


<img
  class="absolute bottom-40 right-10 w-120 "
  src="/1-11.png"
  alt=""
/>


<img
  class="absolute bottom-20 right-10 w-120 "
  src="/1-12.png"
  alt=""
/>

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>


---
transition: fade-out
---

# Methodology

CVTGAD: Simplified Transformer with Cross-View Attention for Unsupervised Graph-level Anomaly Detection

**3.Adaptive Anomaly Scoring Module**

<img
  class="absolute top-50 left-5 w-110 "
  src="/1-13.png"
  alt=""
/>

<img
  class="absolute bottom-20 left-5 w-110 "
  src="/1-14.png"
  alt=""
/>

<img
  class="absolute bottom-20 right-0 w-130 "
  src="/1-15.png"
  alt=""
/>


<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>


---
layout: center
class: text-center
---

# Thanks

刘元铭<br>2025.11.6

<PoweredBySlidev mt-10 />
