# v2ray-config.json

rely on https://www.v2ray.com/  

> **speed rank**
> 1. [ws](https://github.com/pphui8/v2ray-config.json/blob/main/README.md/#ws)
> 2. [mkcp](https://github.com/pphui8/v2ray-config.json/blob/main/README.md/#mkcp)
> 3. [tcp](https://github.com/pphui8/v2ray-config.json/blob/main/README.md/#tcp)
> 4. [shadowsocks](https://github.com/pphui8/v2ray-config.json/blob/main/README.md/#shadowsocks)

## ws
```json
{
  "inbounds": [
    {
      "port": xxxx,
      "protocol": "vmess",
      "settings": {
        "clients": [
          {
            "id": "xxxxxxxxxxxxxx",
            "alterId": 64
          }
        ]
      },
      "streamSettings": {
        "network":"ws"
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

## mkcp  
```json
{
  "inbounds": [
    {
      "port": xxxx,
      "protocol": "vmess",
      "settings": {
        "clients": [
          {
            "id": "xxxxxxxxxxxxxxxxx",
            "alterId": 64
          }
        ]
      },
      "streamSettings": {
        "network": "mkcp",
        "kcpSettings": {
          "uplinkCapacity": 5,
          "downlinkCapacity": 100,
          "congestion": true,
          "header": {
            "type": "none"
          }
        }
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
