# 更换域名

之前在namecheap买的域名满一年了，告诉我续费需要20美刀，我可去你奶奶的。于是就查了其他域名，.xyz域名物美价廉只需1刀，那当然是要买买买。

买完之后就是需要换域名，好久不操作vps，今天花了时间研究了以下，最后还算顺利，记录下来过程。

## 设置DNS

这个比较简单，把旧的A记录记下来，原样改为新的A记录即可。

## 签发证书

需要HTTPS访问，SSL证书必不可少。之前用的是acme，想要知道怎么用，需要到acme在的目录下运行

```
./acme.sh --help
```

在签发之前，需要停止nginx，因为acme验证的时候需要用到80端口，nginx运行的时候会提示80端口被占用。

```
service nginx stop

./acme.sh --issue --standalone -d example.com
```

签发成功之后，会在acme目录下面生成以域名命名的文件夹，里面有一大串证书文件，大概有这些。

```
example.com.cer example.com.conf example.com.csr example.com.csr.conf example.com.key ca.cer fullchain.cer
```

## 修改nginx设置

原理是在nginx的相应位置替换证书就可以了。

找到nginx的设置目录

```
nginx -t

nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
```

在nginx设置里面找到下面两行

```
ssl_certificate xxx.cer;

ssl_certificate_key xxx.key;
```

其中替换为签发的证书中的.cer和.key文件

```s
ssl_certificate .../example.com/fullchain.cer;

ssl_certificate_key .../example.com/example.com.key;
```

然后在nginx中的旧域名位置更改为新域名。

重启nginx

```
service nginx start
```





