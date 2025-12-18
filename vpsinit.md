## 更新及安装组件

## Debian/Ubuntu

```shell
apt install sudo
sudo apt-get update && sudo apt-get install -y sudo wget curl socat
```

## CentOS 系列

```shell
yum install sudo
yum -y install wget
sudo yum -y update && sudo yum install -y sudo wget curl socat
```

### 关闭防火墙

```shell
systemctl stop firewalld.service
systemctl disable firewalld.service
```

## 常见面板

宝塔：

```
if [ -f /usr/bin/curl ];then curl -sSO https://download.bt.cn/install/install_panel.sh;else wget -O install_panel.sh https://download.bt.cn/install/install_panel.sh;fi;bash install_panel.sh ed8484bec
```

1panel：

```
bash -c "$(curl -sSL https://resource.fit2cloud.com/1panel/package/v2/quick_start.sh)"
```

## 安装加速

### 不卸载内核版本

```shell
wget -O tcpx.sh "https://github.com/ylx2016/Linux-NetSpeed/raw/master/tcpx.sh" && chmod +x tcpx.sh && ./tcpx.sh
```

### 卸载内核版本

```shell
wget -O tcp.sh "https://github.com/ylx2016/Linux-NetSpeed/raw/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```

## VPS测试脚本

### 回程脚本

#### backtrace

```shell
curl https://raw.githubusercontent.com/zhanghanyun/backtrace/main/install.sh -sSf | sh
```

![alt](https://www.bandwagonhost.net/wp-content/uploads/2022/09/bandwagonhostnet_backtrace.png)

#### besttrace 带AS编号版

```shell
wget -qO- git.io/besttrace | bash
```

## Acme脚本

```shell
curl https://get.acme.sh | sh
```

## Linux相关命令

### 后台运行

```shell
nohup Sever &
示例： nohup ./test.sh &
```

### 查看占用端口的进程

```shell
lsof -i:端口号
示例：lsof -i:22

netstat -tunlp |grep 端口号
示例：netstat -tunlp |grep 22
```

### 快速清空文件内容

```shell
echo "" > 文件
cat /dev/null > 文件
```

## 其他相关地址

宝塔：
[https://www.bt.cn/bbs/thread-19376-1-1.html](https://www.bt.cn/bbs/thread-19376-1-1.html)

V2Fly：
[https://github.com/v2fly/fhs-install-v2ray](https://github.com/v2fly/fhs-install-v2ray)

multi-v2ray：
[https://github.com/Jrohy/multi-v2ray](https://github.com/Jrohy/multi-v2ray)

Trojan多用户管理：
[https://github.com/Jrohy/trojan](https://github.com/Jrohy/trojan)

十一合一暴力安装脚本：
[https://github.com/jinwyp/one_click_script](https://github.com/jinwyp/one_click_script)

BBR脚本多合一：
[https://github.com/ylx2016/Linux-NetSpeed](https://github.com/ylx2016/Linux-NetSpeed/)
