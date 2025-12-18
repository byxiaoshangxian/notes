# 安装

> V2RayA 安装参考：https://v2raya.org/docs/prologue/installation/debian/
> 
> Xray 内核参考：https://github.com/XTLS/Xray-install
> 
> V2Ray 内核参考：https://github.com/v2fly/fhs-install-v2ray

# 安装v2rayA

## 添加公钥

```bash
wget -qO - https://apt.v2raya.org/key/public-key.asc | sudo tee /etc/apt/keyrings/v2raya.asc
```

## 添加软件源

```
echo "deb [signed-by=/etc/apt/keyrings/v2raya.asc] https://apt.v2raya.org/ v2raya main" | sudo tee /etc/apt/sources.list.d/v2raya.list
sudo apt update
```

## 安装 V2RayA

```
sudo apt install v2raya xray
```

## 启动 v2rayA

```
sudo systemctl start v2raya.service
```

## 设置开机自动启动

```
sudo systemctl enable v2raya.service
```

# 参考教程：

> https://www.v2rayfree.eu.org/post/v2raya-linux-tutorial/
> 
> https://www.sky350.com/1210.html
> 
> https://pengtech.net/network/v2rayA_install.html
> 
> https://tigress.cc/2023/10/22/V2rayA-Xray
> 
> https://bbs.histb.com/d/2270-qiu-ge-v2rayaan-zhuang-jiao-cheng/9
