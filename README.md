# run-shadowsocks-in-Ubuntu-18
在Ubuntu 18上部署shadowsocks

仅供学习使用。。。

1.安装snap，已安装可跳过：sudo apt install snapd

2.安装shadowsocks：sudo snap install shadowsocks-libev

3.修改配置文件并保存：sudo vi /snap/shadowsocks-libev/config.json

{

    "server":"0.0.0.0",
    
    "server_port":8888,
    
    "local":"127.0.0.1",
    
    "local_port":1080,
    
    "password":"你的密码",
    
    "timeout":60,
    
    "method":"xchacha20-ietf-poly1305",
    
    "fast_open":true
    
 }

4.修改服务配置并保存：sudo vi /etc/systemd/system/shadowsocks-libev.service

[Unit]

Description=Shadowsocks-libev Server

After=network.target



[Service]

Type=simple

ExecStartPre=/bin/sh -c 'ulimit -n 51200'

ExecStart=/snap/bin/shadowsocks-libev.ss-server -c /snap/shadowsocks-libev/config.json -u

Restart=on-abort


[Install]

WantedBy=multi-user.target


5.重新加载配置：sudo systemctl daemon-reload

6.启动服务：sudo systemctl start shadowsocks-libev

7.设置开机自动启动：sudo systemctl enable shadowsocks-libev


