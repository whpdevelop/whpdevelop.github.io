# wamp 配置文件

## 第一步

首先将`Wampserver2.4-x64.exe`安装 (直接下一步就可以)

需要注意: 路径中不要有中文路径

然后将wamp => www 文件中的俩个自动生成的文件删除新建一个.html 就可以访问了

### 第二步 

#### 修改www文件夹路径

找到 wamp => bin => apache => Apache2.4.4 =>conf => httpd.conf 打开

- 找到 239 和 240 行 将路径改为相应的
- 找到 268 将Deny 改为 Allow
- 将499行的 # 号去掉
- 此文件配置完毕 保存

### 第三步

#### 配置虚拟主机

找到 wamp => bin => apache => Apache2.4.4 =>conf=>extra=>httpd-vhosts.conf 打开

```text
<VirtualHost *:80>

    ServerAdmin webmaster@dummy-host.example.com
    DocumentRoot "c:/Apache24/docs/dummy-host.example.com"
    ServerName dummy-host.example.com
    ServerAlias www.dummy-host.example.com
    ErrorLog "logs/dummy-host.example.com-error.log"
    CustomLog "logs/dummy-host.example.com-access.log" common

</VirtualHost>
<VirtualHost *:80>

    DocumentRoot "e:/www/api"    这是你将www 移动后的地址
    ServerName api.com
    ServerAlias www.api.com      这俩行是配置的域名  

</VirtualHost>
<VirtualHost *:80>

    ServerAdmin webmaster@dummy-host2.example.com
    DocumentRoot "c:/Apache24/docs/dummy-host2.example.com"
    ServerName dummy-host2.example.com
    ErrorLog "logs/dummy-host2.example.com-error.log"
    CustomLog "logs/dummy-host2.example.com-access.log" common

</VirtualHost>

```

### 第四步

#### 配置hosts 文件

  hosts文件路径  C:/ => windows =>system32 => drivers => etc => hosts

127.0.0.1       localhost

127.0.0.1       www.api.com

127.0.0.1       api.com

### 第五步

重启wamp 图标变绿 OK!







​		