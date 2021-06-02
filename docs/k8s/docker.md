## docker

[rootless running](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux_atomic_host/7/html/managing_containers/finding_running_and_building_containers_with_podman_skopeo_and_buildah)

[Registry as a pull through cache](https://docs.docker.com/registry/recipes/mirror/)

[彻底解决 gcr、quay、DockerHub 镜像下载难题](https://segmentfault.com/a/1190000022627844)

[为什么 Kubernetes 要替换 Docker](https://draveness.me/whys-the-design-kubernetes-deprecate-docker/)

`/etc/systemd/system/docker.service.d/http-proxy.conf`

```text
[Service]
# Environment="HTTP_PROXY=http://192.168.8.42:8123"
# Environment="HTTPS_PROXY=http://192.168.8.42:8123"
# Environment="NO_PROXY=localhost,127.0.0.1,docker-registry.example.com,.corp"
```

[docker images](https://docs.docker.com/engine/reference/commandline/images/): list image => docker image ls

[docker image](https://docs.docker.com/engine/reference/commandline/image/): manage images with sub-command

[rpi 需要添加的配置](https://www.raspberrypi.org/forums/viewtopic.php?t=203128) `/boot/firmware/cmdline.txt` 

```text
cgroup_enable=cpuset cgroup_enable=memory cgroup_memory=1 swapaccount=1
```

