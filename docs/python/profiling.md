benchmark: timeit

[snakevis](https://jiffyclub.github.io/snakeviz/) to visualize the benchmark result

[profiling and timing in IPython](https://colab.research.google.com/github/jakevdp/PythonDataScienceHandbook/blob/master/notebooks/01.07-Timing-and-Profiling.ipynb)

IPython magic commands

都可以用 `%%time` 和 `%%timeit` 等来看 cell的

`%time` 类似 shell 中的 time，会给出 CPU / System / User 等的区别

`%timeit` 是用的 `timeit` , 会执行多此看mean / std，也处理了 GC 的问题，会比 `%time` 略快

`%prun` 可以看其中的调用，看在哪里耗时

`pip install line_profiler memory_profiler`

`%lprun` 可以到逐行看

`%memit` 和 `%mprun` 是对应的 memory 版本

