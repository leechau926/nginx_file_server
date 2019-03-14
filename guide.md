# 安装nginx

根据 https://nginx.org/en/docs/install.html 对于**Debian**系统

在root用户下，执行

Install the prerequisites: 
```shell
apt install curl gnupg2 ca-certificates lsb-release
```
set up the apt repository for stable nginx packages：
```shell
echo "deb http://nginx.org/packages/debian `lsb_release -cs` nginx" | tee /etc/apt/sources.list.d/nginx.list
```
import an official nginx signing key so apt could verify the packages authenticity:
```shell
curl -fsSL https://nginx.org/keys/nginx_signing.key | apt-key add -
```
Verify that you now have the proper key: 
```shell
apt-key fingerprint ABF5BD827BD9BF62
```
The output should contain the full fingerprint 573B FD6B 3D8F BC64 1079 A6AB ABF5 BD82 7BD9 BF62 as follows: 
```shell
pub   rsa2048 2011-08-19 [SC] [expires: 2024-06-14]
      573B FD6B 3D8F BC64 1079  A6AB ABF5 BD82 7BD9 BF62
uid   [ unknown] nginx signing key <signing-key@nginx.com>
```
install nginx
```shell
apt update
apt install nginx
```
# 配置nginx
## 查找nginx安装路径及配置文件路径
运行
```shell
ps -ef | grep nginx
```
输出结果应为
```shell
root       2067      1  0 14:47 ?        00:00:00 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
www-data   2105   2067  0 15:03 ?        00:00:00 nginx: worker process
root       2115    743  0 15:20 pts/0    00:00:00 grep nginx
```
其中 /usr/sbin/nginx 为nginx的程序路径

运行
```shell
/usr/sbin/nginx -t
```
输出结果应为
```shell
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```
其中 /etc/nginx/nginx/conf 为nginx的配置文件

## 修改nginx.conf

```shell
nano /etc/nginx/nginx.conf
```
在http节点下  增加如下 代码：
```
server{
    listen 8888;
    server_name name;
    location / {
        root /home/file;
        access_log on;
        autoindex on;
        }
}
```
重启nginx服务
```shell
/usr/local/nginx/sbin/nginx  -s reload
```
打开 http://ip-address:88888 即可
