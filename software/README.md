# 软件赛道
软件赛道主要评估深度学习框架&模型，在同等硬件、同等数据集、同等网络结构前提下的性能表现。

在定位上，AI-Rank主要为工业界需求方在框架及模型选型上，提供可供参考的性能数据。因此，在模型选择上，重点选择工业界高频使用的模型及数据集。

# 模型
模型选取范围如下：
|模型名称 | 应用领域 | 训练数据集 | 入选理由 |
|----------|---------|---------|---------|
|ResNet50 | 图像分类 | ImageNet | 最常用的图片分类模型 |
|Mask R-CNN + FPN | 目标检测 | - | -|
|YOLOv3 | 目标检测 | - | -|
|DeepLabv3+ | 图像分割 | - | -|
|HRNet | 图像分割 | - | -|
|BERT | 语义表示 | - | -|
|Transformer | 机器翻译 | - | -|
|CycleGAN | 图像生成 | - | -|
|pix2pix | 图像生成 | - | -|
|TSM | 视频分类 | - | -|
|DSSM | 智能推荐 | - | -|
|DeepFM | 智能推荐 | - | -|
|Wide&Deep | 智能推荐 | - | -|
|Word2Vec | 智能推荐 | - | -|

# 执行硬件
为保证软件赛道性能对比的公平性，AI-Rank规定所有软件测试的硬件约束如下：
- GPU：NV V100-SXM2-16GB
    - CUDA:10.1
    - cuDNN:7.6
- CPU：Intel(R) Xeon(R) Gold 6148 CPU @ 2.40GHz
- Memory：64 GB

经调研，改配置硬件被业界广泛使用。后续，AI-Rank可将考虑增加对比执行硬件的范围。

# 提交数据
提交的材料应包括：
- 被测系统信息：包括系统名，支持的模型，测试所用硬件平台等
- 源码：被测系统的源码，包括模型源码、执行脚本源码，也可以是源码链接。
- 数据：测试所需的数据，包括数据下载方法、数据预处理方法等。
- 日志：提交方，自行测试的日志。
- 报告及结果：编写详细的，可用于评审组复现的《测试&复现报告》
- 数据汇总：将核心指标按下文中格式要求汇总整理
- 申请方信息：包括但不限于：单位名称、xxxxx

## 主要指标及日志格式要求
- [训练](./train.md)
- [推理](./inference.md)

## 数据汇总
数据汇总格式如下：
主流模型覆盖：8/10
- 模型1
训练：

|              | Time2train(sec)  | 吞吐(samples/sec) | 准确率(%) | 加速比 |
|--------------|------------|------------|------------|-----------|
| 1卡          | -          |    -     |    -     |    -     |
| 2卡          | -          |    -     |    -     |    -     |
| 8卡          | -          |    -     |    -     |    -     |
| 32卡          | -          |    -     |    -     |    -     |

推理：
|              | 时延(sec)  | 吞吐(samples/sec) | 能耗 |
|--------------|------------|------------|------------|
|           | -          |    -     |    -     |

## 目录结构

提交目录结构示例如下：

- system name
    - system information
    - model1
        - code
        - data
        - log
            - train
                - GPUx1.log
                - GPUx2.log
                - GPUx8.log
                - GPUx32.log
            - inference
                - result.log
        - report
    - model2
        - code
        - data
        - log
            - train
                - GPUx1.log
                - GPUx2.log
                - GPUx8.log
                - GPUx32.log
            - inference
                - result.log
        - report
    - summary metrics
    - submitter information
