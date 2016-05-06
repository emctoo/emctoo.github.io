Python iterator/generator
=========================

## iterable

- iterable每次返回一个成员值.
- 内建的sequence类型(list, str, tuple)和non-sequence类型(dict, file对象)是ierable的. 
- 自定义的类型,实现了__iter__或者__getitem__就是iterable:
  * __iter__返回一个iterator
  
- 使用: for循环, 使用sequence的地方
- iter(iterable object) => iterator
- 判断是不是iterable: isinstance(obj, collections.Iterable)


## iterator

- stream of data
- 调用__next__方法或者用内建的next可以得到stream中连续的值
- stream结束返回StopIteration
- __iter__()方法, 返回self => 所有的iterator都是iterable
- [iterator types](https://docs.python.org/3/library/stdtypes.html#typeiter)

## generator

- generator expression: 返回iterator的表达式. example: sum(nth * nth for nth in range(10) if nth % 2 == 0)
- generator iterator: 由generator function创建的对象
- generator: 返回generator iterator的函数.
  * 包含yield
  * for循环和next情景下使用

https://docs.python.org/3/glossary.html
