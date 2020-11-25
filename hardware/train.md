# 训练指标

- Time2train：在特定数据集上训练一个模型使其达到特定精度的用时。单位：sec（秒）。本指标主要关注被测硬件的计算性能。指标根据参与者提交的运行日志确定。

特定精度的定义如下：
|模型名称 | 目标精度|
|--------------|------------|
|ResNet50 | 75.90% classification|
|Mask R-CNN + FPN | -|
|BERT | -|
|Transformer | -|

- 吞吐：单位时间内，能够推理的样本数量。单位：samples/sec(样本数/秒)。本指标主要关注被测硬件的性能。指标根据参与者提交的运行日志确定。
- 加速比&加速效率：单张显卡Time2train和多张显卡Time2train的比率。本指标主要关注多卡并行训练的性能效果，尤其是硬件建通信机制的性能。指标根据参与者提交的运行日志换算获得。
- 能耗：我们期望能够客观的评估被测硬件的能耗情况，但暂未找到公平、可审核的方法。本指标将在后续提供评估方法。


## 日志格式要求
日志格式样例如下：
```
- AI-Rank-log 1558631910.424 test_begin
- AI-Rank-log 1558631912.424 eval_accuracy:0.16753999888896942, total_epoch_cnt:2
- AI-Rank-log 1558631913.424 eval_accuracy:0.3207400143146515, total_epoch_cnt:4
- AI-Rank-log 1558631914.424 eval_accuracy:0.4756399989128113, total_epoch_cnt:6
- AI-Rank-log 1558631915.424 eval_accuracy:0.6468799710273743, total_epoch_cnt:8
- AI-Rank-log 1558631916.424 eval_accuracy:0.7605400085449219, total_epoch_cnt:10
- AI-Rank-log 1558631922.454 test_finish
- AI-Rank-log 1558631918.454 target_quality_time:8.03sec
- AI-Rank-log 1558631918.455 avg_ips:1190images/sec

```
说明：
- 每行以`AI-Rank-log`开始，后接时间戳
- `test_begin`：测试开始
- `test_finish`：测试结束
- `eval_accuracy`：测试的准确率
- `total_epoch_cnt`：截至当前执行的epoch个数
- `target_quality_time`：`eval_accuracy达到AI-Rank要求的精度时的时间戳` - `test_begin时间戳`
- `avg_ips`：`total_epoch_cnt` * `每个epoch的样本总数` / `total_use_time`
- 训练期间每隔N个epoch进行一次eval测试，N由提交方自定义
- 当eval准确率达到该模型相应要求后，测试即可停止
