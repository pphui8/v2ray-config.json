# transit setting(by nginx)
```conf
stream {
  server {
  listen: port;
  proxy_pass: ip:port;
  }
}
```

# v2ray-config.json

rely on https://www.v2ray.com/  
> /usr/local/etc/v2ray/config.json  

> **speed rank**
> 1. [ws](https://github.com/pphui8/v2ray-config.json/blob/main/README.md/#ws)
> 2. [mkcp](https://github.com/pphui8/v2ray-config.json/blob/main/README.md/#mkcp)
> 3. [tcp](https://github.com/pphui8/v2ray-config.json/blob/main/README.md/#tcp)
> 4. [shadowsocks](https://github.com/pphui8/v2ray-config.json/blob/main/README.md/#shadowsocks)

## ws(with tls on)
```json
{
  "inbounds": [
    {
        "port": xxxx,
        "listen":"127.0.0.1",
        "protocol": "vmess",
        "settings": {
            "clients": [
            {
                "id": "xxxxxxxxxxxxxxxxxxxxxxxxxxx",
                "alterId": 64
            }
            ]
        },
        "streamSettings": {
                "network": "ws",
                "wsSettings": {
                "path": "/ray"
            }
        }
    },
  "outbounds": [
    {
      "protocol": "freedom",
      "settings": {}
    }
  ]
}
```

## mkcp  
```json
{
  "log": {
    "access": "/var/log/v2ray/access.log",
    "error": "/var/log/v2ray/error.log",
    "loglevel": "warning"
  },
  "dns": {},
  "stats": {},
  "inbounds": [
    {
      "port": xxxx,
      "protocol": "vmess",
      "settings": {
        "clients": [
          {
            "id": "xxxxxxxxx",
            "alterId": 64
          }
        ]
      },
      "tag": "in-0",
      "streamSettings": {
        "network": "kcp",
        "security": "none",
        "kcpSettings": {}
      }
    }
  ],
  "outbounds": [
    {
      "tag": "direct",
      "protocol": "freedom",
      "settings": {}
    },
    {
      "tag": "blocked",
      "protocol": "blackhole",
      "settings": {}
    }
  ],
  "routing": {
    "domainStrategy": "AsIs",
    "rules": [
      {
        "type": "field",
        "ip": [
          "geoip:private"
        ],
        "outboundTag": "blocked"
      }
    ]
  },
  "policy": {},
  "reverse": {},
  "transport": {}
}
```

## tcp trans
```json
{
    "inbounds": [{
      "port": xxxx,
      "protocol": "vmess",
      "settings": {
        "clients": [
          {
            "id": "xxxxxxxxxxxxxx",
            "level": 1,
            "alterId": 64
          }
        ]
      }
    }],
    "outbounds": [{
      "protocol": "freedom",
      "settings": {}
    },{
      "protocol": "blackhole",
      "settings": {},
      "tag": "blocked"
    }],
    "routing": {
      "rules": [
        {
          "type": "field",
          "ip": ["geoip:private"],
          "outboundTag": "blocked"
        }
      ]
    }
  }
```

## shadowsocks
```shadowsocks
{
  "inbounds": [
    {
      "port": xxxx,
      "protocol": "shadowsocks",
      "settings": {
        "method": "aes-128-gcm",
        "ota": true,
        "password": "xxxxxxxxxxxxx"
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom",  
      "settings": {}
    }
  ]
}
```
4c3fcd79-2966-479b-cfdc-497f9311194b
