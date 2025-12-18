# 安装Node运行环境

前往Node官网，下载Linux程序：[https://nodejs.org/en/download/current](https://nodejs.org/en/download/current)

解压命令：

```
tar -xvf node.tar.xz

mv node.tar.xz node // 重命名，强迫症福音
```

测试当前是否安装成功：

```
./node -v
```

修改环境变量（没有Node应用可以不做）

```
sudo vim /etc/profile

export NODE_HOME= Node全路径
export PATH=$PATH:$NODE_HOME/bin
export NODE_PATH=$NODE_HOME/lib/node_modules

source /etc/profile  // 刷新配置
```

添加软链（与上面环境变量二选一）

```
ln -s Node全路径/bin/node /usr/local/bin/node
ln -s Node全路径/bin/npm /usr/local/bin/npm
```

# 安装substore

下载subStore：[https://github.com/sub-store-org/Sub-Store/releases](https://github.com/sub-store-org/Sub-Store/releases)

编辑系统服务：

```
vim /etc/systemd/system/sub-store.service

[Unit]
Description=Sub-Store
After=network-online.target
Wants=network-online.target systemd-networkd-wait-online.service

[Service]
Type=simple
Restart=on-failure
Environment="SUB_STORE_BACKEND_API_PORT=4000" // 启动端口
RestartSec=5s
ExecStart=Node全路径 Sub-Store全路径

[Install]
WantedBy=multi-user.target
```

```
// 服务启动
systemctl start sub-store.service  

// 开机自启动
systemctl enable sub-store.service  

// 查看运行状态
systemctl status sub-store.service  

// 重载 systemctl
systemctl daemon-reload
```

# 访问Web

即可使用：[https://sub-store.vercel.app/subs](https://sub-store.vercel.app/subs)

晓风备用站：[https://substore.byxiao.top/](https://substore.byxiao.top/)

# 常见脚本

节点超时：
https://raw.githubusercontent.com/Keywos/rule/main/pname.js

节点重命名：
https://raw.githubusercontent.com/Keywos/rule/main/rename.js

# 参考网站

> [https://www.evan888.top/1974/]()
>
> [https://surge.tel/08/2930/]()
>
> [https://isedu.top/index.php/archives/194/]()
>
> [https://1024.day/d/1899]()
