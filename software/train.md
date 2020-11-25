# 训练指标

- 主流模型覆盖总和：支持工业界主流模型的数量，单位：个。本指标主要关注框架对业界常用模型的支持全面性。指标根据参与者提交的模型个数确定。
- Time2train：在特定数据集上训练一个模型使其达到特定精度的用时。单位：sec（秒）。本指标主要关注框架及模型训练的性能。指标根据参与者提交的运行日志确定。

特定精度的定义如下：
|模型名称 | 目标精度|
|--------------|------------|
|ResNet50 | 75.90% classification|
|Mask R-CNN + FPN | -|
|YOLOv3 | -|
|DeepLabv3+ | -|
|HRNet | -|
|BERT | -|
|Transformer | -|
|CycleGAN | -|
|pix2pix | -|
|TSM | -|
|DSSM | -|
|DeepFM | -|
|Wide&Deep | -|
|Word2Vec | -|

- 吞吐：单位时间内，能够推理的样本数量。单位：samples/sec(样本数/秒)。本指标主要关注框架及模型训练的性能。指标根据参与者提交的运行日志确定。
- 准确率：在eval测试中能够达到的最高准确率。本指标主要关注框架及模型可达到的最好预测精度。指标根据参与者提交的运行日志确定。
- 加速比&加速效率：单张显卡Time2train和多张显卡Time2train的比率。本指标主要关注多卡并行训练的性能效果。指标根据参与者提交的运行日志换算获得。


## 日志格式要求
日志格式样例如下：
```
- AI-Rank-log 1558631910.424 test_begin
- AI-Rank-log 1558631912.424 eval_accuracy:0.16753999888896942, total_epoch_cnt:2
- AI-Rank-log 1558631913.424 eval_accuracy:0.3207400143146515, total_epoch_cnt:4
- AI-Rank-log 1558631914.424 eval_accuracy:0.4756399989128113, total_epoch_cnt:6
- AI-Rank-log 1558631915.424 eval_accuracy:0.6468799710273743, total_epoch_cnt:8
- AI-Rank-log 1558631916.424 eval_accuracy:0.7605400085449219, total_epoch_cnt:10
- AI-Rank-log 1558631918.454 target_quality_time:8.03sec
- AI-Rank-log 1558631919.424 eval_accuracy:0.8005400085449219, total_epoch_cnt:12
- AI-Rank-log 1558631920.424 eval_accuracy:0.855400085449219, total_epoch_cnt:14
- AI-Rank-log 1558631921.424 eval_accuracy:0.9005400085449219, total_epoch_cnt:16
- AI-Rank-log 1558631922.424 eval_accuracy:0.955400085449219, total_epoch_cnt:18
- AI-Rank-log 1558631922.454 test_finish
- AI-Rank-log 1558631918.454 total_use_time:12.03sec
- AI-Rank-log 1558631918.455 avg_ips:1190images/sec

```
说明：
- 每行以`AI-Rank-log`开始，后接时间戳
- `test_begin`：测试开始
- `test_finish`：测试结束
- `eval_accuracy`：测试的准确率
- `total_epoch_cnt`：截至当前执行的epoch个数
- `target_quality_time`：`eval_accuracy达到AI-Rank要求的精度时的时间戳` - `test_begin时间戳`
- `total_use_time`：`test_finish时间戳` - `test_begin时间戳`
- `avg_ips`：`total_epoch_cnt` * `每个epoch的样本总数` / `total_use_time`
- 训练期间每隔N个epoch进行一次eval测试，N由提交方自定义
- 当eval准确率达到该模型相应要求后，提交方跟进自身经验，在精度达到自身模型最优值后，停止测试
