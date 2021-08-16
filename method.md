<div style="text-align:center;font-size:25px">Nginx安装与配置</div>

### 安装
安装nginx：</br>
`sudo apt-get install nginx`</br>
查看nginx服务状态：</br>
`sudo systemctl status nginx`

更改防火墙配置：</br>
`sudo ufw allow 'Nginx Full'`

此时如果访问该网站的ip地址，应该会有下图：</br>
![nginx-default](./image/nginx-default.png)

将域名指向本机:</br>
`sudo vim /etc/hosts`

添加域名：</br>
`127.0.0.1 netlab4njucs.top`

### 配置

建立存放网站的文件夹：</br>
`sudo mkdir /var/www/NJUCS_Web/pub_html`

在其中放入网页html文件，如`index.html`，比如我们的html文件如下：</br>
![htmltxt](./image/html.PNG)

接下来修改配置文件，使得外部能够访问到我们自己的html文件：</br>
`sudo vim /etc/nginx/sites-enabled/default`</br>
修改`root`后面的内容，使其指向存放网页文件的文件夹:</br>
`root /var/www/NJUCS_Web/pub_html;`</br>
修改`index`后面的内容，使其指向网页文件:</br>
`index index.html;`</br>
配置文件default最终看上去：

server {</br>
&emsp;listen&emsp;80;</br>
&emsp;listen&emsp;[::]:80;</br>
&emsp;root&emsp; /var/www/NJUCS_Web/pub_html/;</br>
&emsp;index&emsp; index.html;</br>
&emsp;server_name netlab4njucs.top;</br>
&emsp;access_log /var/log/nginx/access.log;</br>
&emsp;error_log /var/log/nginx/error.log;</br>
&emsp;location / {</br>
  &emsp;&emsp;  try_files $uri $uri/ =404;</br>
&emsp;  }</br>
}

保存关闭后查看配置文件是否有语法错误：</br>
`sudo nginx -t`

最后重启Nginx服务：</br>
`sudo systemctl restart nginx`

此时用ip或者域名来访问，得到如下图：</br>
![after-config](./image/after-config.PNG)
