解决问题的方式两种：对变量加 fine grained lock，或者加GIL

Python 1.5 曾尝试去掉 GIL，单线程 degrade 严重

5ms 或者 IO 发生时候就会释放GIL: cooperative multitasking

但是也可能没有释放 preemptive multitasking

thread 对变量加不加锁跟 bytecode 级别上是不是原子有关

sub-interpreter

bytecode: += 操作并不是原子的，[].append 是原子的，



https://opensource.com/article/17/4/grok-gil

https://granulate.io/introduction-to-the-infamous-python-gil/

https://faster-cpython.readthedocs.io/gil.html

https://github.com/python/cpython/blob/main/Python/ceval_gil.h

https://github.com/python/cpython/blob/main/Include/internal/pycore_gil.h