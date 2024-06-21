# branch develop

1. rebase output
2. add memory comsume
1. add nvtx records

# branch 2f1b

2f1b 分支是对 2F1B 调度算法的实现，旨在显存受限环境下提高 Full Recompute 的效率。
该分支是在 NoTE 分支的基础上进行改动的，因为测试机安装不上 TransformerEngine，在部分文件中删除了和 TE 有关的代码。对于非 INT8 训练的模型应该是不受影响的，如需使用 TE，请复原所作的修改。

## 使用说明
在命令行中加入以下参数即可，注意不要开启任何重计算
```Bash
--use-2f1b \
--no-recompute-stages 1 \
```
`--no-recompute-stages` 是一种更细粒度的控制，允许选择哪些 stage 参与重计算，一般来说，靠后的 stage 没有那么大的显存压力，关闭重计算可以进一步提高吞吐量。

## TO-DO List
+ 显存建模
+ 性能模型搭建
+ 显存泄露问题排查
+ 是否能对Block Recompute和Uniform Recompute进行支持？