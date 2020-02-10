---
title: Quickly Configure Samba
date: 2020-02-04 12:12:23
tags:
---
# 在Centos 7中快速部署Samba
此时的系统软件版本是：
>[root@I ~]# cat /etc/redhat-release 
CentOS Linux release 7.6.1810 (Core)

快速重启和查看状态的快捷命令设定：
>[root@I liyuanblg]# cat >>/etc/bashrc <<EOF

        alias resmb='systemctl restart smb'
        alias stsmb='systemctl status smb'
        EOF
打开Samba的配置文件进行配置：
>[root@I liyuanblg]# vim /etc/samba/smb.conf


        [global]
            workgroup = Fresh
            #工作组
            security = user
            #访问策略
            passdb backend = tdbsam
            #密码验证数据库
            log file = /var/log/samba/log.%m
            #日志文件位置
            max log size = 50
            #日志文件最大大小50KB
            username map = /etc/samba/smbusers
            #用户名映射

        [homes]
            comment = home directories
            valid users = %S
            #有效用户
            writable = yes
            #开启写权限
            browseable = No
        [blog io]
            path = /root/liyuanblg
            valid users = root
            read only = no

> + **任何用户在使用用户名和密码登录Smaba服务时必须使用*`smbpasswd [username]`*来为用户设置专用于Samba的登陆密码。**

 ![](/images/FK.jpeg)

***
<liyanccc@gmail.com>
