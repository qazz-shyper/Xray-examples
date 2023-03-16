### v2rayN - V6.17及以上版本 配置示例

<details><summary>点击查看</summary><br>

| 名称 | 值 |
| :--- | :--- |
| 地址 | VPS的 IP 或你设置的域名（非服务端 "dest" 项填的目标网站网址） |
| 端口 | 443 |
| 用户ID | chika |
| 流控 | 留空 |
| 传输协议 | h2 |
| 传输层安全 | reality |
| SNI | `www.lovelive-anime.jp` |
| Fingerprint | chrome |
| PublicKey | Z84J2IelR9ch3k8VtlVhhs5ycBUlXA7wHBWcBrjqnAw |
| ShortId | 6ba85179e30d4fc2 |
| SpiderX | / |

![1](https://user-images.githubusercontent.com/88967758/224341358-e30ace37-4da6-4e80-b630-e4a7246667fb.png)

</details>

### v2rayNG - V1.8.0及以上版本 配置示例

<details><summary>点击查看</summary><br>

| 名称 | 值 |
| :--- | :--- |
| 地址(address) | 服务端的域名 或 IP |
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
| Alpn | 留空 |
| PublicKey | Z84J2IelR9ch3k8VtlVhhs5ycBUlXA7wHBWcBrjqnAw |
| ShortID | 6ba85179e30d4fc2 |
| SpiderX | / |

</details>

### NekoBox 配置示例

<details><summary>点击查看</summary><br>

| 名称 | 值 |
| :--- | :--- |
| 服务器 | 服务端的域名 或 IP |
| 服务器端口 | 443 |
| 用户ID | chika |
| Flow (VLESS Sub-protocol) | 留空 |
| 包编码 | xudp |
| 传输协议 | http |
| HTTP 主机 | h2 |
| HTTP 路径 | 留空 |
| 传输层加密 | tls |
| 服务器名称指标 | `www.lovelive-anime.jp` |
| 应用层协议协商 | 留空 |
| 证书（链） | 留空 |
| 允许不安全的连接 | 不选 |
| uTLS fingerprint | chrome |
| Reality Public Key | Z84J2IelR9ch3k8VtlVhhs5ycBUlXA7wHBWcBrjqnAw |
| Reality ShortId | 6ba85179e30d4fc2 |

需要在服务端配置中添下面字段
```
                "httpSettings": {
                    "host": ["h2"]
                }
```

</details>

### Pass Wall 配置示例

<details><summary>点击查看</summary><br>

| 名称 | 值 |
| :--- | :--- |
| 类型 | Xray |
| 传输协议 | VLESS |
| 地址（支持域名） | 服务端的域名 或 IP |
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

</details>
