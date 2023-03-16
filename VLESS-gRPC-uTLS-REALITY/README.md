### v2rayN - V6.17及以上版本 配置示例

<details><summary>点击查看</summary><br>

| 名称 | 值 |
| :--- | :--- |
| 地址 | 服务端的域名 或 IP |
| 端口 | 443 |
| 用户ID | chika |
| 流控 | 留空 |
| 传输协议 | grpc |
|  | multi |
| 路径 | grpc |
| 传输层安全 | reality |
| SNI | `www.lovelive-anime.jp` |
| Fingerprint | chrome |
| PublicKey | Z84J2IelR9ch3k8VtlVhhs5ycBUlXA7wHBWcBrjqnAw |
| ShortId | 6ba85179e30d4fc2 |
| SpiderX | / |

![1](https://user-images.githubusercontent.com/88967758/225035376-bb5a3f63-6906-4b13-877f-c6f1433a02d9.png)

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
| 传输协议(network) | grpc |
| gRPC 传输模式 (mode) | multi |
| 伪装域名(host) | 留空 |
| path | grpc |
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
| 传输协议 | grpc |
| gRPC 服务名称 | grpc |
| 传输层加密 | tls |
| 服务器名称指标 | `www.lovelive-anime.jp` |
| 应用层协议协商 | 留空 |
| 证书（链） | 留空 |
| 允许不安全的连接 | 不选 |
| uTLS fingerprint | chrome |
| Reality Public Key | Z84J2IelR9ch3k8VtlVhhs5ycBUlXA7wHBWcBrjqnAw |
| Reality ShortId | 6ba85179e30d4fc2 |

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
| 传输协议 | gRPC |
| ServiceName | grpc |
| gRPC 传输模式 | multi |
| 健康检查 | 不勾 |
| 初始窗口大小 | 0 |
| MUX | 不勾 |

</details>

### Clash Meta Kernel 配置示例

<details><summary>点击查看</summary><br>

```
  - name: gRPC-REALITY
    type: vless
    server: 服务端的域名 或 IP
    port: 443
    uuid: chika
    network: grpc
    tls: true
    udp: true
    flow: null
    servername: www.lovelive-anime.jp
    grpc-opts:
      grpc-service-name: grpc
    reality-opts:
      public-key: Z84J2IelR9ch3k8VtlVhhs5ycBUlXA7wHBWcBrjqnAw
      short-id: 6ba85179e30d4fc2
    client-fingerprint: chrome
```

</details>
