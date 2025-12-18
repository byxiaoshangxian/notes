# 一键懒人包

下载文件：[https://file.byxiao.top/local](https://file.byxiao.top/local) **（注：内含mihomo 核心为X86架构，根据自己机器情况更换核心并赋予权限）**

```
apt-get install zip || yum install -y unzip zip

mkdir clash && mv ./mihomo.zip ./clash

cd clash && unzip mihomo.zip

chmod a+x mihomo && chmod -R 777 ../clash
```

新版本懒人包已将systemd放在目录下自行修改路径后，执行以下命令

```
mv .mihomo.service /etc/systemd/system/mihomo.service #移动系统服务

systemctl daemon-reload  #重启systemd

systemctl enable mihomo  #开启服务

systemctl start mihomo #开启自启动
```

接下来修改 `config.yaml` 将dns和tun模式改为True，即可修改网关体验了。

<font color=#FF0000 >如果出现配置成功但是没有流量转发到Clash ，请参考下方Linux系统设置，将内核转发流量开启</font>

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

---

# 手动安装 【拓展】

## 下载 mihomo Core

[https://github.com/MetaCubeX/mihomo/releases](https://github.com/MetaCubeX/mihomo/releases)

选择 `mihomo-linux-amd64-v1.18.3.gz` 报错选择 `mihomo-linux-amd64-compatible-v1.18.3.gz`

```
chmod -R 777 ./clash #外层目录一定要给权限

gzip -d mihomo-linux-amd64-compatible-v1.18.3.gz

mv mihomo-linux-amd64-compatible-v1.18.3 ./mihomo

chmod a+x mihomo

cp mihomo /usr/local/bin
```

## 配置文件示例

```
port: 7890
socks-port: 7891
allow-lan: true
mode: Rule
log-level: info
tcp-concurrent: true
external-controller: :9090
external-ui: ./ui
geodata-mode: true
global-client-fingerprint: chrome
profile:
  store-selected: true
sniffer:
  enable: true
  force-dns-mapping: true
  parse-pure-ip: true
  force-domain:
    - "+.netflix.com"
    - "+.nflxvideo.net"
    - "+.amazonaws.com"
    - "+.media.dssott.com"
  skip-domain:
    - "+.apple.com"
    - Mijia Cloud
    - dlg.io.mi.com
  sniff:
    TLS:
    HTTP:
      ports:
        - 80
        - 8080-8880
      override-destination: true
tun:
  enable: true
  stack: mixed
  dns-hijack:
    - "any:53"
  auto-route: true
  auto-detect-interface: true

dns:
  enable: true
  listen: :1053
  ipv6: true
  enhanced-mode: fake-ip
  fake-ip-range: 28.0.0.1/8
  fake-ip-filter:
    - "*"
    - "+.lan"
    - "+.local"
  default-nameserver:
    - 223.5.5.5
    - 119.29.29.29
    - 114.114.114.114
    - "[2402:4e00::]"
    - "[2400:3200::1]"
  nameserver:
    - "tls://8.8.4.4#dns"
    - "tls://1.0.0.1#dns"
    - "tls://[2001:4860:4860::8844]#dns"
    - "tls://[2606:4700:4700::1001]#dns"
  proxy-server-nameserver:
    - https://doh.pub/dns-query
  nameserver-policy:
    "geosite:cn,private":
      - https://doh.pub/dns-query
      - https://dns.alidns.com/dns-query

experimental:
  ignore-resolve-fail: true
unified-delay: true

proxy-groups:
  - name: PROXY
    type: select
    proxies:
      - DIRECT
    use:
      - provider1

proxy-providers:
  provider1:
    type: http
    url: "https://dy.byxiao.top/v2ray"
    path: ./proxy_providers/provider1.yaml
    interval: 3600
    health-check:
      enable: true
      url: https://www.gstatic.com/generate_204
      interval: 300
      timeout: 5000
      expected-status: 204
    override:
      udp: true

rule-providers:
  reject:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/reject.txt"
    path: ./ruleset/reject.yaml
    interval: 86400

  icloud:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/icloud.txt"
    path: ./ruleset/icloud.yaml
    interval: 86400

  apple:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/apple.txt"
    path: ./ruleset/apple.yaml
    interval: 86400

  google:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/google.txt"
    path: ./ruleset/google.yaml
    interval: 86400

  proxy:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/proxy.txt"
    path: ./ruleset/proxy.yaml
    interval: 86400

  direct:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/direct.txt"
    path: ./ruleset/direct.yaml
    interval: 86400

  private:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/private.txt"
    path: ./ruleset/private.yaml
    interval: 86400

  gfw:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/gfw.txt"
    path: ./ruleset/gfw.yaml
    interval: 86400

  tld-not-cn:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/tld-not-cn.txt"
    path: ./ruleset/tld-not-cn.yaml
    interval: 86400

  telegramcidr:
    type: http
    behavior: ipcidr
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/telegramcidr.txt"
    path: ./ruleset/telegramcidr.yaml
    interval: 86400

  cncidr:
    type: http
    behavior: ipcidr
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/cncidr.txt"
    path: ./ruleset/cncidr.yaml
    interval: 86400

  lancidr:
    type: http
    behavior: ipcidr
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/lancidr.txt"
    path: ./ruleset/lancidr.yaml
    interval: 86400

  applications:
    type: http
    behavior: classical
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/applications.txt"
    path: ./ruleset/applications.yaml
    interval: 86400

rules:
  - RULE-SET,applications,DIRECT
  - DOMAIN,clash.razord.top,DIRECT
  - DOMAIN,yacd.haishan.me,DIRECT
  - RULE-SET,private,DIRECT
  - RULE-SET,reject,REJECT
  - RULE-SET,icloud,DIRECT
  - RULE-SET,apple,DIRECT
  - RULE-SET,google,PROXY
  - RULE-SET,proxy,PROXY
  - RULE-SET,direct,DIRECT
  - RULE-SET,lancidr,DIRECT
  - RULE-SET,cncidr,DIRECT
  - RULE-SET,telegramcidr,PROXY
  - GEOIP,LAN,DIRECT
  - GEOIP,CN,DIRECT
  - MATCH,PROXY
```

# 创建运行服务

创建 systemd 配置文件 `/etc/systemd/system/mihomo.service`，复制粘贴下方命令到控制台

```
sudo cat > /etc/systemd/system/mihomo.service << 'EOF'
[Unit]
Description=mihomo Daemon, Another Clash Kernel.
After=network.target NetworkManager.service systemd-networkd.service iwd.service

[Service]
Type=simple
LimitNPROC=500
LimitNOFILE=1000000
CapabilityBoundingSet=CAP_NET_ADMIN CAP_NET_RAW CAP_NET_BIND_SERVICE CAP_SYS_TIME CAP_SYS_PTRACE CAP_DAC_READ_SEARCH CAP_DAC_OVERRIDE
AmbientCapabilities=CAP_NET_ADMIN CAP_NET_RAW CAP_NET_BIND_SERVICE CAP_SYS_TIME CAP_SYS_PTRACE CAP_DAC_READ_SEARCH CAP_DAC_OVERRIDE
Restart=always
ExecStartPre=/usr/bin/sleep 1s
ExecStart=/usr/local/bin/mihomo -d /etc/mihomo # 需要修改为自己的
ExecReload=/bin/kill -HUP $MAINPID

[Install]
WantedBy=multi-user.target
EOF
```

使用以下命令重新加载 systemd：

```
systemctl daemon-reload

systemctl enable mihomo

systemctl start mihomo
```

mihomo 重新加载：`systemctl reload mihomo`

检查 mihomo 的运行状况：`systemctl status mihomo`

检查 mihomo 的运行日志：`journalctl -u mihomo -o cat -e`

# DNS 泄露网址

* [https://surfshark.com/zh/dns-leak-test](https://surfshark.com/zh/dns-leak-test)
* [https://ipleak.net/](https://ipleak.net/)
* [https://browserleaks.com/webrtc](https://browserleaks.com/webrtc)
* [https://whoer.net/dns-leak-test](https://whoer.net/dns-leak-test)

# 参考文档

> [配置文件参考](https://github.com/JohnsonRan/CRules)
>
> [https://github.com/Loyalsoldier/v2ray-rules-dat](https://github.com/Loyalsoldier/v2ray-rules-dat)
>
> [https://github.com/Loyalsoldier/clash-rules](https://github.com/Loyalsoldier/clash-rules)
>
> [ https://github.com/DustinWin/ruleset_geodata](https://github.com/DustinWin/ruleset_geodata)
>
> [https://github.com/MetaCubeX/meta-rules-dat](https://github.com/MetaCubeX/meta-rules-dat)
