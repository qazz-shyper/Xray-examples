使用 **waro-go**，注册warp，导出wireguard配置

```
mkdir warp && curl -sLo ./warp/warp https://gitlab.com/ProjectWARP/warp-go/-/releases/v1.0.8/downloads/warp-go_1.0.8_linux_amd64.tar.gz && tar -xzf ./warp/warp -C ./warp && cp ./warp/warp-go . && chmod 0755 warp-go && rm -r warp && ./warp-go --register && ./warp-go -export-singbox wireguard.json
```

打开 **wireguard.json**，复制"private_key"的值，粘贴到"secretKey": "",处，复制"reserved"的值，粘贴到"reserved":[0, 0, 0],处

**"outbounds"**
```
        {
            "protocol": "wireguard",
            "settings": {
                "secretKey": "",
                "address": [
                    "172.16.0.2/32"
                ],
                "peers": [
                    {
                        "publicKey": "bmXOC+F1FxEMF9dyiK2H5/1SUtzH0JuVo51h2wPfgyo=",
                        "allowedIPs": [
                            "0.0.0.0/0"
                        ],
                        "endpoint": "engage.cloudflareclient.com:2408"
                    }
                ],
                "reserved":[0, 0, 0],
                "mtu": 1280
            },
            "tag": "wireguard"
        }
```

编辑 **/usr/local/etc/xray/config.json**，按需增加 **"routing"**，**"outbounds"**，**"inbounds"** 的内容（注意检查json格式），输入 `systemctl restart xray` 重启Xray，访问bgp.he.net查看是否为Cloudflare的IP

**"routing"**
```
        "domainStrategy": "IPIfNonMatch",
        "rules": [
            {
                "type": "field",
                "domain": [
                    "bgp.he.net",
                    "geosite:openai"
                ],
                "outboundTag": "wireguard"
            },
            {
                "type": "field",
                "ip": [
                    "geoip:cn"
                ],
                "outboundTag": "wireguard"
            }
        ]
```

**"inbounds"**
```
            "sniffing": {
                "enabled": true,
                "destOverride": [
                    "http",
                    "tls"
                ]
            }
```

:exclamation:配置示例用 **VLESS-XTLS-uTLS-REALITY** 举例，如需改用其它协议组合，请自行参照修改。

```
{
    "log": {
        "loglevel": "warning"
    },
    "routing": {
        "domainStrategy": "IPIfNonMatch", // 建议使用此参数
        "rules": [
            {
                "type": "field",
                "domain": [
                    "bgp.he.net",
                    "geosite:openai"
                ],
                "outboundTag": "wireguard"
            },
            {
                "type": "field",
                "ip": [
                    "geoip:cn"
                ],
                "outboundTag": "wireguard"
            }
        ]
    },
    "inbounds": [
        {
            "listen": "0.0.0.0",
            "port": 443,
            "protocol": "vless",
            "settings": {
                "clients": [
                    {
                        "id": "chika",
                        "flow": "xtls-rprx-vision"
                    }
                ],
                "decryption": "none"
            },
            "streamSettings": {
                "network": "tcp",
                "security": "reality",
                "realitySettings": {
                    "show": false,
                    "dest": "www.lovelive-anime.jp:443",
                    "xver": 0,
                    "serverNames": [
                        "www.lovelive-anime.jp"
                    ],
                    "privateKey": "2KZ4uouMKgI8nR-LDJNP1_MHisCJOmKGj9jUjZLncVU",
                    "shortIds": [
                        "6ba85179e30d4fc2"
                    ]
                }
            },
            "sniffing": { // 建议使用此参数
                "enabled": true,
                "destOverride": [
                    "http",
                    "tls"
                ]
            }
        }
    ],
    "outbounds": [
        {
            "protocol": "freedom",
            "tag": "direct"
        },
        {
            "protocol": "blackhole",
            "tag": "block"
        },
        {
            "protocol": "wireguard",
            "settings": {
                "secretKey": "sOL9HjJEqi7Xd0gtm6C2CWoDtsxXXYpJyj10Pi10KWM=",
                "address": [
                    "172.16.0.2/32"
                ],
                "peers": [
                    {
                        "publicKey": "bmXOC+F1FxEMF9dyiK2H5/1SUtzH0JuVo51h2wPfgyo=",
                        "allowedIPs": [
                            "0.0.0.0/0"
                        ],
                        "endpoint": "engage.cloudflareclient.com:2408"
                    }
                ],
                "reserved":[19, 152, 142],
                "mtu": 1280
            },
            "tag": "wireguard"
        }
    ],
    "policy": {
        "levels": {
            "0": {
                "handshake": 2,
                "connIdle": 120
            }
        }
    }
}
```
