默认情况下 poetry 在 $HOME/.poetry 下创建 venv

```shell
# create venv in the project root directory
poetry config --local virtualenvs.in-project true

# always create venv in the project root directory
poetry config virtualenvs.in-project true 

# this will create venv
poetry env use python

# entering venv
poetry shell

# show venv information
poetry env info
```

poetry 添加源

```toml
[[tool.poetry.source]]
name = "douban"
url = "https://pypi.tuna.tsinghua.edu.cn/simple/"
```

```shell
poetry add flask
poetry install
```

