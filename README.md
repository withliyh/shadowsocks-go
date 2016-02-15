# shadowsocks-go

兼容原版 shadowsocks-go 并增加以下功能

在多服务器中，指定一个目的地址从特定的服务器访问
比如：

```
    有3台服务器 A、B、C
    A 用作穿墙
    B 用作访问内网资源
    C 用作视频浏览
    可以制定规则 访问 youku.com 时 从 C 服务器访问
```
原理是根据请求的地址在列表中作比较

配置文件举例：

```
{
	"local_port": 7070,
	"server_password": [
		["gfw.xxxx.com:7077", "password", "aes-128-cfb"],
		["127.0.0.1:7077", "password", "aes-128-cfb"],
		["video.xxxx.com:7077", "password", "aes-128-cfb"]
	],
	"server_route":[
		["gfw.txt",	"0",	"2"],
		["local.txt",	"1",	"0"],
		["video.txt",	"2",	"1"]
	]
}
```
server_route 中每一项有3个字段

第一个字段表示规则文件

第二个字段表示使用哪个服务器，按顺序从0开始

第三个字段指定优先级,数字越小优先级越高

规则文件中每个地址一行
例如 local.txt 的内容

192.168.2.100
nexus.sdp.com
192.168.3.100

