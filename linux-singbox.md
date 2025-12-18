# Linux系统设置

```
sudo iptables -P FORWARD ACCEPT
```

二选一

```
sudo iptables -P FORWARD DROP
sudo iptables -A FORWARD -p tcp --dport 443 -j ACCEPT
sudo iptables -A FORWARD -p udp --dport 443 -j ACCEPT
sudo iptables -A FORWARD -p tcp --dport 80 -j ACCEPT
sudo iptables -A FORWARD -p udp --dport 80 -j ACCEPT
```

`uname -r` 查看内核版本，需要 `5.8`

```
vim /etc/sysctl.conf
```

```
net.ipv4.ip_forward=1
net.ipv6.conf.all.forwarding=1
```

```
sysctl -p
```

# 安装大鹅

该脚本需要 `curl`，`unzip`并且 `virt-what`为了工作，这些工具可以在大多数 Linux 系统的安装过程中自动安装。

```
sudo sh -c "$(wget -qO- https://github.com/daeuniverse/dae-installer/raw/main/installer.sh)" @ install
```

卸载大鹅

```
sudo sh -c "$(curl -sL https://raw.githubusercontent.com/daeuniverse/dae-installer/main/uninstaller.sh)"
```

参考文档：[https://github.com/daeuniverse/dae-installer](https://github.com/daeuniverse/dae-installer)

# 手动安装

Config配置：

```
mkdir -p /etc/dae

curl -L -o /etc/dae/config.dae https://github.com/daeuniverse/dae/raw/main/example.dae

# 设置配置文件权限
chmod 0640 /etc/dae/config.dae
```

Geo数据库：

```
mkdir -p /usr/local/share/dae/
pushd /usr/local/share/dae/
curl -L -o geoip.dat https://github.com/v2fly/geoip/releases/latest/download/geoip.dat
curl -L -o geosite.dat https://github.com/v2fly/domain-list-community/releases/latest/download/dlc.dat
popd
```

主程序文件：

```
wget https://github.com/daeuniverse/dae/releases/download/v0.5.1/dae-linux-x86_64.zip
# 解压
unzip dae-linux-x86_64.zip

# 进入到解压目录
cd dae-linux-x86_64

sudo chmod +x dae-linux-x86_64

sudo install -Dm755 dae-linux-x86_64 /usr/bin/dae
```

系统服务：

```
# 下载系统服务
sudo curl -L -o /etc/systemd/system/dae.service https://github.com/daeuniverse/dae/raw/main/install/dae.service

# 重启systemctl
sudo systemctl daemon-reload
# 启动+自启
sudo systemctl enable dae --now
# 状态
sudo systemctl status dae
# 重启大鹅
sudo systemctl restart dae.service
```

参考文档：[https://github.com/daeuniverse/dae/blob/main/docs/en/user-guide/run-as-daemon.md](https://github.com/daeuniverse/dae/blob/main/docs/en/user-guide/run-as-daemon.md)

# 查看日志

```
journalctl -xfu dae.service
```

# 修改singbox透明代理

`ip add`可以查看网口

```
# 全局配置
global {
    # 网卡需要修改
    lan_interface: ens18
    wan_interface: auto
    log_level: info
    auto_config_kernel_parameter: true
    dial_mode: domain
    allow_insecure: false
    so_mark_from_dae: 1234

    # tls配置
    tls_implementation: utls
    utls_imitate: chrome_auto
}

# 订阅配置
subscription {
}

# 节点配置
node {
    # 配置socks5出站节点，连接到sing-box的入站
    proxys: 'socks5://localhost:2080'
}

# 分组配置，以下采用固定策略，使用第一个节点
group {
    elden_proxy {
        policy: fixed(0)
    }
}

# dns配置
dns {
  upstream {
    googledns: 'udp://dns.google.com:53'
    alidns: 'udp://dns.alidns.com:53'
  }
  routing {
    request {
      qname(geosite:cn) -> alidns
      fallback: googledns
    }
    response {
        upstream(googledns) -> accept
        fallback: accept
    }
  }
}

# 路由配置
routing {
    pname(NetworkManager) -> direct
    dip(224.0.0.0/3, 'ff00::/8') -> direct
    dip(geoip:private) -> direct
    ip(geoip:cn) -> direct
    domain(geosite:cn) -> direct
    domain(geosite:category-ads) -> block

    pname(sing-box) -> must_direct
    pname(clash) -> must_direct

    # 默认出站分组
    fallback: elden_proxy
}
```

# 卸载大鹅

```
systemctl stop dae.service

systemctl disable dae.service

sudo systemctl daemon-reload

systemctl status dae.service

rm -f /etc/systemd/system/dae.service

rm -rf /etc/dae

rm -f /usr/bin/dae

rm -rf /usr/local/share/dae
```

# 参考网址

> https://github.com/daeuniverse/dae/blob/main/docs/en/user-guide/run-as-daemon.md
>
> https://github.com/daeuniverse/dae/blob/main/docs/zh/README.md
>
> https://github.com/daeuniverse/dae/blob/main/docs/en/configuration/routing.md
>
> https://idev.dev/proxy/dae-sing-box.html
>
> https://sakari.top/2023/dae-clash
>
> https://idev.dev/proxy/dae-manual-installation.html
