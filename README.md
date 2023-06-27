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
