### 3.1 多尺度自适应图卷积（MAGC）

为同时捕获短时与长时片段中人体关节的跨空间依赖关系，本文提出多尺度自适应图卷积（MAGC）模块，其整体结构如图 2 所示。设上一时序模块输出特征为 $X \in \mathbb{R}^{C_{\text{in}} \times T \times N}$，其中 $C_{\text{in}}$、$T$、$N$ 分别表示通道数、时间步与关节数。我们沿通道维将 $X$ 均匀划分为 $g$ 个子张量：$X = \bigl(X^{(1)}, X^{(2)}, \dots, X^{(g)}\bigr)$，其中 $X^{(i)} \in \mathbb{R}^{\tfrac{C_{\text{in}}}{g} \times T \times N}$。这一分组策略引入了多尺度建模能力，同时显著降低了参数量与计算复杂度。

对于每个尺度 $i$，我们首先对 $X^{(i)}$ 进行变换，提取高阶特征 $\tilde{X}^{(i)} \in \mathbb{R}^{C' \times T \times N}$。随后构建通道特定的邻接矩阵 $D^{(i)}$，其由固定骨架先验 $A \in \mathbb{R}^{N \times N}$ 与自适应相关矩阵 $Q^{(i)}$ 融合而成，表示为：

$$
D^{(i)} = A + \alpha Q^{(i)},
$$

其中 $\alpha$ 为可学习的融合系数。$Q^{(i)}$ 是根据输入特征动态生成的，具体地，通过差分相似性函数 $\mathcal{M}$，对任意两个关节 $a$ 和 $b$ 的变换特征进行建模：

$$
\mathcal{M}\bigl(\varphi(X^{(i)}_a), \psi(X^{(i)}_b)\bigr) = \sigma\bigl(\varphi(X^{(i)}_a) - \psi(X^{(i)}_b)\bigr),
$$

其中 $\varphi(\cdot)$ 和 $\psi(\cdot)$ 表示线性变换与时序池化操作，$\sigma(\cdot)$ 为激活函数，最终通过映射函数 $\varepsilon(\cdot)$ 将相似性结果投影至固定维度，生成 $Q^{(i)}$。

获得邻接矩阵 $D^{(i)}$ 后，利用图卷积函数 $\mathcal{G}$ 执行空间聚合：

$$
z^{(i)} = \mathcal{G}(D^{(i)}, \tilde{X}^{(i)}),
$$

最终将各尺度分支的输出在通道维拼接，得到融合后的图特征表示：

$$
Z = \bigl[z^{(1)} \Vert z^{(2)} \Vert \cdots \Vert z^{(g)}\bigr].
$$

MAGC 模块通过尺度独立的图结构建模，在捕获多尺度语义依赖的同时，有效减少了跨分支的冗余计算与参数开销。
