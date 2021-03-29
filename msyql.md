# mysql常用命令 

## 数据库服务启动/关闭

```bash
$ service mysql start        # rhel6  启动数据库
$ systemctl start mariadb    #rhel7 启动MariaDB
$ systemctl enable mariadb   # 设置开机启动
$ systemctl status mariadb   # 查看状态
$ systemctl stop mariadb     # 停止MariaDB
$ systemctl restart mariadb  # 重启MariaDB

$ mysql.service start        #mac 启动数据库
$ mysql.service status       # 查看数据库状态
$ mysql.service stop         # 停止数据库
$ mysql.service restart      # 停止数据库

$ net mysql start        # windows
$ net stop mysql56       # windows  # 进入mysql安装目录（有时候安装版本不同可能是mysql56）
$ net start mysql56      # windows
```


## 登录数据库
```
# 登录
$ mysql -uxopens -piscs200 -h 192.168.184.137
> Ues xopensdb      #进入数据库xopensdb
> Show tables       #显示所有数据表


mysql -u root --password=123qwe -e “SELECT host FROM mysql.user;”
mysql -u root --password=123qwe -e “SELECT host FROM mysql.user;”

#隐藏列名
mysql -u $user --password=$password -s -N -e "MySQL Query Sentence"
mysql -u root --password=qwe123 -s -N -e "SELECT host FROM mysql.user;"

```

## mas平台查看历史库
```
His_Event_Tab (历史事项表)
data201901    (遥测历史数据表)
pdata201901   (电度历史数据表)
daydata199901 (遥测历史数据日统计表)
daypdata199901(电度历史数据日统计表)
mondata1999   (遥测历史数据月统计表)
monpdata1999  (电度历史数据月统计表)
yeardata1999  (遥测历史数据年统计表)
yearpdata1999 (电度历史数据年统计表)。

遥测历史数据表flag定义 data201901 

1	Real Data	实时值
55	Real Max	日实时存盘最大值 
56	Real Min	日实时存盘最小值
58	Average Data	平均值

电度历史数据表flag定义 pdata201901

79	KWH Day Accumulated Data	日累计电量

历史统计存盘量的标志（flag）

150	Day Statistic Max	日统计最大值
151	Day Statistic Min	日统计最小值
153	Day Statistic Average	日统计平均值


常用sql

select * from xopenshdb.data202102 where sname='Kytps_CD301AI0' and sdate=18663 and time=0 and flag<50
select * from xopenshdb.data202102 where sname='Kytps_CD301AI0' and sdate=18663 and time=0 and flag=55

```

## 常用操作
> SQL 语句都是不区分大小写的
```sql
CREATE DATABASE mysql_shiyan;                                   -- 创建数据库
show databases;                                                 -- 查看数据库
use mysql_shiyan;                                               -- 连接数据库
CREATE TABLE employee (id int(10),name char(20),phone int(12)); -- 新建 数据表
show tables;                                                    -- 查看表
INSERT INTO employee(id,name,phone) VALUES(01,'Tom',110110110); -- 插入数据
INSERT INTO employee VALUES(02,'Jack',119119119);
INSERT INTO employee(id,name) VALUES(03,'Rose');
```

## 系统维护 
```bash 
$ netstat -nat | grep 3306  # 查看3306端口（默认端口)
mysql> show global variables like 'port';  # 进入mysql查看
mysql> show variables like '%version_%';  #查看数据库位数
```

## 常用命令 

```bash 
> show columns from 表名;    //获取表结构
>     create table bill      //创建表
    (
     id INT(11),
     name VARCHAR(25),
     amount FLOAT,
     date VARCHAR(25),
     remark VARCHAR(25)
     );

# 查看表结构
>   describe bill;
    desc bill;
    # NULL 表示该列是否可以存储NULL值
    # Key表示该列是否已编制索引
    # Default 表示该列是否有默认值，如果有，是多少
    # Extra: 表示可以获得德与给定定列有关定附加信息。
    show create table bill\G; #显示创建表定sql语句。\g用于显示更加直观。
```

修改端口(需重启) > 编辑/etc/my.cnf文件，早期版本有可能是my.conf文件名，增加端口参数，并且设定端口，注意该端口未被使用，保存退出。 » Windows: Program Files\MySQL\MySQL Server 5.1\my.ini

mysql通过-D参数指定连接到test数据库
mysql时间条件筛选

```sql
SELECT * FROM 表名 WHERE to_days(时间字段名) = to_days(now());  #今天
SELECT * FROM 表名 WHERE TO_DAYS( NOW( ) ) - TO_DAYS( 时间字段名) <= 1   #昨天
SELECT * FROM 表名 WHERE DATE_SUB(CURDATE(), INTERVAL 7 DAY) <= date(时间字段名)  #近7天
SELECT * FROM 表名 WHERE DATE_SUB(CURDATE(), INTERVAL 30 DAY) <= date(时间字段名) #近30天
SELECT * FROM 表名 WHERE DATE_FORMAT( 时间字段名, '%Y%m' ) = DATE_FORMAT( CURDATE( ) , '%Y%m' )  #本月
SELECT * FROM 表名 WHERE PERIOD_DIFF( date_format( now( ) , '%Y%m' ) , date_format( 时间字段名, '%Y%m' ) ) =1  #上一月
SELECT * FROM `ht_invoice_information` where QUARTER(create_date)=QUARTER(now()); #查询本季度数据
SELECT * FROM `ht_invoice_information` where QUARTER(create_date)=QUARTER(DATE_SUB(now(),interval 1 QUARTER));  #查询上季度数据
SELECT * FROM `ht_invoice_information` where YEAR(create_date)=YEAR(NOW());  #查询本年数
SELECT * FROM `ht_invoice_information` where year(create_date)=year(date_sub(now(),interval 1 year));  #查询上年数据
SELECT name,submittime FROM enterprise WHERE YEARWEEK(date_format(submittime,'%Y-%m-%d')) = YEARWEEK(now()); #查询当前这周的数据
SELECT name,submittime FROM enterprise WHERE YEARWEEK(date_format(submittime,'%Y-%m-%d')) = YEARWEEK(now())-1;  #查询上周的数据
SELECT name,submittime FROM enterprise where date_format(submittime,'%Y-%m')=date_format(DATE_SUB(curdate(), INTERVAL 1 MONTH),'%Y-%m')
SELECT * FROM user where DATE_FORMAT(pudate,'%Y%m') = DATE_FORMAT(CURDATE(),'%Y%m') ; 
SELECT * FROM user where WEEKOFYEAR(FROM_UNIXTIME(pudate,'%y-%m-%d')) = WEEKOFYEAR(now()) 
SELECT * FROM user where MONTH(FROM_UNIXTIME(pudate,'%y-%m-%d')) = MONTH(now()) 
SELECT * FROM user where YEAR(FROM_UNIXTIME(pudate,'%y-%m-%d')) = YEAR(now()) and MONTH(FROM_UNIXTIME(pudate,'%y-%m-%d')) = MONTH(now()) 
SELECT * FROM user where pudate between  上月最后一天  and 下月第一天   #查询上个月的数据
SELECT name,submittime FROM enterprise   where date_format(submittime,'%Y-%m')=date_format(now(),'%Y-%m'); #查询当前月份的数据
SELECT name,submittime FROM enterprise where submittime between date_sub(now(),interval 6 month) and now(); #查询距离当前现在6个月的数

```














