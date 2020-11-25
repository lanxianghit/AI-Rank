# 硬件赛道
硬件赛道主要用于综合评估供深度学习训练、推理所用的硬件计算设备。主要评估原则是，在同等框架、同等模型（及网络结构）、同等数据集前提下，被测硬件的性能表现。
当前业内的第三方评估系统，在导向上追求更高的计算性能，往往参与评估的单位、硬件仅仅是业内最顶尖的几个。殊不知，很多性能中等、性价比较高的设备，在很多实际应用中有着广泛市场。也有些设备，在特定应用场景下有着稳定需求。
在定位上，AI-Rank主要为工业界需求方在硬件选型上，提供可供参考的性能数据。希望为需求方提供更务实、可靠且广泛的硬件性能数据。因此，非常欢迎、渴望众多厂商参与评估。

# 框架
为保证硬件性能数据的可对比性，我们约束，参与评估的硬件厂商，在如下3款深度学习平台下完成测试：
- [PaddlePaddle 2.0.0](https://www.paddlepaddle.org.cn/install/quick/zh/2.0rc-linux-pip)
- [TensorFlow 2.4.0](https://tensorflow.google.cn/install/)
- [PyTorch 1.7.0](https://pytorch.org/get-started/locally/#linux-installation)

# 模型
AI-Rank 选择最具代表性的4个模型，作为衡量硬件计算能力的测试“程序”：
|模型名称 | 应用领域 | 训练数据集 | 入选理由 |
|----------|---------|---------|---------|
|ResNet50 | 图像分类 | ImageNet | 最常用的图片分类模型 |
|Mask R-CNN + FPN | 目标检测 | - | -|
|BERT | 语义表示 | - | -|
|Transformer | 机器翻译 | - | -|
注意，提交测试数据时，务必保证以上4个模型均完成测试、均提供测试数据。

# 提交数据
提交的材料应包括：
- 被测系统信息：硬件型号，选用的框架、模型
- 源码：测试所需源码，如算子、执行脚本等
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
- ResNet50
训练：

|              | Time2train(sec)  | 吞吐(samples/sec) | 加速比 | 能耗(暂不需要填写) |
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
    - ResNet50
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
    - Mask R-CNN + FPN
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
