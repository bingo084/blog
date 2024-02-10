---
title: 配置 Linux 下的 FTP 服务
date: 2024-02-10T21:41:28+08:00
draft: true
keywords:
  - ftp
  - vsftpd
  - linux
tags:
  - ftp
  - linux
categories:
  - config
resources:
  - name: featured-image
    src: images/featured-image.png
---

这篇文章记录了我在 Linux 下使用 [vsftpd] 配置 FTP 服务的过程。

<!--more-->

## 安装

```bash
pacman -S vsftpd
```

## 配置

`vsftpd` 的配置文件位于 `/etc/vsftpd.conf`，默认自带大量注释说明。
下面挑一些需要修改的部分说明，更详细的说明参阅 [vsftpd.conf(5)]

```text
# 开启本地用户登录
local_enable=YES
# 允许上传
write_enable=YES
```

## 启动（并设置开机自启动）

```bash
sudo systemctl enable --now vsftpd
```

{{< admonition note >}}
每次修改配置文件后都需要重启服务。
{{< /admonition >}}

## 测试

### 安装 inetutils 包

```bash
pacman -S inetutils
```

### 使用 `ftp` 命令测试

```bash
ftp localhost
```

根据提示输入正确的用户名和密码后即可登录

```bash
~ > ftp localhost  
Connected to localhost.
220 (vsFTPd 3.0.5)
Name (localhost:bingo): 
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
drwxr-xr-x    2 1000     1000         4096 Jan 24 15:38 Desktop
drwxr-xr-x    5 1000     1000         4096 Feb 10 06:37 Documents
drwxr-xr-x    8 1000     1000         4096 Feb 10 13:52 Downloads
drwxr-xr-x    2 1000     1000         4096 Jan 24 15:38 Music
drwxr-xr-x    4 1000     1000         4096 Sep 27 13:40 Pictures
drwxr-xr-x    2 1000     1000         4096 Jan 24 15:38 Public
drwxr-xr-x    2 1000     1000         4096 Jan 24 15:38 Videos
226 Directory send OK.
ftp>
```

查看本机 ip，在局域网内的其他设备使用该 ip 即可访问。

## 参考

> [ArchWiki]、[vsftpd 配置文件]

[vsftpd]: https://security.appspot.com/vsftpd.html "Probably the most secure and fastest FTP server for UNIX-like systems."
[vsftpd.conf(5)]: https://man.archlinux.org/man/vsftpd.conf.5
[ArchWiki]: https://wiki.archlinuxcn.org/wiki/Very_Secure_FTP_Daemon
[vsftpd 配置文件]: https://gnu-linux.readthedocs.io/zh/latest/Chapter02/90_vsftpd.html
