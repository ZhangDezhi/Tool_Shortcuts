# oracle 基本知识
oracle 11g有两个版本 :
1.  express （xe）   Oracle Database Express Edition 11g Release 2 
2.  标准版  （orcl） Oracle Database 11g Release 2 (11.2.0.1.0) 

安装成功后：
到sqlplus 路径下面： 
标准版： D:\app\Administrator\product\11.2.0\dbhome_1\BIN
express：C:\oraclexe\app\oracle\product\11.2.0\dbhome_1\BIN


## 登录

```bash
$ sqlplus / as sysdba     # 以操作系统权限认证的oracle sys管理员登陆
$ sqlplus /nolog          # (不登录任何数据库)
conn as sysdba                           --以操作系统权限认证的oracle sys管理员登陆
create user test identified by test      -- (创建一个普通用户)
grant test connect,resource,dba to test; --(给该用户授予权限)
conn test/test                           --用test用户登录


$ sqlplus scott/tiger         --非管理员用户登陆
$ sqlplus scott/tiger@orcl    --非管理员用户使用tns别名登陆
$ sqlplus sys/password@orcl as sysdba --管理员用户使用tns别名登陆
$ sqlplus                      #不显露密码的登陆方式
Enter user-name：sys
Enter password：***

$ sqlplus xopens/iscs200@//192.168.2.230:1521/xe        #远程登录 
$ sqlplus usr/pwd@//host:port/sid                       #远程登录
$ sqlplus system/h1w2D3B4@//10.71.105.216:1526/i2kdb


$ sqlplus  xopens/iscs200    #登录数据库 用户名/密码
$ sqlplus  root/root123  as sysdba  #系统管理员登录
```

https://blog.csdn.net/qq_27731689/article/details/103289987

https://blog.csdn.net/qq_27731689/article/details/103289987


## 常用sql语句

```
conn 用户名/密码 [as sysdba]    --切换用户
conn sys/sys as sysdba;       --切换管理员
conn xopens/iscs              --切换普通用户

--设置标格行宽和列宽(防止错乱)
set linesize 300;    --设置每行展示字符数
col 列名 for a[数字]   --某一行占几个字符

#查看表中数据
select *form tab;   --S查看表中数据


#查看表结构
Desc 表名;

```





## 常用sql语句(信息查看)

```sql
show user    --查看当前用户
select * from v$version;   -- Oralce版本查看

select * from all_tables where owner='TEST'； --TEST为用户名，用户名必须是大写。
select table_name from user_tables; --查看当前登录的用户的表


```

## 常用sql(表操作)

```sql
--建一个表
create table HH2(
tid number primary key ,--主键设定
tname varchar2(20)
);

--删除表
drop table HH;

--表空间（相当于一个数据库）(DBA权限)
create tablespace test
datafile 'D:test.dbf'
size 10M
autoextend on
next 10M
maxsize 100M

--指定表在那个表空间里面(默认在USERS表空间里)
create table HH(tid number primary key)
tablespace test;
select * from tabs;

--删除 表空间
drop tablespace test including contents and datafiles --连带物理文件和表空间中的数据也一起删除

 --建表建约束
create table student1(
sid number primary key ,
sname varchar2(20) not null,
sage number,
ssex char(2),
saddress varchar2(100),
cid number references tclass(cid)--建立外键关系
);

create table tclass
(
cid number primary key,
cname varchar2(20)
);
--唯一unique 检查 check 默认值 modify 添加外键关系 添加列
alter table student1 add constraint UQ_student1_sname unique(sname);
alter table student1 add constraint CK_student1_agae check(sage between 19 and 70);
alter table student1 modify ssex default '男';
alter table student1 add constraint FK_student1_cid foreign key(cid) references tclass(cid);
alter table student1 add dt date;
--删除约束
alter table student1 drop constraint UQ_student1_sname ; 

```