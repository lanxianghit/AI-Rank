# 硬件赛道

## 云端训练
- Time2train：在特定数据集上训练一个模型使其达到Quality Target时的用时。单位：sec（秒）。
- 吞吐：单位时间内，能够训练的样本数量。单位：samples/sec(样本数/秒)。
- 加速比&加速效率：单卡下，相同模型在混合精度模式及FP32模式下的吞吐比。
- 能耗：每度电（千瓦时），能够训练的样本数量。单位samples/kW·h(样本数/度)。

## 云端推理
- 时延：完成1次推理，所需时间。单位：ms（毫秒）
- 吞吐：单位时间内，能够推理的样本数量。单位：samples/sec(样本数/秒)。
- 能耗：每度电，能够推理的样本数量。单位samples/kW·h(样本数/度)。

## 终端推理
- 时延：完成1次推理，所需时间。单位：ms（毫秒）
- 吞吐：单位时间内，能够推理的样本数量。单位：samples/sec(样本数/秒)。
- 能耗：每瓦秒，能够推理的样本数量。单位samples/W*sec(样本数/瓦秒)。

# 提交数据

# 主要测试结果

| Processor                  | Single Precision             | Int8 inputs/32 bit math | 
|-----------------------|------------------|-----------------------|
| Raspberry Pi 3        | Conv                         | GEMM, Sparse GEMM               |
| iPhone 6              |                              | GEMM, Sparse GEMM               |
| iPhone 7              |                              | GEMM, Sparse GEMM               |
