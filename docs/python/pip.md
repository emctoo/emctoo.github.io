### Commands for setup tuna pypi mirror

```python
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple -U pip setuptools wheel

# write to $HOME/.config/pip/pip.conf
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

