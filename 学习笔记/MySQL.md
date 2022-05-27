# 表的理解

数据库当中是以表格的形式表示数据的。

任何一张表都有行和列：

行（Row）：被称为数据/记录

列（column）：被称为字段，如姓名、性别、年龄等

每一个字段都有：字段名、数据类型、约束等属性。



常用命令：

```sql
show databases;

use test;

show tables;

desc 表名;  describe

查看数据库的版本号
select version();
使用的哪个数据库
select database();



```





# Sql 分类

- DQL：数据查询语言（凡是带有select关键字的都是查询语句）
- DML：数据操作语言（凡是对表当中的数据进行增删改的都是DML）
- DDL：数据定义语言（凡事带有create, drop, alter的都是DDL，DDL主要操作表的结构，不是表中的数据）
- TCL：事务控制语言，commit, rollback
- DCL：数据控制语言，例如：授权 grant, revoke等







select * 不建议在开发中使用：

1. 效率低
2. 可读性差，没办法看到有哪些字段



# 列起别名

```sql
select deptno, dname as deptname from dept;
```

使用 as 关键字起别名，省略 as 也可以

如果想起的别名含有空格怎么办？

```sql
select deptno, dname 'dept name' from dept; 双引号也行
```



# 列参与数学运算

```sql
select ename, sal * 12 as an_sal from emp; 
```

把 sal 字段 * 12





# 条件查询

```sql
select empno, ename from emp where sal = 800;

select empno, ename from emp where sal != 800;
select empno, ename from emp where sal <> 800;  不等于
```

<>或 != 不等于

< 小于

<= 小于等于

between .. and ... 两个值之间

注意：使用 between .. and 必须遵循左小右大，且是闭区间，包括两端的值



is null 为空

is not null 不为空

在数据库中 null 表示啥也没有，不是一个值，所以不能用值衡量

and 并且

```sql
select empno, ename, job, sal from emp where job = 'MANAGER' and sal > 2500
```



or 

```sql
查询工资大于2500并且部门编号为10或者20的员工
select * from emp where sal > 2500 and deptno = 10 or deptno = 20;
这个问题在于 and 的优先级比 or 高，所以是前半句 or deptno = 20;
正确：
select * from emp where sal > 2500 and (deptno = 10 or deptno = 20);
```



in 包含， 相当于多个 or

not in 不包含

```sql
查询工作岗位是MANAGER和SALESMAN的员工
select empno, ename, job from emp where job = 'MANAGER' or job = 'SALESMAN';
select empno, ename, job from emp where job in ('MANAGER','SALESMAN');
```

in 后面 不是一个区间，而是具体的值, not in 同理



like 模糊查询(fuzzy search)，支持 % 或下划线匹配   percent sign   underscore   hyphen    en-dash    em-dash

% 匹配任意个字符

一个下划线只能匹配一个字符

```sql
```







