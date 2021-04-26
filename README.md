# 10M Concurrent Websockets

Originally found at [10M Concurrent Websockets](http://goroutines.com/10m)

**I'm not the author of this code/post, this is just a refactored version to support go modules.**

### How to run

Server:

```bash
apt-get update
apt-get install -y redis-server
echo "bind *" >> /etc/redis/redis.conf
systemctl restart redis-server
sysctl -w fs.file-max=11000000
sysctl -w fs.nr_open=11000000
ulimit -n 11000000
sysctl -w net.ipv4.tcp_mem="100000000 100000000 100000000"
sysctl -w net.core.somaxconn=10000
sysctl -w net.ipv4.tcp_max_syn_backlog=10000
go build -o bin/server cmd/server/main.go
bin/server
```

Client:

```bash
sysctl -w fs.file-max=11000000
sysctl -w fs.nr_open=11000000
ulimit -n 11000000
sysctl -w net.ipv4.ip_local_port_range="1025 65535"
sysctl -w net.ipv4.tcp_mem="100000000 100000000 100000000"
go build -o bin/client cmd/client/main.go
bin/client <ip address> <number of connections>
```