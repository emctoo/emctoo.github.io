[direnv](https://github.com/direnv/direnv)

Golang 写的二进制文件，放到 `$HOME/.local/bin` 并可执行

[需要 hook 到 shell 中](https://github.com/direnv/direnv/blob/master/docs/hook.md)：

```shell
# 添加到 ~/.bashrc
eval "$(direnv hook bash)"

# 添加到 ~/.zshrc
eval "$(direnv hook zsh)"
```

到一个目录下会检查 `.envrc` 文件，对于 Python 的可以写:

```toml
layout python

# ? not sure if this works
use python 3.7.6
```

初次进去会提示 `direnv allow`

会创建 `.direnv/python-$python_version` 虚拟环境并启用

PS1 上并没有默认的提示，需要添加，[参考](https://github.com/direnv/direnv/wiki/Python#restoring-the-ps1)

其他的 Python 支持参考 [wiki](https://github.com/direnv/direnv/wiki/Python)

------

### stdlib

```toml
# ~/projects/some-project/.envrc
# 目录下的 bin 加入到 $PATH
PATH_add bin
```

```toml
export DATABASE_URL=postgres://localhost:5432/db1

# 如果存在就覆盖
source_env_if_exists ".envrc.local"
```

------

### extending

`~/.config/direnv/lib/*.sh` 下的 bash 脚本可以用于扩展 stdlib 的功能

direnv 会在 bash 的 subshell 中执行 `.envrc` 中的内容，然后将变化了的环境变量复制到 active shell 中去





参考：

[Sharp tools: direnv](https://www.gertgoet.com/2020/10/28/direnv.html)