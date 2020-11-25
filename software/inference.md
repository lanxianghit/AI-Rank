# 推理指标

（待更新）

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
- AI-Rank-log 1558631918.454 total_use_time:8.03sec
- AI-Rank-log 1558631918.455 avg_ips:1190images/sec
```
说明：
- 每行以`AI-Rank-log`开始，后接时间戳
- `test_begin`：测试开始
- `test_finish`：测试结束
- `total_use_time`：`test_finish时间戳` - `test_begin时间戳`
- 训练期间每隔N个epoch进行一次eval测试，N由提交方自定义
- `eval_accuracy`：测试的准确率
- `total_epoch_cnt`：截至当前执行的epoch个数
- `avg_ips`：`total_epoch_cnt` * `每个epoch的样本总数` / `total_use_time`
- 当eval准确率达到该模型相应要求时，停止测试
