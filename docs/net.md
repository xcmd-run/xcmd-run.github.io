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
## 查看网络端口
- netstat命令
```
netstat -an | grep 3306
```

- lsof命令
```
lsof -i:80
```
通过list open file命令可以查看到当前打开文件，在linux中所有事物都是以文件形式存在，包括网络连接及硬件设备。-i参数表示网络链接，:80指明端口号，该命令会同时列出PID。
查看所有进程监听的端口
```
sudo lsof -i -P | grep -i "listen"
```
