### 注意：

:exclamation:gRPC/H2 建议在有优化回程路由（如 CN2-GIA、AS9929/AS10099、CMI/CMIN2、AS4837 等）的VPS上使用。并且VPS所在的地区距离你的位置越近越好。即使你的VPS满足以上条件，仍然不能避免断流现象。建议参考ChatGPT的回答优化系统内核参数。除此以外，你可以参考[文档](https://xtls.github.io/Xray-docs-next/config/transports/h2.html#httpobject)，使用健康检查功能。

<details><summary>点击查看</summary><br>

```
cat > /etc/sysctl.conf << EOF
net.core.somaxconn = 65535
net.ipv4.tcp_max_syn_backlog = 65535
net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_tw_reuse = 1
net.ipv4.tcp_fin_timeout = 30
net.ipv4.tcp_keepalive_time = 1200
net.ipv4.tcp_keepalive_probes = 5
net.ipv4.tcp_keepalive_intvl = 15
net.ipv4.tcp_slow_start_after_idle = 0
net.ipv4.tcp_mtu_probing = 1
net.ipv4.tcp_max_syn_backlog = 8192
net.ipv4.tcp_max_tw_buckets = 5000
net.core.default_qdisc = fq
net.ipv4.tcp_congestion_control = bbr
EOF
```

```
sysctl -p
```

</details>

### v2rayN - V6.19及以上版本 配置示例

<details><summary>点击查看</summary><br>

| 名称 | 值 |
| :--- | :--- |
| 地址 | 服务端的 IP |
| 端口 | 443 |
| 用户ID | chika |
| 流控 | 留空 |
| 传输协议 | h2 |
| 传输层安全 | reality |
| SNI | `www.lovelive-anime.jp` |
| Fingerprint | chrome |
| PublicKey | Z84J2IelR9ch3k8VtlVhhs5ycBUlXA7wHBWcBrjqnAw |
| ShortId | 6ba85179e30d4fc2 |
| SpiderX | 留空 |

</details>

### v2rayNG - V1.8.1及以上版本 配置示例

<details><summary>点击查看</summary><br>

| 名称 | 值 |
| :--- | :--- |
| 地址(address) | 服务端的 IP |
| 端口(prot) | 443 |
| 用户ID(id) | chika |
| 流控(flow) | 留空 |
| 加密方式(encryption) | none |
| 传输协议(network) | h2 |
| 伪装类型 | --- |
| 伪装域名(host) | 留空 |
| path | 留空 |
| 传输层安全(tls) | reality |
| SNI | `www.lovelive-anime.jp` |
| Fingerprint | chrome |
| PublicKey | Z84J2IelR9ch3k8VtlVhhs5ycBUlXA7wHBWcBrjqnAw |
| ShortID | 6ba85179e30d4fc2 |
| SpiderX | 留空 |

</details>

### PassWall 配置示例

<details><summary>点击查看</summary><br>

| 名称 | 值 |
| :--- | :--- |
| 类型 | Xray |
| 传输协议 | VLESS |
| 地址（支持域名） | 服务端的 IP |
| 端口 | 443 |
| 加密方式 | none |
| ID | chika |
| TLS | 勾上 |
| flow | 停用 |
| REALITY | 勾上 |
| 域名 | `www.lovelive-anime.jp` |
| 公钥 | Z84J2IelR9ch3k8VtlVhhs5ycBUlXA7wHBWcBrjqnAw |
| Short Id | 6ba85179e30d4fc2 |
| Spider X | 留空 |
| 指纹伪造 | chrome |
| 传输协议 | HTTP/2 |
| HTTP/2 主机名 | 留空 |
| HTTP/2 路径 | 留空 |
| 健康检查 | 不勾 |
| MUX | 不勾 |

</details>

### ShadowSocksR Plus+ 配置示例

<details><summary>点击查看</summary><br>

| 名称 | 值 |
| :--- | :--- |
| 服务器节点类型 | V2Ray/Xray |
| V2Ray/XRay 协议 | VLESS |
| 服务器地址 | 服务端的 IP |
| 端口 | 443 |
| Vmess/VLESS ID (UUID) | chika |
| VLESS 加密 | none |
| 传输协议 | HTTP/2 |
| HTTP/2 主机名 | 留空 |
| HTTP/2 路径 | 留空 |
| H2/gRPC 健康检查 | 不勾 |
| TLS | 不勾 |
| REALITY | 勾上 |
| Public key | Z84J2IelR9ch3k8VtlVhhs5ycBUlXA7wHBWcBrjqnAw |
| Short ID | 6ba85179e30d4fc2 |
| spiderX | 留空 |
| 指纹伪造 | chrome |
| TLS 主机名 | `www.lovelive-anime.jp` |
| Mux | 不勾 |
| 启用自动切换 | 不勾 |
| 本地端口 | 1234 |

</details>
