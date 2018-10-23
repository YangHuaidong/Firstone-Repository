# Firstone-Repository



SQL常用单词：
create		创建
database	数据库
show		显示,查看
alter		修改
delete 		删除
use			使用,运用		
select		挑选
drop		使终止

tables		表，表格

distinct	独特的,有区别的	
address		地址

创建表步骤：
没有请创建！！！
步骤一:先进入数据库show databases;
步骤二:切换创建的数据库	 use 库名;
步骤三:进入数据表		show tables;

		

数据库操作：
		create database 数据库名;	创建数据库(create database testdb;)
		show create database 数据库名;		显示数据库创建信息(show create database testdb;) 
		show databases;				显示所有数据库
		use testdb;		切换、使用数据库 use 数据库名
		select database(); 			显示当前数据库 

数据表操作：
show tables;		查看表 作用：查看所选数据库中所有的表 
create table 表名();	创建表 作用:在数据库中创建一张新表create table stu(sid int,sname char(20),sage 20);
show create table stu;	显示创建表信息 作用：用来显示创建表时的信息 语法：show create table 表名;
alter table stu add gender char(4);		增加字段 作用：为已存在的表添加一个新字段 语法：alter table 表名 add 列名 数据类型

查询插入数据：
select * from stu;		查询数据。语法：select 字段名列表 from 表名
desc stu   		查询表属性。语法:desc 表名
insert into tStudent values(1,'tom',20)	插入数据,插入所有字段数据.语法：insert into 表名 [(字段名列表, ...)] values(值列表, ...)
insert into stu(sage,sname) values(20,'jack'); 插入数据,插入指定字段
insert into stu values(2,'rose',20),(3,'tony',22);  插入数据,插入多条数据

修改数据：
语法：update 表名 set 字段=值[条件]；
update stu set sAge=25;		更新所有的数据
update stu set sname='alice' where name='tony';	更新满足条件的数据


truncate stu;		删除全部数据。语法：truncate 表名
delete from stu;		删除数据。
delete from stu where snumber = 1;	删除满足条件的数据.语法：delete from 表名 where snumber = 条件



数据库常用约束：
主键约束 作用：让数据具有唯一标识 语法：primary key
 create table tpk(id int primary key , name char(10));
添加数据:insert into tpk values(1,'tom'),(2,'jack');



数据表查询操作：：

一、创建一个空数据库：create database db charset utf8;
二、使用这个空数据库、use db
三、使用source将数据导入备用

四、单表查询数据：
1、select * from t_student;			查询数据表中所有数据语法：select * from 表名
2、select c_id,c_name,c_address from t_student;查询指定字段的显示语法：select 字段1，字段2,...from表名
as  取别名，可不写用空格代替；
3、select c_id as 学号,c_name as 姓名,c_address 地址 from t_student; 	as别名在查询时,默认结果显示的字段和表中字段名相同，语法:select 字段1 as 别名,字段2 别名,...from 表名
4、select distinct c_address from t_student;	消除重复数据在查询数据时,可以使用distinct来实现去重。语法:select distinct 字段名 from 表名。注意：distinct 在去重时，会比较所有的指定字段，只有完全相同时才认为是重复的。
5、select * from t_student where c_gender='男';		通过where子句来设置查询条件
6、比较运算符：等于：=  大于：>  大于等于：>=  小于:<  小于等于:<=   不等于:!= 或<>
select * from t_student where c_age < 20;
7、逻辑运算符:and or not
select * from t_student where c_age < 20 and c_gender=‘女';


五、模糊查询：like   %表示任意多个任意字符    _表示一个任意字符
	select * from t_student where c_name like '孙’；
	select * from t_student where c_name like '孙%’；
	select * from t_student where c_name like '孙_’；
范围查询：：
	in 表示在一个非连续的范围内,可以使用or实现
	法一、select * from t_student where id in (1,3,8);
	法二、select * from t_student where c_id=1 or c_id=3 or c_id=8;
	between...and...表示在一个连续的范围内，可以使用and实现
	法一更简洁、select *from t_student where c_id between 2 and 5;
	法二、select *from t_student where c_id>=2 and c_id<=5;
查询结果排序:
	排序使用 order by 子句 asc(默认) 升序 / desc 降序 语法：select * from 表名 order by 列1 asc|desc [,列2 asc|desc,...]
	select * from t_student order by c_age asc;
	select * from t_student order by c_age desc,c_id asc;
