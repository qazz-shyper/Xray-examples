准备
```
cat > /etc/sysctl.d/ip_forward.conf << EOF
net.ipv4.ip_forward=1
EOF
```

```
sysctl -p /etc/sysctl.d/ip_forward.conf
```

安装
```
apt install -y iptables-persistent
```

添加
```
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j DNAT --to-destination 目标网站的IP:80
iptables -t nat -A PREROUTING -i eth0 -p udp --dport 443 -j DNAT --to-destination 目标网站的IP:443
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

保存
```
netfilter-persistent save
```

查看
```
iptables -t nat -nL --line
```

删除
```
iptables -t nat -D PREROUTING 1
```

```
iptables -t nat -D POSTROUTING 1
```
