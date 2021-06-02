[dapr 1.0 展望](https://skyao.io/talk/202103-dapr-from-servicemesh-to-cloudnative/) 介绍 service mesh，云原生，微服务相关的演进发展

[dapr做的 .NET Core 电商demo](https://mp.weixin.qq.com/s?__biz=MzAwNTMxMzg1MA%3D%3D&chksm=80d83c92b7afb584055c95c1386ddcd830b483110dbcad7d2a480758fcedae60d50e793ac296&idx=1&mid=2654083271&scene=21&sn=54baded97eea9dfc406d6375f4cae488#wechat_redirect)

dapr init 时可以 -s, --slim 选项指定 [slim-init mode](https://docs.dapr.io/operations/hosting/self-hosted/self-hosted-no-docker/)，无需docker

默认环境包含了:

- redis container，本地的状态管理和消息代理
- zipkin container, 观测性
- 创建默认components文件夹 ~/.dapr/components/
- dpar placement

```shell
dapr run --app-id myapp --dapr-http-port 3500
```

