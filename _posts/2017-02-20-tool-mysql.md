---
layout: post
title: Mysql无法插入中文(Insert语句)
keywords: Tool
categories: [Tool]
tags: [Tool]
---
### 问题描述
mysql中 **INSERT INTO users(NAME, age) VALUES('日暮清晨', 23);**
报以下错误:
Error Code: 1366. Incorrect string value: '\xE6\x97\xA5\xE6\x9A\xAE...' for column 'NAME' at row 1

### 解决办法
重新配置字符集为utf8，配置完重启mysql，而后新建库，表，就可以添加中文字段了。
即便配置好了字符集并重启了，如果还在之前的库里创建表，或者在之前创建的表里添加中文字段，还是会提示上面的错误信息。

* 系统环境:Macbook

接下来看如何重新配置mysql的字符集:

* 查看 **/etc/** 目录下是否有my.cnf文件,若有,则在my.cnf文件中覆盖如下代码,若没有,则创建:

```java

# Example MySQL config file for small systems.  
#  
# This is for a system with little memory (<= 64M) where MySQL is only used  
# from time to time and it's important that the mysqld daemon  
# doesn't use much resources.  
#  
# MySQL programs look for option files in a set of  
# locations which depend on the deployment platform.  
# You can copy this option file to one of those  
# locations. For information about these locations, see:  
# http://dev.mysql.com/doc/mysql/en/option-files.html  
#  
# In this file, you can use all long options that a program supports.  
# If you want to know which options a program supports, run the program  
# with the "--help" option.  
 
# The following options will be passed to all MySQL clients  
[client]  
default-character-set=utf8  
#password   = your_password  
port        = 3306 
socket      = /tmp/mysql.sock  
 
# Here follows entries for some specific programs  
 
# The MySQL server   
[mysqld]  
default-storage-engine=INNODB  
character-set-server=utf8  
collation-server=utf8_general_ci  
port        = 3306 
socket      = /tmp/mysql.sock  
skip-external-locking  
key_buffer_size = 16K  
max_allowed_packet = 1M  
table_open_cache = 4 
sort_buffer_size = 64K  
read_buffer_size = 256K  
read_rnd_buffer_size = 256K  
net_buffer_length = 2K  
thread_stack = 128K  
 
# Don't listen on a TCP/IP port at all. This can be a security enhancement,  
# if all processes that need to connect to mysqld run on the same host.  
# All interaction with mysqld must be made via Unix sockets or named pipes.  
# Note that using this option without enabling named pipes on Windows  
# (using the "enable-named-pipe" option) will render mysqld useless!  
#   
#skip-networking  
server-id   = 1 
 
# Uncomment the following if you want to log updates  
#log-bin=mysql-bin  
 
# binary logging format - mixed recommended  
#binlog_format=mixed  
 
# Causes updates to non-transactional engines using statement format to be  
# written directly to binary log. Before using this option make sure that  
# there are no dependencies between transactional and non-transactional  
# tables such as in the statement INSERT INTO t_myisam SELECT * FROM  
# t_innodb; otherwise, slaves may diverge from the master.  
#binlog_direct_non_transactional_updates=TRUE  
 
# Uncomment the following if you are using InnoDB tables  
#innodb_data_home_dir = /usr/local/mysql/data  
#innodb_data_file_path = ibdata1:10M:autoextend  
#innodb_log_group_home_dir = /usr/local/mysql/data  
# You can set .._buffer_pool_size up to 50 - 80 %  
# of RAM but beware of setting memory usage too high  
#innodb_buffer_pool_size = 16M  
#innodb_additional_mem_pool_size = 2M  
# Set .._log_file_size to 25 % of buffer pool size  
#innodb_log_file_size = 5M  
#innodb_log_buffer_size = 8M  
#innodb_flush_log_at_trx_commit = 1 
#innodb_lock_wait_timeout = 50 
 
[mysqldump]  
quick  
max_allowed_packet = 16M  
 
[mysql]  
no-auto-rehash  
# Remove the next comment character if you are not familiar with SQL  
#safe-updates  
 
[myisamchk]  
key_buffer_size = 8M  
sort_buffer_size = 8M  
 
[mysqlhotcopy]  
interactive-timeout 

```
 

* 重启mysql服务

可以参考:
[http://www.tuicool.com/articles/QBFZV3R](http://www.tuicool.com/articles/QBFZV3R)
[http://blog.sina.com.cn/s/blog_7175926b0102ws03.html](http://blog.sina.com.cn/s/blog_7175926b0102ws03)

 

