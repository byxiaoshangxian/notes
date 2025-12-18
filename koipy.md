# 运行环境

[https://koipy.gitbook.io/koipy/doc/miaospeed](https://koipy.gitbook.io/koipy/doc/miaospeed-hou-duan/da-jian-zhi-nan/docker-shi-yong)
[https://koipy.gitbook.io/koipy/kuai-su-kai-shi#docker-qi-dong](https://koipy.gitbook.io/koipy/kuai-su-kai-shi#docker-qi-dong)

重置Debian12系统（**可选**）：
默认root密码: `MoeClub.org`

```
bash <(wget --no-check-certificate -qO- 'https://www.moeelf.com/attachment/LinuxShell/InstallNET.sh') -d 12 -v 64 -a
```

命令后方可以跟镜像源

```
bash <(wget --no-check-certificate -qO- 'https://www.moeelf.com/attachment/LinuxShell/InstallNET.sh') -d 12 -v 64 -a --mirror 'http://mirrors.huaweicloud.com/debian/'
```

```
apt-get update && apt-get install -y sudo wget curl
```

1Panel面板（**可选**）：

```
curl -sSL https://resource.fit2cloud.com/1panel/package/quick_start.sh -o quick_start.sh && bash quick_start.sh
```

本机代理（**可选**）：

文件下载地址：[https://file.byxiao.top/local](https://file.byxiao.top/local)

终端复用器安装命令：`apt-get install screen -y`

在Clash配置文件中，添加 `external-ui: ./ui`

# miaospeed：

```
docker run -idt \
   --name miaospeed \
   --network=host \
   --restart always \
   airportr/miaospeed:latest \
   server -bind 0.0.0.0:8765 -path miaospeed -token SbbieN2e{Q?W -mtls
```

# Koipy：

```
docker run -itd \
--name=koipy \
--network=host \
--restart=always \
-v /root/koipy/config.yaml:/app/config.yaml \
koipy/koipy
```

# 订阅转换：

```
docker run -d --restart=always --network host asdlokj1qpi23/subconverter:latest
```

建议修改 `pref.toml` 文件第75行，更新规则、订阅走代理，原始订阅不走代理。
官网文档参考：https://github.com/tindy2013/subconverter/blob/master/README-cn.md

![](https://pic1.imgdb.cn/item/68120b3758cb8da5c8d5613e.png)

# 配置文件

[https://koipy.gitbook.io/koipy/pei-zhi-mu-ban](https://koipy.gitbook.io/koipy/pei-zhi-mu-ban)

自用配置如下，需要改写的地方已经使用 `<  >` 标注，注意替换。
PS：参考上方链接官网配置示例和FulltClash申请的相关ID。

```
admin:
  - <管理员TG ID>
bot:
  analyzeText: ""
  antiGroup: false
  api-hash: <请填写你的TG Bot API Hash>
  api-id: <请填写你的TG Bot API ID>
  bot-token: <请填写你的TG Bot Token>
  bar: "=" # 进度条
  bleft: "[" # 进度条
  bright: "]" # 进度条
  bspace: "  " # 进度条
  cacheTime: 0
  inviteGroup: []
  ipv6: true
  parseMode: MARKDOWN
  proxy: <socks5代理>
  scriptText: ""
  speedText: ""
  strictMode: false
image:
  color:
    background:
      inbound:
        alpha: 255
        end-color: "#ffffff"
        label: 0.0
        name: ""
        value: "#ffffff"
      outbound:
        alpha: 255
        end-color: "#ffffff"
        label: 0.0
        name: ""
        value: "#ffffff"
      script:
        alpha: 255
        end-color: "#ffffff"
        label: 0.0
        name: ""
        value: "#ffffff"
      scriptTitle:
        alpha: 255
        end-color: "#ffffff"
        label: 0.0
        name: ""
        value: "#EAEAEA"
      speed:
        alpha: 255
        end-color: "#ffffff"
        label: 0.0
        name: ""
        value: "#ffffff"
      speedTitle:
        alpha: 255
        end-color: "#ffffff"
        label: 0.0
        name: ""
        value: "#EAEAEA"
      topoTitle:
        alpha: 255
        end-color: "#ffffff"
        label: 0.0
        name: ""
        value: "#EAEAEA"
    delay:
      - label: 1.0
        name: "1"
        value: "#e4f8f9"
        alpha: 255
        end_color: "#ffffff"
      - label: 50.0
        name: "2"
        value: "#e4f8f9"
        alpha: 255
        end_color: "#ffffff"
      - label: 100.0
        name: "2"
        value: "#bdedf1"
        alpha: 255
        end_color: "#ffffff"
      - label: 200.0
        name: "3"
        value: "#96e2e8"
        alpha: 255
        end_color: "#ffffff"
      - label: 300.0
        name: "4"
        value: "#78d5de"
        alpha: 255
        end_color: "#ffffff"
      - label: 500.0
        name: "5"
        value: "#67c2cf"
        alpha: 255
        end_color: "#ffffff"
      - label: 1000.0
        name: "6"
        value: "#61b2bd"
        alpha: 255
        end_color: "#ffffff"
      - label: 2000.0
        name: "7"
        value: "#466463"
        alpha: 255
        end_color: "#ffffff"
      - label: 0.0
        name: "8"
        value: "#8d8b8e"
        alpha: 255
        end_color: "#ffffff"
    ipriskHigh:
      alpha: 255
      end-color: "#ffffff"
      label: 0.0
      name: ""
      value: "#ffffff"
    ipriskLow:
      alpha: 255
      end-color: "#ffffff"
      label: 0.0
      name: ""
      value: "#ffffff"
    ipriskMedium:
      alpha: 255
      end-color: "#ffffff"
      label: 0.0
      name: ""
      value: "#ffffff"
    ipriskVeryHigh:
      alpha: 255
      end-color: "#ffffff"
      label: 0.0
      name: ""
      value: "#ffffff"
    na:
      alpha: 255
      end-color: "#8d8b8e"
      label: 0.0
      name: ""
      value: "#8d8b8e"
    "no":
      alpha: 255
      end-color: "#ee6b73"
      label: 0.0
      name: ""
      value: "#ee6b73"
    outColor: []
    speed:
      - label: 0.0
        name: "1"
        value: "#fae0e4"
        alpha: 255
        end_color: "#ffffff"
      - label: 0.0
        name: "2"
        value: "#f7cad0"
        alpha: 255
        end_color: "#ffffff"
      - label: 25.0
        name: "3"
        value: "#f9bec7"
        alpha: 255
        end_color: "#ffffff"
      - label: 50.0
        name: "4"
        value: "#ff85a1"
        alpha: 255
        end_color: "#ffffff"
      - label: 100.0
        name: "5"
        value: "#ff7096"
        alpha: 255
        end_color: "#ffffff"
      - label: 150.0
        name: "6"
        value: "#ff5c8a"
        alpha: 255
        end_color: "#ffffff"
      - label: 200.0
        name: "7"
        value: "#ff477e"
        alpha: 255
        end_color: "#ffffff"
    wait:
      alpha: 255
      end-color: "#dcc7e1"
      label: 0.0
      name: ""
      value: "#dcc7e1"
    warn:
      alpha: 255
      end-color: "#fcc43c"
      label: 0.0
      name: ""
      value: "#fcc43c"
    "yes":
      alpha: 255
      end-color: "#bee47e"
      label: 0.0
      name: ""
      value: "#bee47e"
  compress: false
  emoji:
    enable: true
    source: TwemojiLocalSource
  endColorsSwitch: false
  font: ./resources/alibaba-Regular.ttf
  nonCommercialWatermark:
    alpha: 16
    angle: -16.0
    color:
      alpha: 16
      end-color: "#ffffff"
      label: 0.0
      name: ""
      value: "#000000"
    enable: false
    row-spacing: 1
    shadow: false
    size: 64
    start-y: 0
    text: 请勿用于商业用途
    trace: false
  speedEndColorSwitch: false
  title: 节点测试机器人
  watermark:
    alpha: 32
    angle: -16.0
    color:
      alpha: 16
      end-color: "#ffffff"
      label: 0.0
      name: ""
      value: "#000000"
    enable: false
    row-spacing: 0
    shadow: false
    size: 64
    start-y: 0
    text: FullTclash dev
    trace: false

license: <填写许可证>

log-level: INFO
network:
  userAgent: ClashMetaForAndroid/2.8.9.Meta Mihomo/0.16
runtime:
  entrance: true
  excludeFilter: ""
  geoipAPI: ip-api.com
  includeFilter: ""
  interval: 10
  ipstack: true
  localip: false
  nospeed: false
  pingURL: https://www.gstatic.com/generate_204
  sort: 订阅原序
  speedFiles:
    - https://dl.google.com/dl/android/studio/install/3.4.1.0/android-studio-ide-183.5522156-windows.exe
  speedNodes: 300
  speedThreads: 4
scriptConfig:
  scripts: # 脚本载入
    - type: gofunc # 表示是miaospeed的内置实现
      name: "TEST_PING_RTT" # 特殊保留名称，当设置为这些特殊保留值时会覆写程序内部的默认配置，更多的特殊保留值请参阅这里: https://github.com/airportr/miaospeed/blob/master/interfaces/matrix.go#L3
      rank: -100 # 排序
    - type: gojajs # 表示miaospeed主流脚本类型
      name: "示例脚本" # 脚本名称
      rank: 0 # 排序，越小排在越前面
      content: | # 脚本内容
        const C_NA = '142,140,142';
        const C_UNL = '186,230,126';
        const C_FAIL = '239,107,115';
        const C_UNK = '92,207,230';

        function handler() {
          return {
              text: '失败',
              background: C_UNK,
          }
        }
    - type: gojajs
      name: "Youtube"
      rank: 0
      content: "resources/scripts/builtin/youtube.js" # 也可以指定一个文件路径
    - type: gojajs
      name: "Disney+"
      rank: 1
      content: "resources/scripts/builtin/disney+.js"
    - type: gojajs
      name: "OpenAI"
      rank: 2
      content: "resources/scripts/builtin/openai.js"
    - type: gojajs
      name: "Tiktok"
      rank: 3
      content: "resources/scripts/builtin/tiktok.js"
    - type: gojajs
      name: "维基百科"
      rank: 4
      content: "resources/scripts/builtin/wikipedia.js"
    - type: gojajs
      name: "Claude"
      rank: 5
      content: "resources/scripts/builtin/Claude.js"
    - type: gojajs
      name: "Bilibili"
      rank: 6
      content: "resources/scripts/builtin/bilibili.js"
    - type: gojajs
      name: "微软Copilot"
      rank: 7
      content: "resources/scripts/builtin/copilot.js"
    - type: gojajs
      name: "Spotify"
      rank: 8
      content: "resources/scripts/builtin/spotify.js"
    - type: gojajs
      name: "Viu"
      rank: 9
      content: "resources/scripts/builtin/viu.js"
    - type: gojajs
      name: "IP风险"
      rank: 11
      content: "resources/scripts/builtin/iprisk.js"
    - type: gojajs
      name: "DNS区域"
      rank: 10
      content: "resources/scripts/builtin/dns.js"
# 以下为固定脚本名称，用于覆写内置的GEOIP脚本，脚本名称不可更改：
#    - type: gojajs
#      name: "GEOIP_INBOUND"
#      rank: 0
#      content: "YOUR_GEOIP_SCRIPT" # 默认的GEOIP脚本参见 https://github.com/AirportR/miaospeed/blob/master/engine/embeded/default_geoip.js

slaveConfig:
  default: ""
  showID: true
  slaves:
    - id: <后端id>
      comment: <后端备注，显示在bot页面的>
      hidden: false
      token: <miaoko后端token>
      type: miaospeed
      address: 127.0.0.1:8765
      path: <miaoko请求路径>
      option:
        downloadDuration: 8
        downloadThreading: 4
        pingAverageOver: 3
        taskRetry: 4
        downloadURL: https://dl.google.com/dl/android/studio/install/3.4.1.0/android-studio-ide-183.5522156-windows.exe
        pingAddress: https://cp.cloudflare.com/generate_204
        stunURL: udp://stunserver2024.stunprotocol.org:3478
      skipCertVerify: true
      tls: true
      invoker: "114514"
      buildtoken: MIAOKO4|580JxAo049R|GEnERAl|1X571R930|T0kEN
subconverter:
  address: 127.0.0.1:25500
  enable: true
  exclude: ""
  include: ""
  tls: false
translation:
  lang: zh_CN
  resources: {}
user: []
```

# 解锁脚本

[https://github.com/CloudPassenger/miaospeed-scripts](https://github.com/CloudPassenger/miaospeed-scripts)
