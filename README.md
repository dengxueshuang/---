# 虚假新闻检测项目

本项目使用 LightGBM 对新闻文本向量 (Word2Vec) 特征进行多分类，旨在检测新闻真伪，并通过可视化展示模型效果。

---

## 目录

- [项目简介](#项目简介)  
- [环境依赖](#环境依赖)  
- [数据说明](#数据说明)  
- [快速开始](#快速开始)  
- [项目结构](#项目结构)  
- [可视化展示](#可视化展示)  
- [License](#license)  

---

## 项目简介

- **任务**：基于训练集中的新闻文本向量特征，构建 LightGBM 多分类模型，判断新闻是真 (real)、假 (fake) 还是无需判断 (unknown)。  
- **技术栈**：Python 3.8、Pandas、NumPy、Scikit-Learn、LightGBM、Matplotlib、Seaborn。  
- **输出**：控制台打印 MSE、Accuracy、Classification Report，并弹出归一化混淆矩阵热力图。  

---

## 环境依赖

请确保已安装以下 Python 包：

```bash
pip install pandas numpy scikit-learn lightgbm matplotlib seaborn
