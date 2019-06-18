# 数据库操作
## 1、mysql 时间相关sql , 按天、月、季度、年等条件进行查询

### 1.1、 mysql按天查询
#### 1.1.1、 今天
select * from ticket_order_detail where to_days(use_time) = to_days(now());
#### 1.1.2、  7天
SELECT *FROM ticket_order_detail  where DATE_SUB(CURDATE(), INTERVAL 7 DAY) <= date( use_time)
#### 1.1.3、  近30天
SELECT *FROM ticket_order_detail  where DATE_SUB(CURDATE(), INTERVAL 30 DAY) <= date( use_time)
### 1.2、 mysql按月查询
#### 1.2.1、 本月
SELECT *FROM ticket_order_detail  WHERE DATE_FORMAT(  use_time, '%Y%m' ) = DATE_FORMAT( CURDATE( ) , '%Y%m' )
#### 1.2.2、 上一月
SELECT *FROM ticket_order_detail  WHERE PERIOD_DIFF( date_format( now( ) , '%Y%m' ) , date_format(  use_time, '%Y%m' ) ) =1
#### 1.2.3、  查询当前月份的数据
select name,submittime from enterprise where date_format(submittime,’%Y-%m’)=date_format(now(),’%Y-%m’)
#### 1.2.4、  查询距离当前现在6个月的数据
select name,submittime from enterprise where submittime between date_sub(now(),interval 6 month) and now();
#### 1.2.5、  查询上个月的数据
select name,submittime from enterprise where date_format(submittime,’%Y-%m’)=date_format(DATE_SUB(curdate(), INTERVAL 1 MONTH),’%Y-%m’)
select*from`user`whereDATE_FORMAT(pudate,‘%Y%m‘)=DATE_FORMAT(CURDATE(),‘%Y%m‘) ;
select * from user where WEEKOFYEAR(FROM_UNIXTIME(pudate,’%y-%m-%d’)) = WEEKOFYEAR(now())
select*
fromuser
whereMONTH(FROM_UNIXTIME(pudate,‘%y-%m-%d‘))=MONTH(now())
select*
from[user]
whereYEAR(FROM_UNIXTIME(pudate,‘%y-%m-%d‘))=YEAR(now())
andMONTH(FROM_UNIXTIME(pudate,‘%y-%m-%d‘))=MONTH(now())
### 1.3、 mysql按季度查询
#### 1.3.1、 查询本季度数据
select * from `ticket_order_detail` where QUARTER(use_time)=QUARTER(now());
#### 1.3.2、 查询上季度数据
select * from `ticket_order_detail` where QUARTER(use_time)=QUARTER(DATE_SUB(now(),interval 1 QUARTER));
### 1.4、 mysql按年度查询
#### 1.4.1、 查询本年数据
select * from `ticket_order_detail` where YEAR(use_time)=YEAR(NOW());
#### 1.4.2、 查询上年数据
select * from `ticket_order_detail` where year(use_time)=year(date_sub(now(),interval 1 year));
### 1.5、 mysql按周查询
#### 1.5.1、  查询当前这周的数据
SELECT name,submittime FROM enterprise WHERE YEARWEEK(date_format(submittime,’%Y-%m-%d’)) = YEARWEEK(now());
#### 1.5.2、  查询上周的数据
SELECT name,submittime FROM enterprise WHERE YEARWEEK(date_format(submittime,’%Y-%m-%d’)) = YEARWEEK(now())-1;

select*
from[user]
 今天 wherepudatebetween上月最后一天
-- and下月第一天
where date(regdate) = curdate();
select * from test where year(regdate)=year(now()) and month(regdate)=month(now()) and day(regdate)=day(now())
SELECT date( c_instime ) ,curdate( )
FROM `t_score`
WHERE 1
LIMIT 0 , 30