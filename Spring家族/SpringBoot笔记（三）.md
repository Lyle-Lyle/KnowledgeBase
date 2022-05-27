# Redis



## NoSQL概述





# Redis安装和部署

https://juejin.cn/post/7054559356708192270





# 基本操作

Redis 并不具有MySQL那样的严格的表结构，Redis是一个键值数据库，因此，可以像Map一样的操作方式，通过键值对向 Redis 数据库中添加数据

在 Redis下，数据库是由一个整数索引标识，而不是有一个数据库名称。默认情况下，我们连接 Redis 数据库之后，会使用0号数据库。我们可以通过 Redis 配置文件中的参数来修改数据库总数，默认为16个。

我们可以通过 select 语句进行切换:

```
select 序号;
```



## 数据操作

向 Redis 中添加数据:

```sql
set <key> <value>
-- 一次性多个
mset [<key> <value>]...
```

所有存入的数据默认会以字符串的形式保存，键值具有一定的命名规范，以方便我们可以快速定位我们的数据属于哪个部分，比如用户的数据：

```sql
-- 使用冒号来进行板块分割，比如下面表示用户XXX的信息中的name属性，值为lbw
set user:info:用户ID:name lbw
```

我们可以通过键值获取存入的值：

```sql
get <key>
```

支持数据的过期时间设定

```sql
set <key> <value> EX 秒
set <key> <value> PX 毫秒
```

当数据到达指定时间时，会被自动删除，我们也可以单独为其他的键值对设置过期时间：

```sql
expire <key> 秒
```

通过下面的命令来查询某个键值对的过期时间还剩多少：

```
ttl <key>
-- 毫秒显示
pttl <key>
-- 转换为永久
persist <key>
```

当我们想直接删除某个数据，直接使用

```
del <key>
```

删除命令可以同时拼接多个键值一起删除

当我们想要查看数据库中所有的键值时：

```
keys *
```

也可以查询某个键是否存在：

```
exists <key>
```

也可以随机拿一个键

```
randomkey
```

我们可以将一个数据库中的内容移动到另一个数据库中：

```
move <key> 数据库序号
```

修改一个键为另一个键

```
rename <key> <新的名称>
-- 下面这个会检查新的名称是否已经存在
renamex <key> <新的名称>
```

如果存放的数据是一个数字，我们还可以对其进行自增自减操作：

```
-- 等价于a = a + 1
incr <key>
-- 等价于 a = a + b
incrby <key> b
-- 等价于 a = a - 1
decr <key>
```

最后就是查看值的数据类型：

```
type <key>
```

Redis 数据库也支持多种数据类型，但是它更偏向于我们在Java中认识的那些数据类型



# 数据类型

一个键值对除了存储一个String类型的值以外，还支持多种常用的数据类型。

## Hash

这种类型本质上就是一个HashMap, 也就是嵌套一个HashMap罢了，在Java中就像这样：

```java
#Redis默认存String类似于这样：
Map<String, String> hash = new HashMap<>();
#Redis存Hash类型的数据类似于这样：
Map<String, Map<String, String>> hash = new HashMap<>();
```

它比较适合存储类这样的数据，由于值本身又是一个Map，因此我们可以在此Map中放入类的各种属性和值，以实现一个Hash数据类型存储一个类的数据。

我们可以像这样来添加一个Hash类型的数据：

```
haset <key> [<字段> <值>]
```

我们可以直接获取：

```
hget <key> <字段>
-- 如果想要一次性获取所有的字段和值
hgetall <key>
```

同样的，我们也可以判断某个字段是否存在：

```
hexists <key> <字段>
```

删除Hash中的某个字段：

```
hdel <key>
```

我们发现，在操作一个Hash时，实际上就是我们普通操作命令前面添加一个 h ，就不一一列出所有操作了，看几个比较特殊的：

想知道 Hash 中一共存了多少个键值对：

```
hlen <key>
```

我们也可以一次性获取所有字段的值：

```
hvals <key>
```

唯一需要注意的是，Hash中只能存放字符串值，不允许出现嵌套的情况。

## List

它就是一个列表，列表中存放一系列的字符串，它支持随机访问，支持双端操作，就像我们使用Java中的LinkedList一样。

我们可以直接向一个已存在或是不存在的List中添加数据，如果不存在，会自动创建

```
-- 向列表头部添加元素
lpush <key> <element>
-- 向列表尾部添加元素
rpush <key> <element>
-- 在指定元素前面/后面插入元素
linsert <key> before/after <指定元素> <element>
```

同样的，获取元素也非常简单：

```
-- 根据下表获取元素
lindex <key> <element>
-- 向列表尾部添加元素
lpush <key> <element>
-- 在指定元素前面/后面插入元素
linsert <key> before/after <指定元素> <element>
```

同样的，获取元素也非常简单：

```
-- 根据下标获取元素
lindex <key> <下标>
-- 获取并移除头部元素
lpop <key>
-- 获取并移除尾部元素
rpop <key>
-- 获取指定范围内的
lrange <key> start stop
```

注意下标可以使用负数来表示从后到前数的数组

```
-- 获取列表a中的全部元素
lrange a 0-1
```

没想到吧，push和pop还能连着用呢：





















