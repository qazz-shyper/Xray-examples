使用 **warp-go**，注册warp，导出wireguard配置

```
curl -Lso- https://gitlab.com/ProjectWARP/warp-go/-/releases/v1.0.8/downloads/warp-go_1.0.8_linux_amd64.tar.gz | tar -zxf- warp-go && chmod +x warp-go && ./warp-go -register > /dev/null && ./warp-go -export-singbox wg.json > /dev/null && grep -Eo --color=never '"2606:4700:[0-9a-f:]+/128"|"private_key":"[0-9a-zA-Z\/+]+="|"reserved":\[[0-9]+(,[0-9]+){2}\]' wg.json && rm warp-go warp.conf wg.json
```

- 复制输出的 IPv6 地址，替换下面配置中的 `2606:4700::/128`
- 复制输出的 `private_key` 值，粘贴到 `secretKey` 后的`""`中
- 复制输出的 `reserved` 值，粘贴到 `reserved` 后的`[]`中

**"outbounds"**
```jsonc
        {
            "protocol": "wireguard",
            "settings": {
                "secretKey": "", // 粘贴你的 "private_key" 值
                "address": [
                    "172.16.0.2/32"，
                    "2606:4700::/128" // 粘贴你获得的 warp IPv6 地址
                ],
                "peers": [
                    {
                        "publicKey": "bmXOC+F1FxEMF9dyiK2H5/1SUtzH0JuVo51h2wPfgyo=",
                        "allowedIPs": [
                            "0.0.0.0/0"
                        ],
                        "endpoint": "162.159.192.1:2408"
                    }
                ],
                "reserved":[0, 0, 0], // 粘贴你的 "reserved" 值
                "mtu": 1280
            },
            "tag": "wireguard"
        }
```

编辑 **/usr/local/etc/xray/config.json**，按需增加 **"routing"**，**"inbounds"**，**"outbounds"** 的内容（注意检查json格式），输入 `systemctl restart xray` 重启Xray，访问bgp.he.net查看是否为Cloudflare的IP

**"routing"**
```
        "domainStrategy": "IPIfNonMatch",
        "rules": [
            {
                "type": "field",
                "port": "443",
                "network": "udp",
                "outboundTag": "block"
            },
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
            },
            {
                "type": "field",
                "ip": [
                    "geoip:private"
                ],
                "outboundTag": "block"
            }
        ]
```

**"inbounds"**
```
            "sniffing": {
                "enabled": true,
                "destOverride": [
                    "http",
                    "tls",
                    "quic"
                ]
            }
```

:exclamation:配置示例用 **VLESS-XTLS-uTLS-REALITY** 举例，如需改用其它协议组合，请自行参照修改。

```jsonc
{
    "log": {
        "loglevel": "warning"
    },
    "routing": {
        "domainStrategy": "IPIfNonMatch",
        "rules": [
            {
                "type": "field",
                "port": "443",
                "network": "udp",
                "outboundTag": "block"
            },
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
            },
            {
                "type": "field",
                "ip": [
                    "geoip:private"
                ],
                "outboundTag": "block"
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
            "sniffing": {
                "enabled": true,
                "destOverride": [
                    "http",
                    "tls",
                    "quic"
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
                "secretKey": "", // 粘贴你的 "private_key" 值
                "address": [
                    "172.16.0.2/32"，
                    "2606:4700::/128" // 粘贴你获得的 warp IPv6 地址
                ],
                "peers": [
                    {
                        "publicKey": "bmXOC+F1FxEMF9dyiK2H5/1SUtzH0JuVo51h2wPfgyo=",
                        "allowedIPs": [
                            "0.0.0.0/0"
                        ],
                        "endpoint": "162.159.192.1:2408"
                    }
                ],
                "reserved":[0, 0, 0], // 粘贴你的 "reserved" 值
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
