```
姓名：彭海峰
角色名：peng_hai_feng_res_view
用户名：peng_hai_feng
密码：123
```

首先，我根据实验要求运行了第一段查询语句
<br>
截图如下
<br>
![第一段查询语句的运行截图](https://github.com/phf449540929/Oracle/blob/master/test1/20181010095753.png)
<br>
紧接着，我又运行了第二段查询语句
<br>
截图如下
<br>
![第二段查询语句的运行截图](https://github.com/phf449540929/Oracle/blob/master/test1/20181010095729.png)
<br>
之后，我根据实验要求，仔细比对了一下两次查询的运行时间
<br>
第一次运行的时间是
<br>
![第一段查询语句的运行时间](https://github.com/phf449540929/Oracle/blob/master/test1/01.png)
<br>
可以看到是0.02秒
<br>
第二次运行的时间是
<br>
![第一段查询语句的运行时间](https://github.com/phf449540929/Oracle/blob/master/test1/02.png)
<br>
可以看到是0.34秒
<br>
虽然时间都很短，但明显可以看到第一段查询语句的时间是少于第二段查询语句的
<br>
根据实验要求，于是将第一段查询语句进行代码优化
<br>
可以看到代码优化之后的截图
<br>
![第二段查询语句的运行截图](https://github.com/phf449540929/Oracle/blob/master/test1/20181010095707.png)
<br>
根据提示，说的建一个索引可以优化查询
<br>
经过编辑，我对查询加了索引
<br>
```
CREATE NONCLUSTERED INDEX IX_TEST_TNAME
ON TEST(hr.departments d，hr.employees e)
WITH FILLFACTOR = 30
GO
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
from TEST(hr.departments d，hr.employees e)
where d.department_id = e.department_id
and d.department_name in ('IT'，'Sales')
GROUP BY department_name;
```
<br>
可以看到，我为这个查询新建了一个索引
<br>
并使用索引对整个查询进行了优化
<br>
这个索引的优化能稍微增加查询的运行速度
<br>
毕竟索引存在的本身可以理解为一种特殊的目录
<br>
我在这个特殊的目录中进行查询
<br>
自然速度会稍微快一点
