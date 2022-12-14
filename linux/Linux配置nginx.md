默认会有安装：

        sudo apt-get install nginx

更新：

        apt-get update
    
        apt-get install nginx

服务启动与停止：

        sudo systemctl stop nginx
    
        sudo systemctl start nginx
    
        sudo systemctl restart nginx
    
        sudo systemctl reload nginx

服务设置是否自启动：

        sudo systemctl disable nginx
    
        sudo systemctl enable nginx

查看服务是否启动：

         ps -ef | grep nginx

查看服务的状态：

        systemctl status nginx

nginx的默认配置：

​        

‘–conf-path=/etc/nginx/nginx.conf’, #配置文件路径，默认是conf/nginx
‘–error-log-path=/var/log/nginx/error.log’, #错误日志路径，默认是/logs/error.log
‘–http-client-body-temp-path=/var/lib/nginx/body’, #指定http客户端请求缓存文件存放目录的路径
‘–http-fastcgi-temp-path=/var/lib/nginx/fastcgi’, #指定http FastCGI缓存文件存放目录的路径
‘–http-log-path=/var/log/nginx/access.log’, #指定http默认访问日志的路径
‘–http-proxy-temp-path=/var/lib/nginx/proxy’, #指定http反向代理缓存文件存放目录
‘–http-scgi-temp-path=/var/lib/nginx/scgi’, #指定http sigi缓存文件存放目录的路径
‘–http-uwsgi-temp-path=/var/lib/nginx/uwsgi’, #指定http uwsgi缓存文件存放目录的路径
‘–lock-path=/var/lock/nginx.lock’, # 指定nginx.lock文件的路径
‘–pid-path=/var/run/nginx.pid’, # 指定nginx.pid文件的路径，默认是/logs/nginx.pid
‘–with-debug’, #启用调试日志
‘–with-http_addition_module’, #启用http_addition_module
‘–with-http_dav_module’, #启用http_dav_module
‘–with-http_geoip_module’,
‘–with-http_gzip_static_module’,
‘–with-http_image_filter_module’,
‘–with-http_realip_module’,
‘–with-http_stub_status_module’,
‘–with-http_ssl_module’,
‘–with-http_sub_module’,
‘–with-http_xslt_module’,
‘–with-ipv6’,
‘–with-sha1=/usr/include/openssl’,
‘–with-md5=/usr/include/openssl’,
‘–with-mail’,
‘–with-mail_ssl_module’,
‘–add-module=/build/buildd/nginx-0.8.54/debian/modules/nginx-upstream-fair’

安装完成后Nginx所使用的目录如下
/usr/sbin/nginx
/usr/share/nginx
/usr/share/doc/nginx
/etc/nginx
/etc/init.d/nginx
/etc/default/nginx
/etc/logrotate.d/nginx
/etc/ufw/applications.d/nginx
/var/lib/nginx
/var/lib/update-rc.d/nginx
/var/log/nginx

网站文件可以放就在 /usr/share/nginx/www下.具体情况需要查看响应的配置文件
网站配置文件： 

         默认目录：/etc/nginx/sites-available
    
        在此配置文件中配置和修改网站目录及域名等等信息

站点配置：

Nginx服务器阻止文件或站点配置文件存储在“/etc/nginx/sites-available /”目录中。要使这些文件在Nginx上使用，请将文件链接到“/etc/nginx/sites-enable/”目录中。
要激活任何新的站点配置，我们需要在“sites-available”目录中创建到“sites-enabled”目录的站点配置文件的符号链接。
要标识站点的配置，请遵循服务器阻止文件的标准命名转换。例如，您有一个网站a5idc.net。最好将文件创建为“/etc/nginx/sites-available/a5idc.net.conf”，以便在Nginx Web服务器中配置了多个站点时快速识别。
解决或调试错误最重要的文件称为日志文件。在“/var/log/nginx”目录中生成的Nginx日志文件（access.log和error.log）。如果每个服务器块都有不同的访问和错误日志文件，则对于调试很有用。
配置域文档的根目录没有限制，您可以设置任何所需的位置。但是，对于Web根目录，最推荐的位置是：
/home/<user>/<site-name>
/var/www/<site-name>
/var/www/html/<site-name>
/opt/<site-name>
        1、配置多个配置文件，作为每一个网站的单独配置文件，当然只是用系统默认提供的基础上修改也可以：配置目录/etc/nginx/sites-available

        例如： /etc/nginx/sites-available/limonero
    
        limonero文件内容：与default类似，只需要在器基础上配置自己的域名、端口和网站文件村饭的目录即可,端口后面的default_server 需要注释掉
    
        2、建立软链接：建立在site-enabled中
    
                sudo ln -s /etc/nginx/sites-available/limonero  /etc/nginx/sites-enabled/
    
                修改配置之后需要重新建立软链接
- 查看nginx日志，路径为/var/log/nginx/error.log。
-  查看nginx 版本号 sudo nginx -v

2、防火墙配置
今天，我们所有人都在使用UFW防火墙来管理Debian 10机器上的网络连接和流量。
要使用Nginx，您需要打开HTTP端口（80）和HTTPS端口（443）。您可以通过在UFW上启用“ Nginx Full”配置文件来打开HTTP和HTTPS端口：
\# sudo ufw allow 'Nginx Full'



server {

 listen 6557 default_server;

 lister [::]:6557 default_server;



 root /var/www/h_html;

 index index.html index.htm;



 server_name _;

 location / {

  try_files $uri $uri/ = 404

 }

}