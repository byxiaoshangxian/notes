免费节点池：https://www.bsbb.cc

windows下载：https://github.com/cmliu/SubsCheck-Win-GUI/releases

web地址：https://sub-store.vercel.app?api=http://127.0.0.1:8299

## 相关命令
> https://github.com/beck-8/subs-check
```
# 基础运行
docker run -d \
  --name subs-check \
  -p 8299:8299 \
  -p 8199:8199 \
  -v ./config:/app/config \
  -v ./output:/app/output \
  --restart always \
  ghcr.io/beck-8/subs-check:latest

# 使用代理运行
docker run -d \
  --name subs-check \
  -p 8299:8299 \
  -p 8199:8199 \
  -e HTTP_PROXY=http://192.168.1.1:7890 \
  -e HTTPS_PROXY=http://192.168.1.1:7890 \
  -v ./config:/app/config \
  -v ./output:/app/output \
  --restart always \
  ghcr.io/beck-8/subs-check:latest
```

windows版的docker
```
cd D:\docker\subs-check
docker run -d --name subs-check -p 8299:8299 -p 8199:8199 `
  -v ${PWD}/config:/app/config `
  -v ${PWD}/output:/app/output `
  --restart always ghcr.io/beck-8/subs-check:latest
```

```
sub-urls:
  - "https://raw.githubusercontent.com/firefoxmmx2/v2rayshare_subcription/main/subscription/clash_sub.yaml"
  - "https://raw.githubusercontent.com/Q3dlaXpoaQ/V2rayN_Clash_Node_Getter/refs/heads/main/APIs/sc0.yaml"
  - "https://raw.githubusercontent.com/xiaoji235/airport-free/refs/heads/main/clash/naidounode.txt"
  - "https://raw.githubusercontent.com/mahdibland/SSAggregator/master/sub/sub_merge_yaml.yml"
  - "https://raw.githubusercontent.com/snakem982/proxypool/main/source/clash-meta.yaml"
  - "https://raw.githubusercontent.com/chengaopan/AutoMergePublicNodes/master/list.yml"
  - "https://raw.githubusercontent.com/zhangkaiitugithub/passcro/main/speednodes.yaml"
  - "https://raw.githubusercontent.com/aiboboxx/v2rayfree/refs/heads/main/README.md"
  - "https://raw.githubusercontent.com/peasoft/NoMoreWalls/master/list.meta.yml"
  - "https://raw.githubusercontent.com/anaer/Sub/refs/heads/main/clash.yaml"
  - "https://raw.githubusercontent.com/free18/v2ray/refs/heads/main/c.yaml"
  - "https://raw.githubusercontent.com/peasoft/NoMoreWalls/master/list.yml"
  - "https://raw.githubusercontent.com/Ruk1ng001/freeSub/main/clash.yaml"
  - "https://raw.githubusercontent.com/SoliSpirit/v2ray-configs/main/all_configs.txt"
  - "https://raw.githubusercontent.com/ripaojiedian/freenode/main/clash"
  - "https://raw.githubusercontent.com/go4sharing/sub/main/sub.yaml"
  - "https://raw.githubusercontent.com/actionsfz/v2ray/refs/heads/master/all.yaml"
  - "https://raw.githubusercontent.com/Pawdroid/Free-servers/refs/heads/main/sub"
  - "https://raw.githubusercontent.com/aiboboxx/v2rayfree/refs/heads/main/v2"
  - "https://raw.githubusercontent.com/acymz/AutoVPN/main/data/V2.txt"
  - "https://raw.githubusercontent.com/ggborr/FREEE-VPN/refs/heads/main/6V2ray"
  - "https://raw.githubusercontent.com/Barabama/FreeNodes/main/nodes/wenode.txt"
  - "https://raw.githubusercontent.com/Barabama/FreeNodes/main/nodes/v2rayshare.txt"
  - "https://raw.githubusercontent.com/Barabama/FreeNodes/main/nodes/nodefree.txt"
  - "https://raw.githubusercontent.com/Barabama/FreeNodes/main/nodes/ndnode.txt"
  - "https://raw.githubusercontent.com/Barabama/FreeNodes/main/nodes/clashmeta.txt"
  - "https://raw.githubusercontent.com/xiaoji235/airport-free/main/v2ray/v2rayshare.txt"
  - "https://raw.githubusercontent.com/xiaoji235/airport-free/main/v2ray.txt"
  - "https://raw.githubusercontent.com/xiaoji235/airport-free/main/clash/naidounode.txt"
  - "https://VLESS.fxxk.dedyn.io/auto"
  - "https://raw.githubusercontent.com/Pawdroid/Free-servers/main/sub"
  - "https://raw.githubusercontent.com/aiboboxx/v2rayfree/main/v2"
  - "https://raw.githubusercontent.com/ssrsub/ssr/master/ssrsub"
  - "https://www.liesauer.net/yogurt/subscribe"
  - "https://www.xrayvip.com/free.txt"
  - "https://raw.githubusercontent.com/go4sharing/sub/main/sub.yaml"
  - "https://1.baiproxy.workers.dev/"
  - "https://raw.githubusercontent.com/chengaopan/AutoMergePublicNodes/master/list.yml"  
```

提示词

`修改这个请求，请将data-raw里面的content内容从/app/output/base64.txt文件中读取出来放入请求，并且改写为Shell脚本的形式`
