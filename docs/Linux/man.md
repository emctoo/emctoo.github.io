### daily tools

```shell
man -Lzh_CN 7 man
man -k namespaces
```

运行在1024以下的端口：

```shell
sudo setcap 'cap_net_bind_service=+ep' ./hello
```

