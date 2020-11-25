ML-Perf参考文档：
https://github.com/mlperf/training_policies/edit/master/training_rules.adoc
https://arxiv.org/pdf/1910.01500.pdf


# 软件赛道
软件赛道主要评估深度学习框架&模型，在同等硬件、同等数据集、同等网络结构前提下的性能表现。模型选取中国现阶段工业界高频使用的模型，对每个模型的执行性能进行评估。

# 模型
中国现阶段工业界高频使用的模型及对应数据集如下，选取范围如下：
| 模型                  | 数据集  | 入选理由 | 
|-----------------------|------------------|------------------|
| Resnet50              | ImageNet2012                 |    最常用的分类模型       |
| Bert Large Pre-train  | wikicorpus_en                |                        |
| OCR                   |                              |                        |

# 执行硬件
| 加速器                  | 处理器 | 入选理由 | 
|-----------------------|------------------|------------------|
|V100-SXM2-16GB | Intel(R) Xeon(R) Gold 6148 CPU @ 2.40GHz | 业内最常用显卡 |
| Intel             | |  |
| 华为              | |  |

ML-Perf硬件数据参考： https://github.com/mlcommons/hpc_results_v0.7/blob/main/CSCS/systems/daint_gpu_n128_tf2.2.0.json

# 主要指标

## 云端训练
- 主流模型覆盖总和：支持工业界主流模型的数量，单位：个。
- Time2train：在特定数据集上训练一个模型使其达到特定精度的用时。单位：sec（秒）。特定精度的定义如下：

TODO: 以下数据来自ML-Perf，需有所调整


|领域|问题 |数据集 |特定精度|
|-----------------------|-----------------------|-----------------------|-----------------------|
|Vision |Image classification |ImageNet |75.90% classification|
| |Object detection (light weight) |COCO |23.0% mAP|
| |Object detection (heavy weight) |COCO |0.377 Box min AP and 0.339 Mask min AP|
|Language |Translation (recurrent) |WMT English-German |24.0 Sacre BLEU|
| |Translation (non-recurrent) |WMT English-German |25.00 BLEU|
| |NLP |Wikipedia 2020/01/01 |0.712 Mask-LM accuracy|
|Commerce |Recommendation |1TB Click Logs|0.8025 AUC|
|Research |Reinforcement learning |Go |50% win rate vs. checkpoint|

- 加速比&加速效率：单卡下，相同模型在混合精度模式及FP32模式下的吞吐比。
- 吞吐：单位时间内，能够推理的样本数量。单位：samples/sec(样本数/秒)。

## 云端推理
- 主流硬件支持综合：支持部署的，业界常用芯片数量，单位：个。
- 主流模型覆盖综合：支持工业界主流模型的数量，单位：个。
- 时延：完成1次推理，所需时间。单位：ms（毫秒）
- 吞吐：单位时间内，能够推理的样本数量。单位：samples/sec(样本数/秒)。

## 终端推理
- 主流硬件支持综合：
- 主流模型覆盖综合：支持工业界主流模型的数量，单位：个。
- 时延：完成1次推理，所需时间。单位：ms（毫秒）
- 吞吐：单位时间内，能够推理的样本数量。单位：samples/sec(样本数/秒)。
- 内存占用：推理期间，推理模型最大使用内存量。单位：MB。

# 提交数据

## 日志格式要求
日志格式样例如下：
```
- AI-Rank-log 1558631910.424 test_begin
- AI-Rank-log 1558631912.424 eval_accuracy:0.16753999888896942, total_epoch_cnt:2
- AI-Rank-log 1558631913.424 eval_accuracy:0.3207400143146515, total_epoch_cnt:4
- AI-Rank-log 1558631914.424 eval_accuracy:0.4756399989128113, total_epoch_cnt:6
- AI-Rank-log 1558631915.424 eval_accuracy:0.6468799710273743, total_epoch_cnt:8
- AI-Rank-log 1558631916.424 eval_accuracy:0.7605400085449219, total_epoch_cnt:10
- AI-Rank-log 1558631917.424 test_finish
- AI-Rank-log 1558631918.454 total_use_time:8.03 sec
```
说明：
- 每行以`AI-Rank-log`开始，后接时间戳
- test_begin：测试开始
- test_finish：测试结束
- total_use_time：test_finish时间戳 - test_begin时间戳
- 训练期间每隔N个epoch进行一次eval测试，N由提交方自定义
- eval_accuracy：测试的准确率
- total_epoch_cnt：截至当前执行的epoch个数
- 当eval准确率达到该模型相应要求时，停止测试

参考
https://github.com/AIIABenchmark/AIIA-DNN-benchmark
https://github.com/mlperf/training/blob/master/benchmark_readme_template.md
https://github.com/mlperf/training/tree/master/image_classification