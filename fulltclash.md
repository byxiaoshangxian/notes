# 全自动脚本

[https://github.com/AirportR/autoftc](https://github.com/AirportR/autoftc)

## 环境

* Python： [https://v2rayssr.com/go?url=https://www.python.org/downloads/windows/](https://v2rayssr.com/go?url=https://www.python.org/downloads/windows/)
* pip 源和依赖环境：[https://v2rayssr.com/ssrspeedn.html](https://v2rayssr.com/ssrspeedn.html)
* 官方源：[https://github.com/AirportR/FullTclash](https://github.com/AirportR/FullTclash)
* 官方依赖： `pip install -r requirements.txt`
* 测速Core： [https://github.com/AirportR/FullTCore/releases](https://github.com/AirportR/FullTCore/releases)
* subconverter Alpha： [https://github.com/MetaCubeX/subconverter/releases/tag/Alpha](https://github.com/MetaCubeX/subconverter/releases/tag/Alpha)

## 配置补全：

UID 获取：[@userinfobot](https://t.me/userinfobot) 

api\_id、api\_hash获取：[https://my.telegram.org/apps](https://my.telegram.org/apps)
获取此步比较挑IP，干净IP成功率大！
bot token获取：[@BotFather](https://t.me/BotFather) 创建一个机器人

## 配置填写

创建：`config.yaml` 文件

```
admin:
- telegram UID
bot:
  api_hash: telegram 官方网页获取api_hash
  api_id: telegram 官方网页获取api_id
  bot_token: 创建机器人的ID
  proxy: socks5 代理地址和端口
clash:
  path: ./bin/FullTCore

subconverter:
  enable: true
  host: 127.0.0.1:25500
  remoteconfig: https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/config/ACL4SSR_Online.ini    
```

## FullTclash，启动！

在此处新建powershell输入 `python main.py` 即可启动程序

## 简单使用命令

测速度：`/speedurl 订阅`   |   测落地：`/analyzeurl 订阅`   |   测流媒体 `/testurl 订阅`

**参考资料源**：

> [https://www.mspace.cc/archives/903](https://www.mspace.cc/archives/903)
>
> [https://fulltclash.gitbook.io/fulltclash-doc](https://fulltclash.gitbook.io/fulltclash-doc)
>
> [https://www.updating.top/media-unlock-bot/](https://www.updating.top/media-unlock-bot/)
>
> [https://c1oudf1are.link/p/fulltclash/#fulltclash%E5%90%AF%E5%8A%A8](https://c1oudf1are.link/p/fulltclash/#fulltclash%E5%90%AF%E5%8A%A8)
>
> 配色参考：[https://peiseka.com/jianbianse.html](https://peiseka.com/jianbianse.html)
