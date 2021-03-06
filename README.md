# nginx-apache-mysql-php
Bulid PHP server environment

首先运行<code>apt-get update</code>完成以后在运行<code>apt-get upgrade</code>

##install nginx

download http://nginx.org/

在安装nginx之前需要一个<a href="http://nchc.dl.sourceforge.net/project/pcre/pcre/8.39/pcre-8.39.tar.bz2">pcre(http://nchc.dl.sourceforge.net/project/pcre/pcre/8.39/pcre-8.39.tar.bz2)</a>的一个库才成正确的安装nginx
直接进入nginx的目录执行<code>./configure --prefix=/usr/local/etc/nginx --with-pcre=~/pcre-8.39</code>如果执行php返回空白页面请在fastchi_params文件中加上fastcgi_param  SCRIPT_FILENAME $document_root$fastcgi_script_name;
重启nginx，即可正常显示页面了。
##install apache

  download http://mirror.bit.edu.cn/apache//httpd/httpd-2.4.23.tar.gz
  
  在安装apache之前需要一个<a href="http://nchc.dl.sourceforge.net/project/pcre/pcre/8.39/pcre-8.39.tar.bz2">pcre(http://nchc.dl.sourceforge.net/project/pcre/pcre/8.39/pcre-8.39.tar.bz2)</a>的一个库才成正确的安装apache
  
  下载好以后解压<code>tar -jxvf pcre-8.39.tar.bz2</code>以后进入目录运行<code>./configure --prefix=/usr/local/etc/pcre</code>编译完成以后在<code>make && make install</code>
  
  接着还要需要两个库文件一个是<a href="http://apache.fayea.com//apr/apr-1.5.2.tar.bz2">apr(http://apache.fayea.com//apr/apr-1.5.2.tar.bz2)</a>和<a href="http://apache.fayea.com//apr/apr-util-1.5.4.tar.bz2">apr-util(http://apache.fayea.com//apr/apr-util-1.5.4.tar.bz2)</a>把这两个库解压到httpd-2.4.23的srclib目录下面，改名为apr和apr-util
  
  进入httpd-2.4.23目录<code>./configure --prefix=/usr/local/etc/apache --with-pcre=/usr/local/etc/pcre</code>接着<code>make && make install</code>
   
  配置apache多站点，修改httpd.conf去掉Include conf/extra/httpd-vhosts.conf前面的#并且把<code>\<Directory /\></code>的Require all denied改为Require all granted,接着进入extra,编辑虚拟机vhost配置文件,配置详情google

##insall PHP
 download http://cn2.php.net/distributions/php-7.0.11.tar.bz2 也可以去官网下载
 安装之前需要先安装一个库直接<code>apt-get install libxml2-dev</code>
 进入解压的目录<code>cd php-7.0.11</code>使用<code>./configure --prefix=/usr/local/etc/php --with-apxs2=/usr/local/etc/apache/bin/apxs</code>nginx安装需要加载fpm<code>./configure --prefix=/usr/local/etc/php --enable-fpm</code>然后使用<code>make && make install</code>安装过程比较久，可以利用这段时间安装mysql
 
 这里还需要配置apache和php的关联
 Apache与PHP整合：
 编辑Apache配置：vi /usr/local/apache/conf/httpd.conf
找到AddType application/x-gzip .gz .tgz
在后面添加
<code>AddType application/x-httpd-php .php</code>
<code>AddType application/x-httpd-php-source .php5</code>  
找到DirectoryIndex index.html
修改为
DirectoryIndex index.html index.php

##install mysql
  官网download http://dev.mysql.com/downloads/mysql 选择对应的系统进行下载然后解压
  
  按照下面的顺序进行安装
  
    1.mysql-common_5.7.10-1ubuntu14.04_amd64.deb
    2.libmysqlclient20_5.7.10-1ubuntu14.04_amd64.deb
    3.libmysqlclient-dev_5.7.10-1ubuntu14.04_amd64.deb
    4.libmysqld-dev_5.7.10-1ubuntu14.04_amd64.deb
    5.mysql-community-client_5.7.10-1ubuntu14.04_amd64.deb
    6.mysql-client_5.7.10-1ubuntu14.04_amd64.deb
    7.mysql-community-server_5.7.10-1ubuntu14.04_amd64.deb
 到底所有的环境都配置好了，接下来我们来安装php的扩展
 
 如果安装mysql需要库文件，使用<code>apt-get -f install</code>再次安装就可以了
 
 ##install marizdb
 安装命令<code>apt-get install mariadb-server</code>
 在<code>/etc/mysql/conf.d</code>创建mysqld_openstack.cnf的文件写入一下内容
 
 <code>bind-address = 127.0.0.1
default-storage-engine = innodb
innodb_file_per_table
collation-server = utf8_general_ci
init-connect = 'SET NAMES utf8'
character-set-server = utf8</code>

  然后重新启动mysql<code>service mysql restart</code>
  
