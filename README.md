# v2ray-config.json

> rely on https://www.v2ray.com/

## tcp trans
```json
{
    "inbounds": [{
      "port": xxxx,
      "protocol": "vmess",
      "settings": {
        "clients": [
          {
            "id": "xxxx",
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
            "id": "xxxx",
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
