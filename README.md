```shell
wget https://raw.githubusercontent.com/Argo160/minitiny/main/minitiny.tar.gz

```
```shell
tar -xzf minitiny.tar.gz
```
```shell
nano config.toml
```
in server:
```shell
[server]
bind_addr = "0.0.0.0:3080"
transport = "tcpmux"
token = "token" 
keepalive_period = 75
nodelay = true 
heartbeat = 40 
channel_size = 2048
mux_con = 8
mux_version = 1
mux_framesize = 32768 
mux_recievebuffer = 4194304
mux_streambuffer = 65536 
sniffer = false 
web_port = 2060
sniffer_log = "/root/backhaul.json"
log_level = "info"
ports = ["8080"]
```
out server:
```shell
[client]
remote_addr = "iran ip:3080"
transport = "tcpmux"
token = "token" 
connection_pool = 8
aggressive_pool = false
keepalive_period = 75
dial_timeout = 10
retry_interval = 3
nodelay = true 
mux_version = 1
mux_framesize = 32768 
mux_recievebuffer = 4194304
mux_streambuffer = 65536 
sniffer = false 
web_port = 2060
sniffer_log = "/root/backhaul.json"
log_level = "info"
```
```shell
nano /etc/systemd/system/backhaul.service
```
```shell
[Unit]
Description=Backhaul Reverse Tunnel Service
After=network.target

[Service]
Type=simple
ExecStart=/root/backhaul_premium -c /root/config.toml
Restart=always
RestartSec=3
LimitNOFILE=1048576

[Install]
WantedBy=multi-user.target
```
```shell
sudo systemctl daemon-reload
sudo systemctl enable backhaul.service
sudo systemctl start backhaul.service
```
