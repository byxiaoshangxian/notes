# 搭建要求

```
1、 公网IP，必须条件，没有这个文章就不用看了
2、 你需要一个能跑 mihomo 内核的载体，如 openwrt、Linux，Windows 等系统。
```

# 解决问题

1. 在外不想直接暴露协议，并且对数据有一定加密需求，列如：校园网禁止访问某些网站，或者有审计。
2. 可以直接访问内网，并不需要每个设备都暴露公网端口
3. 想要一个稳定的代理环境，因为家里软路由随时都可以切换代理，并不需要导入机场。

# 原理解释

mihomo内核可以监听到入站代理，只需要将协议配置好，即可进入clash规则进行拦截，并且转发到节点。

![](https://pic.imgdb.cn/item/66fa1e13f21886ccc06b8c47.png)

# 详细操作步骤

我这里配置文件以 `SS 2022` 和带TLS的 `Tuic V5` 为例，系统为openwrt，插件为 `MihomoTProxy`，以下配置文件为**头部**，下方的代理和代理组可以通过订阅转换生成。

listeners 配置，为入站协议配置。详细配置也可以参考 [此处点击跳转官方文档](https://wiki.metacubex.one/config/inbound/listeners/ss/) 。

**这里说一个 `MihomoTProxy` 的坑，在配置ssl证书的时候，该路径指的是运行路径，也就是 `/etc/mihomo/run/` ，需要将证书放在这个路径下，并且配置文件中，不能使用绝对路径，不然会报错找不到。**

```
port: 7890
socks-port: 7891
mixed-port: 2333
allow-lan: true
mode: rule
log-level: info
tcp-concurrent: true
global-client-fingerprint: chrome
unified-delay: true
profile:
  store-selected: true
sniffer:
  enable: true
  sniff:
    HTTP:
      ports: [80, 8080-8880]
      override-destination: true
    TLS:
      ports: [443, 8443]
    QUIC:
      ports: [443, 8443]
  skip-domain:
    - "Mijia Cloud"
    - "+.push.apple.com"

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
    - 122.112.208.1
    - "[2400:3200::1]"
    - "[2402:4e00::]"
  nameserver:
    - 119.29.29.29
    - 223.5.5.5
    - "tls://8.8.4.4#dns"
    - "tls://1.0.0.1#dns"
    - "tls://[2001:4860:4860::8844]#dns"
    - "tls://[2606:4700:4700::1001]#dns"
  proxy-server-nameserver:
    - https://223.5.5.5/dns-query
    - https://doh.pub/dns-query
  nameserver-policy:
    "geosite:cn,private":
      - https://dns.alidns.com/dns-query
      - https://doh.pub/dns-query

listeners:
  - name: tuicv5
    type: tuic
    port: 10002
    listen: 0.0.0.0
    users:
      2cd6ed0f-636e-4e6c-9449-5a263d7a0fa5: password6666
    certificate: ./server.crt
    private-key: ./server.key
    congestion-controller: bbr
    max-idle-time: 15000
    authentication-timeout: 1000
    alpn:
      - h3
    max-udp-relay-packet-size: 1500

  - name: ss-in
    type: shadowsocks
    port: 10001
    listen: 0.0.0.0
    cipher: 2022-blake3-aes-256-gcm 
    password: vlmpIPSyHH6f4S8WVPdRIHIlzmB+GIRfoH3aNJ/t9Gg=
    udp: true
```
