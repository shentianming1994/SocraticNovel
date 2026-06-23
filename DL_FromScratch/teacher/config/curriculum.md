# 课程大纲 — 深度学习入门：基于 Python 的理论与实现

> **延迟加载。** 各章教材路径已嵌入对应 `knowledge_points/ch{XX}.md` 头部，本文件仅在需要查看完整课程结构或跨章节路径时读取。

**教材**：《深度学习入门：基于 Python 的理论与实现》（斎藤康毅 著）  
**教材格式**：OCR 转换的 Markdown，已上传至 Claude 会话  
**配套练习册**：无独立练习册——书中各章末的代码实现任务和"小结"即为练习来源  
**实现语言**：Python 3 + NumPy（不使用深度学习框架，全部从零实现）

---

## 课程理念（来自教材）

这本书的核心是"**从零开始**"——不依赖 TensorFlow / PyTorch 等框架，用 NumPy 一行一行实现深度学习的每个组件。教学适配的核心原则：

> **先跑起来看结果，后理解数学原理。**

每个概念都应该先有可运行的代码、可观察的输出，然后再回头理解背后的数学。这与本书"理论与实现"并重的取向一致。

---

## 单元划分与轮值

| 单元 | 章节 | 主题 | 老师 | 情感阶段 |
|------|------|------|------|---------|
| **单元一·基础** | Ch.1–Ch.3 | Python/NumPy → 感知机 → 神经网络前向传播 | 瑠夏 | 初期·距离 → 中期入口 |
| **单元二·学习机制** | Ch.4–Ch.5+AppA | 损失函数与梯度 → 反向传播 → Softmax | 千鶴 | 中期·裂隙 |
| **单元三·工程与深度** | Ch.6–Ch.8 | 训练技巧 → CNN → 深度学习全景 | 墨 | 后期·重力 → 备考期 |

---

## 章节详表与教材路径映射

> 教材路径采用占位符 `materials/textbook/dl_from_scratch.md` 表示已上传的 OCR Markdown 主文件。运行时以会话中实际上传的文件为准；若教材被拆分为多文件，按章节定位对应段落。

| 章 | 标题 | 教材定位 | 核心实现任务 |
|----|------|---------|------------|
| Ch.1 | Python 入门 | `materials/textbook/dl_from_scratch.md` 第1章 | NumPy 数组、广播、matplotlib 基础 |
| Ch.2 | 感知机 | `materials/textbook/dl_from_scratch.md` 第2章 | AND/OR/NAND 门、XOR 与多层感知机 |
| Ch.3 | 神经网络 | `materials/textbook/dl_from_scratch.md` 第3章 | 激活函数、多维数组运算、前向传播、手写数字识别推理 |
| Ch.4 | 神经网络的学习 | `materials/textbook/dl_from_scratch.md` 第4章 | 损失函数、数值微分、梯度、梯度下降、mini-batch 学习 |
| Ch.5 | 误差反向传播法 | `materials/textbook/dl_from_scratch.md` 第5章 | 计算图、链式法则、各层（Affine/ReLU/Sigmoid）的反向传播实现 |
| AppA | Softmax-with-Loss | `materials/textbook/dl_from_scratch.md` 附录A | Softmax 与交叉熵的合并层、数值稳定性 |
| Ch.6 | 与学习相关的技巧 | `materials/textbook/dl_from_scratch.md` 第6章 | 参数更新方法（SGD/Momentum/Adam）、权重初始化、Batch Norm、正则化、Dropout、超参数 |
| Ch.7 | 卷积神经网络 | `materials/textbook/dl_from_scratch.md` 第7章 | 卷积层、池化层、im2col、CNN 实现与可视化 |
| Ch.8 | 深度学习 | `materials/textbook/dl_from_scratch.md` 第8章 | 加深网络、代表性架构、深度学习的应用与前景 |

---

## 教材使用规则

1. **核心知识传递基于教材目录下的主教材。** 讲义 OCR 乱码不可用——遇到公式或图片的 OCR 错误，以文字描述和上下文推断为准。
2. **代码示例是主要实操材料。** 本书的特点是每个概念都有对应的 NumPy 实现，这些代码是教学的核心载体。
3. **教材是地基，不是天花板。** 超纲是鼓励的——更现代的架构（Transformer、扩散模型）、框架的内部原理、论文里的实验故事，都是好的教学素材。回答超纲问题时保持角色性格。
4. **章节顺序可微调，但不跳级。** 反向传播（Ch.5）依赖损失与梯度（Ch.4）；CNN（Ch.7）依赖前面所有内容。AppA 在 Ch.5 之后、Ch.6 之前最自然。

---

## 进度追踪

当前进度见 `teacher/runtime/progress.md`。各章知识点（LO）覆盖状态见 `teacher/config/knowledge_points/ch{XX}.md`。
