# 硬件赛道

## 云端推理
- 时延：完成1次推理，所需时间。单位：ms（毫秒）
- 吞吐：单位时间内，能够推理的样本数量。单位：samples/sec(样本数/秒)。
- 能耗：每度电，能够推理的样本数量。单位samples/kW·h(样本数/度)。

## 终端推理
- 时延：完成1次推理，所需时间。单位：ms（毫秒）
- 吞吐：单位时间内，能够推理的样本数量。单位：samples/sec(样本数/秒)。
- 能耗：每瓦秒，能够推理的样本数量。单位samples/W*sec(样本数/瓦秒)。

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