分页查询：limit n(数据)  select * from t_student limit 2,3;

六、聚合函数：：
	sum() 数字，对指定列中的所有非空值求总和
	avg() 数字，对指定列中的所有非空值求平均值
	min() 数字.字符.datetime，返回指定列中的最小数字、最早的日期或者最小的字符串
	max() 数字.字符.dateime，返回指定列中的最大数字、最早的日期或者最大的字符串
	count() 任意基于行的数据类型， 统计结果集合中全部记录行的数量
	例：select sum(c_age) from t_student;
		select avg(c_age) from t_student;
		select max(c_age) from t_student where c_gender = '男';
		select min(c_age) from t_student where c_gender = '女';
		select count(*) from t_student;
		select count(*) from t_student where c_gender = '女';
	
七、分组：
	语法： select 分组的字段名,聚合函数... from 表名 group by 分组字段名 having 分组后的条件 注意：在执行 group by 分组时，select 后只能有被分组的字段，不允许有其它字段,除非这些字段在聚合函数中
	执行分组时，group by 后面写了那个字段，select后就只能写那个字段。
	单字段分组：select c_gender from t_student group by c_gender;
	多字段分组：select c_gender,c_address from t_student group by c_gender,c_address;
	group_concat() 作用：根据分组结果，使用group_concat()来获取分组中指定字段的集合 语法：group_concat(字段名)
		代码:select c_gender,group_concat(c_name) from t_student group by c_gender;
	分组和聚和函数使用 单纯的使用分组并没有实际意义，需要使用聚合函数对数据进行处理
		select c_gender,max(c_age),min(c_age),sum(c_age),avg(c_age),count(*) from t_student group by c_gender;
		select c_gender,max(c_age),min(c_age),sum(c_age),avg(c_age),count(c_age) from t_student group by c_gender;
	having条件子句 having 作用和 where 类似,having 是对group by 分组后的数据进行筛选.
		select c_gender,group_concat(c_name) from t_student group by c_gender having c_gender = '女';
		select c_gender,group_concat(c_name) from t_student where c_age > 50 group by c_gender having c_gender = '女';
	分组汇总:	语法：with rollup
		select c_gender,count(*) from t_student group by c_gender with rollup;
	
八、多表查询数据：
	普通多表查询：语法：select 表名.字段 ... from 表名1，表名2..		
		select * from t_student,t_class;
	多表查询连接条件 在多表个表进行查询时，表与表之间应该是有有关系的，一般会以外键的形式来建立表间的关系	
		select t_student.c_name,t_class.c_name  from t_student,t_class where t_student.c_class_id = t_class.c_id;
	表别名在多表操作时，表的名字比较长。可以在查询时起别名语法： select 别名.字段名... from 表1 as 表1别名，表2 表2别名... [条件]
		select ts.c_name as '姓名' , tc.c_name '班级名' from t_student as ts,t_class tc where ts.c_class_id = tc.c_id;
	内连接查询 作用：查询的结果为两个表匹配到的数据 语法： select * from 表1 inner join 表2 on 表1.列 运算符 表2.列。。。尽量不要使用where
		select ts.c_name, tc.c_name from t_student as ts inner join t_class tc on ts.c_class_id = tc.c_id;
	左连接查询 作用：查询的结果为根据左表中的数据进行连接，如果右表中没有满足条件的记录，则连接空值。 语法： select * from 表1 left join 表2 on 表1.列 运算符 表2. 
		select ts.c_name, tc.c_name from t_student as ts left join t_class tc on ts.c_class_id = tc.c_id;
	右连接查询(了解) 作用：查询的结果为根据右表中的数据进行连接，如果左表中没有满足条件的记录，则连接空值。 语法： select * from 表1 right join 表2 on 表1.列 运算符 表2.
		select ts.c_name, tc.c_name from t_student as ts right join t_class tc on ts.c_class_id = tc.c_id;
	子查询 作用：作用：在一个 select 语句中,嵌入了另外一个 select 语句, 那么被嵌入的 select 语句称之为子查询语句 语法： select * from 表1 where 条件 运算符 （select 查询）
		select * from t_student where c_age > (select avg(c_age) from t_student);
		

	
	
	






