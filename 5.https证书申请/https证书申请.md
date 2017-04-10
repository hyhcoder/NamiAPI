# https证书申请

小程序的api请求正式部署上线都需要是https请求, 因此如何给自己的服务器部署https证书也是非常重要的事情.  
本文介绍的是现在易得的两种免费https证书的获取:

## 阿里云,腾讯云等

第一种https免费证书比较容易获得, 应该说服务器端比较容易弄, 就是现在各种国内的云服务商所提供的免费https证书, 以阿里云和腾讯云为主;  
下面以阿里云举例, 腾讯云类似;都可以看官网的说明, 大同小异;  
1. 登陆阿里云的账号, 进入证书服务;  
![](http://omwycd607.bkt.clouddn.com/17-4-9/92345068-file_1491733095779_357f.png)  
2. 点击右侧的购买证书;选择免费型的DV SSL证书;  
![](http://omwycd607.bkt.clouddn.com/17-4-9/22394895-file_1491733185721_11303.png)  
3. 然后对证书进行补全;  
![](http://omwycd607.bkt.clouddn.com/17-4-9/65891661-file_1491733270480_740f.png)  
4. 最后参照阿里云的指引在原域名解析加上一项CNAME解析,完成认证;证书就可以发放了 ;  
5. 下载证书, 根据不同的服务器来进行部署;  
![](http://omwycd607.bkt.clouddn.com/17-4-9/6871841-file_1491733529771_1996.png)  
6. 附上自己nginx的设置;以供参考;

```
server {
    listen 443;
    listen 80;
    server_name demo.xxx.com; #域名
    ssl on;
    ssl_certificate   /etc/nginx/cert/xxx.pem; #pem的位置
    ssl_certificate_key  /etc/nginx/cert/xxx.key;#key的位置
    ssl_session_timeout 5m;
    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;
    location / {
      proxy_pass http://127.0.0.1:8080/; # 服务端口
      proxy_set_header   Host    $host;
      proxy_set_header   X-Real-IP   $remote_addr;
      proxy_set_header   X-Forwarded-For proxy_add_x_forwarded_for;
      proxy_set_header   X-Forwarded-Proto $scheme;
    }
    if ($scheme = http) {
        return 301 https://$server_name$request_uri;
    }
}
```

## Let's Encrypt

Let's Encrypt是一个很火的免费SSL证书开源项目, 可以实现自动化发布证书, 但有限期只有90天, 不过可以通过脚本来进行自动续签, 这也是官方给出的解决方案, 是一个免费好用的证书.

Let's Encrypt官方发布一个安装工具,[certbot](https://certbot.eff.org),可以通过官方的地址来获取安装的步骤,下面我以nginx+centos7的组合来说明如何安装部署,具体其他系统可以参考官网,大同小异;

### 安装证书

1. 先执行以下命令进行环境的安装;
   ```
   yum install epel-release
   ```
2. 执行以下命令安装certbot
   ```
   sudo yum install certbot
   ```
3. 申请证书
   ```
   certbot certonly --standalone -d example.com -d www.example.com
   ```
4. 按照提示输入邮箱, 点击几次确认,会得到以下信息:
   ```
   Output:
   IMPORTANT NOTES:
   - If you lose your account credentials, you can recover through
   e-mails sent to xxx@gmail.com
   - Congratulations! Your certificate and chain have been saved at
   /etc/letsencrypt/live/www.example.com/fullchain.pem. Your
   cert will expire on 2017-02-02. To obtain a new version of the
   certificate in the future, simply run Let's Encrypt again.
   - Your account credentials have been saved in your Let's Encrypt
   configuration directory at /etc/letsencrypt. You should make a
   secure backup of this folder now. This configuration directory will
   also contain certificates and private keys obtained by Let's
   Encrypt so making regular backups of this folder is ideal.
   - If like Let's Encrypt, please consider supporting our work by:
   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le
   ```
5. 至此,证书申请完毕;
6. 对nginx进行设置,然后重启nginx;

   ```
   server {
                listen       443 ssl;
                listen       80;
                server_name  www.example.cn; ##域名
                ssl_certificate /etc/letsencrypt/live/example.cn/fullchain.pem; #pem位置
                ssl_certificate_key /etc/letsencrypt/live/example.cn/privkey.pem; #key位置
                ssl_dhparam /etc/ssl/certs/dhparam.pem;
                ssl_ciphers 'ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA';
                ssl_prefer_server_ciphers  on;
                ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
                ssl_session_timeout 1d;
                ssl_session_cache shared:SSL:50m;
                ssl_stapling on;
                ssl_stapling_verify on;
                add_header Strict-Transport-Security max-age=15768000;
                location / {
                        proxy_pass http://127.0.0.1:8400/; ##服务端口
                        proxy_set_header   Host    $host;
                        proxy_set_header   X-Real-IP   $remote_addr;
                        proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
                        proxy_set_header   X-Forwarded-Proto $scheme;
                }

                if ($scheme = http) {
                        return 301 https://$server_name$request_uri;

                }
        }
   ```

### 自动更新

Let's Encrypt最大的不足就是只有90天的有效性, 所以需要我们配合计划任务来周期性更新证书;  
在计划任务中加入以下命令:

```
0 0 5 1 *  /usr/bin/certbot renew  >> /var/log/le-renew.log
```

每月1号的5点便会更新一遍证书, 可以自己设定周期, 不过不要太频繁;因为有请求次数的限制.

