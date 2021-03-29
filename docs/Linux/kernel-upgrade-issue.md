## r server Linux kernel upgrade issue

问题是升级之后boot分区不够用

```shell
update-initramfs: Generating /boot/initrd.img-5.4.0-67-generic
Error 24 : Write error : cannot write compressed block
E: mkinitramfs failure cpio 141 lz4 -9 -l 24
update-initramfs: failed for /boot/initrd.img-5.4.0-67-generic with 1.
dpkg: error processing package initramfs-tools (--configure):
 installed initramfs-tools package post-installation script subprocess returned error exit status 1
Errors were encountered while processing:
 linux-firmware
 initramfs-tools
```

```shell
df -h | grep boot # 查看boot分区大小
```

```shell
uname -r # 查看当前的kernel
```

输出 5.4.0-62-generic

```shell
apt list --installed | grep linux-image # 安装了的kernel
```

```shell
WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

linux-image-5.4.0-62-generic/focal-updates,focal-security,now 5.4.0-62.70 amd64 [installed,automatic]
linux-image-5.4.0-66-generic/focal-updates,focal-security,now 5.4.0-66.74 amd64 [installed,automatic]
linux-image-5.4.0-67-generic/focal-updates,focal-security,now 5.4.0-67.75 amd64 [installed,automatic]
linux-image-generic/focal-updates,focal-security,now 5.4.0.67.70 amd64 [installed,automatic]
```

当前是62, 上面要装的是 67，这里中间的66是多余的。

```shell
apt remove linux-headers-5.4.0-66 linux-headers-5.4.0-66-generic linux-image-5.4.0-66-generic linux-modules-5.4.0-66-generic
```

问题解决。

------

[update-initramfs-error-24-write-error-cannot-write-compressed-block](https://superuser.com/questions/1601194/update-initramfs-error-24-write-error-cannot-write-compressed-block)

[error-24-write-error-cannot-write-compressed-block](https://askubuntu.com/questions/1207958/error-24-write-error-cannot-write-compressed-block)