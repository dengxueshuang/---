
# 虚假新闻检测项目

本项目使用 LightGBM 对新闻文本向量 (Word2Vec) 特征进行多分类，旨在检测新闻真伪，并通过多种可视化图表展示数据分布和模型效果。运行脚本后，控制台将输出模型的 MSE、Accuracy 和详细分类报告，并弹出归一化后的混淆矩阵热力图，帮助直观评估模型性能。

---

## 目录

- [项目简介](#项目简介)  
- [环境依赖](#环境依赖)  
- [数据说明](#数据说明)  
- [快速开始](#快速开始)  
- [代码结构](#代码结构)  
- [模型训练](#模型训练)  
- [可视化结果](#可视化结果)  
- [License](#license)  

---

## 项目简介

本项目通过读取预先计算好的 Word2Vec 特征向量，对新闻文本进行三分类——真 (real)、假 (fake) 及无需判断 (unknown)。采用 LightGBM 进行模型训练，结合 Python 常用数据分析与可视化库，实现从数据加载、模型训练、结果评估到图表呈现的完整流程。你可以通过命令行快速运行脚本，也可以将生成的混淆矩阵嵌入 Web 页面，借助 ECharts 实现交互式展示。

---

## 环境依赖

在开始使用前，请确保本地已安装以下依赖包：

```bash
pip install pandas numpy scikit-learn lightgbm matplotlib seaborn
````

以上工具将用于数据处理、模型训练与结果可视化。若需将图表嵌入网页，还可额外安装 `pyecharts`：

```bash
pip install pyecharts jupyter
```

---

## 数据说明

本项目自带训练数据文件 `data_wordvec_train.csv`，格式为 CSV，共 51 列：

* **前 50 列** ：Word2Vec 特征向量（浮点数），代表每条新闻的文本表示。
* **最后一列 `label`**：三分类标签

  * `0`：无需判断 (unknown)
  * `1`：假新闻 (fake)
  * `2`：真新闻 (real)

请务必将此文件放置于项目根目录，以保证脚本能够正确加载并训练模型。

---

## 快速开始

1. 克隆或下载本项目到本地：

   ```bash
   git clone https://github.com/your-username/fake-news-detection.git
   cd fake-news-detection
   ```
2. 将 `data_wordvec_train.csv` 放入项目根目录。
3. 安装 Python 依赖：

   ```bash
   pip install -r requirements.txt
   ```
4. 运行训练与可视化脚本：

   ```bash
   python train_and_visualize.py
   ```

   脚本执行完成后，将在控制台打印 MSE、Accuracy 和分类报告，并弹出一幅归一化混淆矩阵的热力图窗口。

---

## 代码结构

```text
.
├── data_wordvec_train.csv    # 训练数据，前 50 列为特征，最后一列为标签
├── train_and_visualize.py    # 模型训练与可视化脚本
├── requirements.txt          # 依赖列表
└── README.md                 # 项目说明（本文件）
```

其中，`train_and_visualize.py` 包含从数据加载、训练集划分、LightGBM 训练、评估指标计算到混淆矩阵可视化的完整逻辑。

---

## 模型训练

在 `train_and_visualize.py` 中，核心流程如下：

1. **加载数据**：使用 `pandas.read_csv` 读取 `data_wordvec_train.csv`。
2. **特征与标签分离**：将前 50 列作为特征矩阵 `X`，`label` 列作为目标向量 `y`。
3. **划分训练/测试集**：按 70/30 的比例随机划分，设置 `random_state=45` 保证可复现。
4. **构建 LightGBM 分类器**：设置 `feature_fraction=0.8, learning_rate=0.1, max_depth=2, num_leaves=10` 等超参。
5. **模型训练与预测**：调用 `fit` 方法进行训练，再对测试集预测。
6. **评估指标**：计算 MSE、Accuracy，并打印分类报告（Precision/Recall/F1-Score）。
7. **可视化混淆矩阵**：归一化后使用 Seaborn 绘制热力图，标注百分比。

---
## 可视化结果

脚本运行结束后，会生成并展示归一化后的混淆矩阵热力图，以直观呈现模型在三分类任务上的预测效果：

![Normalized Confusion Matrix](images/confusion_matrix.png)

如果需要在网页中展示，也可以参考以下 ECharts 模板……
