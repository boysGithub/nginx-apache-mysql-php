# nginx-apache-mysql-php
Bulid PHP server environment

首先运行<code>apt-get update</code>完成以后在运行<code>apt-get upgrade</code>

##install nginx

download http://nginx.org/

##install apache

  download http://mirror.bit.edu.cn/apache//httpd/httpd-2.4.23.tar.gz

  在安装apache之前需要一个<a href="http://nchc.dl.sourceforge.net/project/pcre/pcre/8.39/pcre-8.39.tar.bz2">pcre(http://nchc.dl.sourceforge.net/project/pcre/pcre/8.39/pcre-8.39.tar.bz2)</a>的一个库才成正确的安装apache
  
  下载好以后解压<code>tar -jxvf pcre-8.39.tar.bz2</code>以后进入目录运行<code>./configure --prefix=/usr/local/etc/pcre</code>编译完成以后在<code>make && make install</code>
  
  接着还要需要两个库文件一个是<a href="http://apache.fayea.com//apr/apr-1.5.2.tar.bz2">apr(http://apache.fayea.com//apr/apr-1.5.2.tar.bz2)</a>和<a href="http://apache.fayea.com//apr/apr-util-1.5.4.tar.bz2">apr-util(http://apache.fayea.com//apr/apr-util-1.5.4.tar.bz2)</a>把这两个库解压到httpd-2.4.23的srclib目录下面，改名为apr和apr-util
  
  进入httpd-2.4.23目录<code>./configure --prefix=/usr/local/etc/apache --with-pcre=/usr/local/etc/pcre</code>接着<code>make && make install</code>
   
  配置apache多站点，修改httpd.conf去掉Include conf/extra/httpd-vhosts.conf前面的#并且把<code>\<Directory /\></code>的Require all denied改为Require all granted,接着进入extra,编辑虚拟机vhost配置文件,配置详情google
