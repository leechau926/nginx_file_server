这篇文章将指导如何在Debian系统下搭建简易的文件服务器

安装nginx
===
根据 https://nginx.org/en/docs/install.html 对于**Debian**系统

在root用户下，执行

Install the prerequisites: 

>apt install curl gnupg2 ca-certificates lsb-release

set up the apt repository for stable nginx packages：

>echo "deb http://nginx.org/packages/debian `lsb_release -cs` nginx" | tee tee /etc/apt/sources.list.d/nginx.list

import an official nginx signing key so apt could verify the packages authenticity:

>curl -fsSL https://nginx.org/keys/nginx_signing.key | apt-key add -

Verify that you now have the proper key: 

>apt-key fingerprint ABF5BD827BD9BF62

The output should contain the full fingerprint 573B FD6B 3D8F BC64 1079 A6AB ABF5 BD82 7BD9 BF62 as follows: 

>pub   rsa2048 2011-08-19 [SC] [expires: 2024-06-14]
      573B FD6B 3D8F BC64 1079  A6AB ABF5 BD82 7BD9 BF62
uid   [ unknown] nginx signing key <signing-key@nginx.com>

install nginx

>apt update
>apt install nginx

#配置nginx
运行
>ps -ef | grep nginx
可以看出




