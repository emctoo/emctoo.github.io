### dunder: Double under (Underscore) -- magic methods

dir() to see the dunder methods

Python docs: datamodel 

##### [3.3 special method names](https://docs.python.org/3/reference/datamodel.html#special-method-names)

- `__new__` create a new instance
- `__init__` created 之后初始化
- `__del__`
- `__str__`, `__repr__` : object representation
- `__bytes__`
- `__format__`
- `__getitem__`, `__setitem__`, `__len__`: iteration, [] (indexer operator)
- `__call__`: object invocation
- `__lt__`, `__le__`, `__eq__`, `__ne__`, `__gt__`, `__ge__`
- `__hash__`
- `__bool__`

##### [3.4 customizing attribute access](https://docs.python.org/3/reference/datamodel.html#customizing-attribute-access)

- `__getattr__`
- `__getattribute__`
- `__setattr__`
- `__delattr__`
- `__dir__`

##### 3.3.2.1 Customizing module attribute access

3.3.2.2 implementing descriptors

3.3.2.3 invoking descriptors

3.3.2.4 `__slots__`

3.3.3 customizing class creation

3.3.3.1 metaclass

3.3.3.2 resolving MRO entries

3.4 coroutines

awaitable object: 实现了 `__await__`

`coroutine objects` returned from `async def` functions are awaitable



