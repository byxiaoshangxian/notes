固件下载地址：[https://downloads.immortalwrt.org/](https://downloads.immortalwrt.org/)

主题名称：`luci-theme-Argon`

其他额外的一些东西：`ttyd`、`screen`、`openssh-sftp-server`、`luci-app-homeproxy`、`procd-ujail`（MihomoTProxy额外插件）

```
apt install parted
opkg install zip unzip
```

常用命令：`netstat -tulnp`

防火墙推荐设置：

![image.png](/upload/image.png)

扩容教程：

```
gunzip immortalwrt-24.10.0-rc3-x86-64-generic-squashfs-combined-efi.img.gz

dd if=/dev/zero bs=1M count=500 >>openwrt.img

parted openwrt.img

print

resizepart 2 100%

print

quit
```

> 分区读取报错看这个：https://blog.aoe.top/notes/474
> 
> 分区代码：https://www.cnblogs.com/maguyusi/p/18574745
> 
> 博客：https://www.aladown.com/2023/01/OpenWRT-%E6%89%A9%E5%AE%B9%E6%96%B9%E6%B3%95/
