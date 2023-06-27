# Hy-tutorial

```sh
wget https://github.com/apernet/hysteria/releases/download/v1.3.5/hysteria-linux-amd64-avx
chmod +x hysteria-linux-amd64-avx
sysctl -w net.core.rmem_max=16777216
sysctl -w net.core.wmem_max=16777216
```

服务端配置config.json：
```json
{
  "listen": ":[端口]",
  "protocol": "udp",
  "acme": {
    "domains": [
      "[域名]"
    ],
    "email": "hacker@gmail.com"
  },
  "auth": {
    "mode": "passwords", 
    "config": ["[密码]"]
  },
  "resolve_preference": "46"
}
```

```
vi /lib/systemd/system/hysteria.service
```
输入内容：
```sh
[Unit]
Description=Hysteria
After=network.target network-online.target nss-lookup.target
 
[Service]
Restart=on-failure
Type=simple
ExecStart=/root/hysteria-linux-amd64-avx -config /root/config.json server
 
[Install]
WantedBy=multi-user.target
```

```
systemctl daemon-reload
systemctl enable hysteria
systemctl start hysteria
```

客户端配置：

首先在[点我](https://github.com/apernet/hysteria/releases/download/v1.3.5/hysteria-windows-amd64-avx.exe)下载到v2ray目录下

然后新建一个config.json文档：
```json
{
  "server": "[IP地址]:[同服务端端口]",
  "auth_str": "[同服务端密码]", 
  "up_mbps": 120, //上传速度，根据实际情况
  "down_mbps": 200,//下载速度，根据实际情况
  "insecure": false,
  "retry": 3,
  "socks5": {
    "listen": "127.0.0.1:10808"
  },
  "http": {
    "listen": "127.0.0.1:10809"
  },
  "server_name": "[同服务端域名]",
  "fast_open": true,
  "resolve_preference": "46"
}
```
