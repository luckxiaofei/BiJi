被控制端

```shell
[common]
server_addr = 47.115.124.84
server_port = 7000
token = 12345678

[p2p_vnc]
type = xtcp
sk = abcdefg_vnc
local_ip = 127.0.0.1
local_port = 5900

[p2p_ssh]
type = stcp
sk = abcdefg_ssh
local_ip = 127.0.0.1
local_port = 22
```



控制端

```
[common]
server_addr = 47.115.124.84
server_port = 7000
token = 12345678

[p2p_vnc_visitor]
type = xtcp
role = visitor
server_name = p2p_vnc
sk = abcdefg_vnc
bind_addr = 127.0.0.1
bind_port = 6000
use_compression = true

[p2p_ssh_visitor]
type = xtcp
role = visitor
server_name = p2p_ssh
sk = abcdefg_ssh
bind_addr = 127.0.0.1
bind_port = 6001

[web]
type = http
local_port = 8082
custom_domains = www.core.com


scp -r  /Users/luck/Downloads/frp_0.31.2_linux_386.tar.gz root@43.226.151.160:/home/

./frpc -c ./frpc.ini
./frpc reload -c ./frpc.ini
./frpc status -c ./frpc.ini

http://47.115.124.84:6000/static/

http://www.core.com:8080
```

