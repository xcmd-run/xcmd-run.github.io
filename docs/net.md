# 网络

## 查看ip
- ipconfig
- ip addr
## 配置ip
- net-tools
```bash
$ sudo ifconfig eth1 10.0.0.1/24
$ sudo ifconfig eth1 up
```
- iprotue2
```bash
$ sudo ip addr add 10.0.0.1/24 dev eth1
$ sudo ip link set up eth1
```