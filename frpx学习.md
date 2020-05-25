### frp常用指令

```shell
#启动客户端
./frps -c ./frps.ini
#启动服务端
./frps -c ./frps.ini
#重启命令
./frpc reload -c ./frpc.ini
#客户端查看代理状态
./frpc status -c ./frpc.ini

```



```shell
[common]
server_addr = 47.115.124.84
server_port = 7000
admin_addr = 127.0.0.1
admin_port = 7400
token = 12345678
protocol = kcp

[p2p_vnc]
type = stcp
sk = abcdefg_vnc
local_ip = 127.0.0.1
local_port = 5900
use_compression = true


[p2p_ssh]
type = stcp
sk = abcdefg_ssh
local_ip = 127.0.0.1
local_port = 22
use_compression = true


[test_static_file]
type = tcp
remote_port = 6001
plugin = static_file
# 要对外暴露的文件目录
plugin_local_path = /Users/fei
# 访问 url 中会被去除的前缀，保留的内容即为要访问的文件路径
plugin_strip_prefix = static
plugin_http_user = abc
plugin_http_passwd = abc
use_compression = true

```

```
[common]
server_addr = 47.115.124.84
server_port = 7000
admin_addr = 127.0.0.1
admin_port = 7400
token = 12345678
protocol = kcp


[vnc]
type = tcp
local_ip = 127.0.0.1
local_port = 5900
remote_port = 6000
use_compression = true


[p2p_vnc]
type = stcp
sk = abcdefg_vnc
local_ip = 127.0.0.1
local_port = 5900
use_compression = true



[p2p_ssh]
type = stcp
sk = abcdefg_ssh
local_ip = 127.0.0.1
local_port = 22
use_compression = true


[test_static_file]
type = tcp
remote_port = 6001
plugin = static_file
# 要对外暴露的文件目录
plugin_local_path = /Users/fei
# 访问 url 中会被去除的前缀，保留的内容即为要访问的文件路径
plugin_strip_prefix = static
plugin_http_user = abc
plugin_http_passwd = abc
use_compression = true
```

