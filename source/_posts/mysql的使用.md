---
title: mysql的使用
date: 2017-05-22 17:38:45
tags: mysql
---
> mysql的使用

##### 设置alias的路径
1.vim ~/.               打开隐藏文件  
2.找到.zshrc文件 
2.alias mysql=/usr/local/mysql/bin/mysql；

##### Macbook Pro 安装及卸载mysql教程
http://www.th7.cn/db/mysql/201504/101743.shtml   mysql的教程
http://blog.csdn.net/yanqinbin/article/details/50442676   
1.http://dev.mysql.com/downloads/mysql/
  http://dev.mysql.com/downloads/workbench/
2. cd /usr/local/mysql/bin/
3.回车后 登录管理员权限  sudo su
4.回车后输入以下命令来禁止mysql验证功    ./mysqld_safe --skip-grant-tables &
5.输入 alias 命令   alias mysql=/usr/local/mysql/bin/mysql
#如果是登录远程主机上的mysql数据库 mysql -h 主机地址 -u 用户名 -p 用户密码
sudo apt-get install mysql-workbench   安装mysql
create database Company default char set utf8 collate utf8_general_ci;; 第一步： 创建中文输入
use mysqlTest           // 使用库名
create table students   // 创建表的名字
(
Id_P int NOT NULL auto_increment,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
PRIMARY KEY (Id_P)
)charset = utf8 

drop database MYdb;  删除数据
select  name , gender from stduent
[where gender = "男" and sorce <= 70]
[limit 0 offset 4 ]   limit 选择下标  offset 选择几项
update student set phone='13411112222',english_score=90 where name='韩梅梅';    //更新数据
delete from student where id=3;         //删除第3行 
select * from student where phone like '1%';  取电话开头市1的所有电话
distinct  把重复的合并成打第一个;
select avg(age) from school.student;   求平均数
select count(distinct name) from school.student;  （去掉重名的行数
max（） min（）sum（）  最大 最小函数  求和
select mid(name,1,2) from school.student;  从姓名中第一位开始取两个。
select length(name),name from school.student;   姓名的长度   注：1个文字占三个字节
select now();  当前的时间
order by age desc/asc;  排序 降序 升序;
where and/or  不能是聚合函数  having and/or   可以是聚合函数;
（select age from student） 子查询语法
黑窗户命令
mysql -u root -p  
show databases;
create database Company default char set utf8 collate utf8_general_ci;; 第一步： 创建中文输入
use Company;
查询1-5条数据
select * from news where 1=1 limit 0,5;

##### unbuntu下载

1. w 查看登陆信息
2. apt-cache search mysql-server
3.sudo apt-get install mysql-server-5.6
4.ps -ef|grep mysqld      //查看mysql的进程
5.sudo /etc/init.d/mysql start/stop/restart status       //查看mysql的状态
6.mysql -h127.0.0.1 -p3306 -uroot -p   ||    mysql -S/tmp/mysql.sock -uroot -p               // 连接到服务器(服务器和本机)
7. status;                 // 查看mysql的连接状态
8. show processlist;     // 查看进程列表
9. show global variables like 'socket';   // 查看socket文件所在的位置  (mysql -S/tmp/mysql.sock -uroot -p)
10.配置MySQL接受远程登录连接:grant all PRIVILEGES on mydb.* to linjk@'%' identified by '123456'
11.配置完后使用命令：flush privileges;使配置生效。