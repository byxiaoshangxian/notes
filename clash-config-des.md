# 示例文件

providers示范：[https://github.com/byxiaoshangxian/config/blob/main/providers.yaml](https://github.com/byxiaoshangxian/config/blob/main/providers.yaml)[
]([https://](https://github.com/byxiaoshangxian/config/blob/main/providers.yaml))

geoip示范：[https://github.com/byxiaoshangxian/config/blob/main/geoip.yaml](https://github.com/byxiaoshangxian/config/blob/main/geoip.yaml)

github示范1：[https://gist.github.com/xqm32/266a7ecdf8363dbf8dddabbf5f6643a7](https://gist.github.com/xqm32/266a7ecdf8363dbf8dddabbf5f6643a7)

github示范2：[https://gist.github.com/ricky9w/31fffc1b6eadadba2603f323dc92bebf](https://gist.github.com/ricky9w/31fffc1b6eadadba2603f323dc92bebf)

# 思维图

![image](https://pic.imgdb.cn/item/66179b9168eb9357135c6859.png)

# 帮助理解网址

* 在线解析：[https://nodeca.github.io/js-yaml/](https://nodeca.github.io/js-yaml/)
* 菜鸟yaml教程：[https://www.runoob.com/w3cnote/yaml-intro.html](https://www.runoob.com/w3cnote/yaml-intro.html)

# 详细字段讲解

1、全局配置：

该配置位于 `proxies` 组上方，定义ipv6功能、dns、客户端指纹、外部控制等等，该配置可参考官方文档。

2、proxy （代理）：

该配置用于定义服务器（节点），书写方式如下，详细参考 [链接](https://wiki.metacubex.one/config/proxies/)

```
{
    "type": "vless",
    "name": "🇺🇸 自建 RackNerd 美国",
    "server": "youxuan.byxiao.top",
    "port": 443,
    "uuid": "90e7d3e8-0be8-4f6a-d325-5081ec25e714",
    "tls": true,
    "sni": "us.byxiao.top",
    "skip-cert-verify": false,
    "network": "ws",
    "ws-opts": {
      "headers": {
        "Host": "us.byxiao.top"
      },
      "path": "/hello"
    },
  }
```

3、proxy-providers （代理集）
代理集合，该配置项用于将机场订阅聚合到文件中。

```
freenodes:
    type: http
    url: "https://dy.byxiao.top/v2ray"
    path: ./proxy_providers/freenodes.yaml
    interval: 86400
    health-check:
      enable: true
      url: https://www.gstatic.com/generate_204
      interval: 300
      timeout: 5000
      expected-status: 204
    override:
      udp: true
```

![](https://pic.imgdb.cn/item/66cdcca9d9c307b7e92ed843.png)

4、proxy-groups
将节点进行分类（分组），可自定义嵌套。示例如下：

```
- name: 🚀 手动切换
  type: select
  proxies:
    - 香港
```

5、rule-providers （规则集）：
在线规则，使规则更加灵活，作用同rules相同。示例如下：

```
rule-providers:
  apple:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/apple.txt"
    path: ./RuleSet/apple.yaml
    interval: 86400
```

6、rules （规则）
将满足规则的流量转发到指定分组中，进行出站处理，匹配方式有很多种，如下列表格：

| 规则名称   | 详细参数              |
| ---------- | --------------------- |
| 域名规则   | DOMAIN、DOMAIN-SUFFIX |
| 数据库匹配 | GEOIP、GEOSITE        |
| ......     | ......                |

# 参考地址

> [https://github.com/Loyalsoldier/clash-rules](https://github.com/Loyalsoldier/clash-rules)
>
> [https://wiki.metacubex.one/example/conf/#__tabbed_2_1](https://wiki.metacubex.one/example/conf/#__tabbed_2_1)
>
> [https://gist.github.com/xqm32/266a7ecdf8363dbf8dddabbf5f6643a7](https://gist.github.com/xqm32/266a7ecdf8363dbf8dddabbf5f6643a7)
>
> [https://a-nomad.com/clash](https://a-nomad.com/clash)
>
> [https://github.com/Loyalsoldier/v2ray-rules-dat](https://github.com/Loyalsoldier/v2ray-rules-dat)
>
> [https://gist.github.com/liuran001/5ca84f7def53c70b554d3f765ff86a33](https://gist.github.com/liuran001/5ca84f7def53c70b554d3f765ff86a33)
>
> [https://github.com/MetaCubeX/meta-rules-dat](https://github.com/MetaCubeX/meta-rules-dat)
>
> [https://wener.me/notes/service/network/proxy/clash/conf](https://wener.me/notes/service/network/proxy/clash/conf)
>
> [https://www.10101.io/2020/02/12/use-clash-proxy-provider-with-subconverter/comment-page-1](https://www.10101.io/2020/02/12/use-clash-proxy-provider-with-subconverter/comment-page-1)
>
> [https://wiki.metacubex.one/startup/service/](https://wiki.metacubex.one/startup/service/)

# 群友的引用
> https://github.com/Lbiebest/clash-config/blob/main/README.md
>
> https://github.com/Lbiebest/clash-config/blob/main/scripts/custom-rule.js
>
> https://github.com/ClashConnectRules/Self-Configuration/blob/main/README_CN.md
>
> https://github.com/ClashConnectRules/Self-Configuration/blob/main/Clash.yaml
