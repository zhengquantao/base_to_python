# 数据库和缓存（46题）

113.列举常见的关系型数据库和非关系型都有那些？
```text
关系型数据库(需要有表结构)
    mysql、oracle 、 spl、server、db2、sybase
非关系型数据库（是以key-value存储的，没有表结构）（NoSQL）
 MongoDB
MongoDB 是一个高性能，开源，无模式的文档型数据库，开发语言是C++。它在许多场景下可用于替代传统的关系型数据库或键/值存储方式。
 Redis
Redis 是一个开源的使用ANSI C语言编写、支持网络、可基于内存亦可持久化的日志型、Key-Value数据库，并提供多种语言的API。目前由VMware主持开发工作。
```
114.MySQL常见数据库引擎及比较？
```text
InnoDB 
支持事务
支持表锁、行锁（for update）
表锁：select * from tb for update
行锁：select id,name from tb where id=2 for update
myisam
查询速度快
全文索引
支持表锁
表锁：select * from tb for update
NDB
高可用、 高性能、高可扩展性的数据库集群系统
Memory 
默认使用的是哈希索引
```
115.简述数据库三大范式？
```text
 数据库的三大特性：
'实体':表
'属性'：表中的数据(字段)
'关系'：表与表之间的关系
----------------------------------------------------
# 数据库设计三大范式：
1：确保每列保持原子性（即数据库表中的所有字段值是不可分解的原子值）
2：确保表中的每列都是和主键相关（表中只能保存一种数据，不可以把多种数据保存在同一张表中）--->完全属于当前表的数据
3：确保每列都和主键直接相关，而不是间接相关（在一个数据库表中保存的数据只能与主键相关）----> 消除传递依赖（间接）
比如在设计一个订单数据表的时候，可以将客户编号作为一个外键和订单表建立相应的关系。
而不可以在订单表中添加关于客户其它信息（比如姓名、所属公司等）的字段。

数据库五大约束'
    1.primary KEY:设置主键约束；
    2.UNIQUE：设置唯一性约束，不能有重复值；
    3.DEFAULT 默认值约束    
    4.NOT NULL：设置非空约束，该字段不能为空；
    5.FOREIGN key :设置外键约束。
```
116、什么是事务？MySQL如何支持事务？
```text
事务用于将某些操作的多个SQL作为原子性操作，一旦有某一个出现错误，即可回滚到原来的状态，从而保证数据库数据完整性。

事务的特性： 
原子性: 确保工作单元内的所有操作都成功完成，否则事务将被中止在故障点，和以前的操作将回滚到以前的状态。
一致性: 确保数据库正确地改变状态后，成功提交的事务。
隔离性: 使事务操作彼此独立的和透明的。
持久性: 确保提交的事务的结果或效果的系统出现故障的情况下仍然存在。

Mysql实现事务
InnoDB支持事务，MyISAM不支持
    # 启动事务：
        # start transaction；
        # update from account set money=money-100 where name='a';
        # update from account set money=money+100 where name='b';
        # commit；
        'start transaction 手动开启事务，commit 手动关闭事务'
```
117.简述数据库设计中一对多和多对多的应用场景？
````text
FK(一对多)
下拉框里面的数据就需要用FK关联另一张表

M2M（多对多）
多选的下拉框，或者checkbox
````
119.常见SQL（必备）
```text
group by 分组对聚合的条件进行筛选需要通过havhing

SQL的left join 、right join、inner join之间的区别
left join (左连接) 返回包括左表中的所有记录和右表中联结字段相等的记录
right join(右连接) 返回包括右表中的所有记录1和左表中联结字段相等的记录
inner join（内连接）： 只返回两个表中联结字段相等的行
```
120.简述触发器、函数、视图、存储过程？
```text
触发器：
对数据库某张表的增加、删除，修改前后定义一些操作

函数：(触发函数是通过select)
聚合函数：max/sum/min/avg
时间格式化：date_format
字符串拼接：concat

存储过程：
将SQL语句保存到数据库中，并命名，以后在代码调用时，直接调用名称即可
参数类型：
　　in    只将参数传进去
　　out   只拿结果
　　inout 既可以传，可以取

函数与存储过程区别：
本质上没区别。只是函数有如：只能返回一个变量的限制。而存储过程可以返回多个。而函数是可以嵌入在sql中使用的,可以在select中调用，而存储过程不行。

视图：
视图是一个虚拟表，不是真实存在的（只能查，不能改）
```
121.MySQL索引种类
```text
单列
功能
   普通索引：加速查找
   唯一索引：加速查找 + 约束：不能重复（只能有一个空，不然就重复了）
   主键（primay key）：加速查找 + 约束：不能重复 +  不能为空
多列
　　联合索引（多个列创建索引）-----> 相当于单列的普通索引
　　联合唯一索引            -----> 相当于单列的唯一索引
　　ps：联合索引的特点：遵循最左前缀的规则
其他词语：
·· - 索引合并，利用多个单例索引查询；（例如在数据库查用户名和密码，分别给用户名和密码建立索引）
   - 覆盖索引，在索引表中就能将想要的数据查询到；
```
122.索引在什么情况下遵循最左前缀的规则？
```text
联合索引
```
123.主键和外键的区别？
```text
主键是能确定一条记录的唯一标示。例如，身份证证号
外键：用于与另一张表的关联，是能确定另一张表记录的字段，用于保持数据的一致性
```
124.MySQL常见的函数？
```text
聚合函数
max/sum/min/avg
时间格式化
date_format
字符串拼接
concat（当拼接了null，则返回null）
截取字符串
substring
返回字节个数
length
```
125.列举 创建索引但是无法命中索引的8种情况。
```text
1.- like '%xx'
    select * from tb1 where name like '%cn';
2.- 使用函数
    select * from tb1 where reverse(name) = 'wupeiqi';
3.- or
    select * from tb1 where nid = 1 or email = 'seven@live.com';
    特别的：当or条件中有未建立索引的列才失效，以下会走索引
            select * from tb1 where nid = 1 or name = 'seven';
            select * from tb1 where nid = 1 or email = 'seven@live.com' and name = 'alex'
4.- 类型不一致
    如果列是字符串类型，传入条件是必须用引号引起来，不然...
    select * from tb1 where name = 999;
5.- !=
    select * from tb1 where name != 'alex'
    特别的：如果是主键，则还是会走索引
        select * from tb1 where nid != 123
6.- >
    select * from tb1 where name > 'alex'
    特别的：如果是主键或索引是整数类型，则还是会走索引
        select * from tb1 where nid > 123
        select * from tb1 where num > 123
7.- order by
    select email from tb1 order by name desc;
    当根据索引排序时候，选择的映射如果不是索引，则不走索引
    特别的：如果对主键排序，则还是走索引：
        select * from tb1 order by nid desc;
8.- 组合索引最左前缀
    如果组合索引为：(name,email)
    name and email       -- 使用索引
    name                 -- 使用索引
    email                -- 不使用索引
```
126.如何开启慢日志查询？
```text

修改配置文件
slow_query_log = OFF                            是否开启慢日志记录
long_query_time = 2                              时间限制，超过此时间，则记录
slow_query_log_file = /usr/slow.log        日志文件
log_queries_not_using_indexes = OFF     为使用索引的搜索是否记录

下面是开启
slow_query_log = ON
long_query_time = 2   
log_queries_not_using_indexes = OFF 
log_queries_not_using_indexes = ON

注：查看当前配置信息：
　　     show variables like '%query%'
     修改当前配置：
　　　　set global 变量名 = 值
```
127.数据库导入导出命令（结构+数据）？
```text
导出现有数据库数据：（当有提示出入密码。-p就不用加密码）
  mysqldump -u用户名 -p密码 数据库名称 >导出文件路径           # 结构+数据
  mysqldump -u用户名 -p密码 -d 数据库名称 >导出文件    路径       # 结构 

导入现有数据库数据：
    mysqldump -uroot -p密码  数据库名称 < 文件路径  
```
128.数据库优化方案？
```text
1、创建数据表时把固定长度的放在前面（）
2、将固定数据放入内存： 例如：choice字段 （django中有用到，数字1、2、3…… 对应相应内容）
3、char 和 varchar 的区别(char可变, varchar不可变 )
　　
4、联合索引遵循最左前缀(从最左侧开始检索)
5、避免使用 select * 
6、读写分离
　　　　- 实现：两台服务器同步数据
　　　　- 利用数据库的主从分离：主，用于删除、修改、更新；从，用于查；
读写分离:利用数据库的主从进行分离：主，用于删除、修改更新；从，用于查
7、分库
　　　　- 当数据库中的表太多，将某些表分到不同的数据库，例如：1W张表时
　　　　- 代价：连表查询
8、分表
　　　　- 水平分表：将某些列拆分到另外一张表，例如：博客+博客详情
　　　　- 垂直分表：讲些历史信息分到另外一张表中，例如：支付宝账单
9、加缓存
　　　　- 利用redis、memcache （常用数据放到缓存里，提高取数据速度）
如果只想获取一条数据
     - select * from tb where name=‘alex’ limit 1
```
129.char和varchar的区别？
```text
char 和 varchar 的区别(char可变, varchar不可变 )
```
130.简述MySQL的执行计划
```text
查看有没有命中索引，让数据库帮看看运行速度快不快
explain select * from table;
当type为all时，是为全表索引
```
131.在对name做了唯一索引前提下，简述以下区别：  
```text
select * from tb where name = ‘Oldboy-Wupeiqi’   
select * from tb where name = ‘Oldboy-Wupeiqi’ limit 1
是这样的的，用where条件过滤出符合条件的数据的同时，进行计数，
比如limit 1，那么在where过滤出第1条数据后，他就会直接把结果select出来返回给你，整个过程就结束了。
没做唯一索引的话,前者查询会全表扫描,效率低些
limit 1,只要找到对应一条数据,就不继续往下扫描.
然而 name 字段添加唯一索引了,加不加limit 1,意义都不大;
```
132.1000w条数据，使用limit offset 分页时，为什么越往后翻越慢？如何解决？
```text
  答案一：
      先查主键，在分页。
      select * from tb where id in (
          select id from tb where limit 10 offset 30
      )
  答案二：
      按照也无需求是否可以设置只让用户看200页
  答案三：
      记录当前页  数据ID最大值和最小值
      在翻页时，根据条件先进行筛选；筛选完毕之后，再根据limit offset 查询。
      select * from (select * from tb where id > 22222222) as B limit 10 offset 0
      如果用户自己修改页码，也可能导致慢；此时对url种的页码进行加密（rest framework ）
```
133.什么是索引合并？
```text
1、索引合并是把几个索引的范围扫描合并成一个索引。
2、索引合并的时候，会对索引进行并集，交集或者先交集再并集操作，以便合并成一个索引。
3、这些需要合并的索引只能是一个表的。不能对多表进行索引合并。

简单的说，索引合并，让一条sql可以使用多个索引。对这些索引取交集，并集，或者先取交集再取并集。
从而减少从数据表中取数据的次数，提高查询效率。
```
134.什么是覆盖索引？
```text
在索引表中就能将想要的数据查询到
```
135.简述数据库读写分离？
```text
- 实现：两台服务器同步数据
　　　　- 利用数据库的主从分离：主，用于删除、修改、更新；从，用于查；
方式一:是视图里面用using方式可以进行指定到哪个数据读写
from django.shortcuts import render,HttpResponse
from app01 import models
def index(request):

    models.UserType.objects.using('db1').create(title='普通用户')
　　# 手动指定去某个数据库取数据
    result = models.UserType.objects.all().using('db1')
    print(result)

    return HttpResponse('...')

方式二：写配置文件
class Router1:
　　#  指定到某个数据库取数据
    def db_for_read(self, model, **hints):
        """
        Attempts to read auth models go to auth_db.
        """
        if model._meta.model_name == 'usertype':
            return 'db1'
        else:
            return 'default'
　　　# 指定到某个数据库存数据
    def db_for_write(self, model, **hints):
        """
        Attempts to write auth models go to auth_db.
        """
        return 'default'
再写到配置
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    },
    'db1': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
DATABASE_ROUTERS = ['db_router.Router1',]
```
136.简述数据库分库分表？（水平、垂直）
```text
 1、分库
    当数据库中的表太多，将某些表分到不同数据库，例如：1W张表时
    代价：连表查询跨数据库，代码变多
# 2、分表
    水平分表：将某些列拆分到另一张表，例如：博客+博客详情
    垂直分表：将某些历史信息，分到另外一张表中，例如：支付宝账单
```
137.redis和memcached比较？
```text
区别
1：redis不仅支持简单的key_value类型，还支持字典，字符串，列表，集合，有序集合类型
2：内存使用效率对比，使用简单的key-value存储的话，
   Memcached的内存利用率更高而如果Redis采用hash结构来做key-value存储，由于其组合式的压缩，其内存利用率会高于Memcached。
3.性能对比：由于Redis只使用单核，而Memcached可以使用多核，.
   所以平均每一个核上Redis在存储小数据时比Memcached性能更高。而在100k以上的数据中，Memcached性能要高于Redis，
4.Redis虽然是基于内存的存储系统，但是它本身是支持内存数据的持久化的，而且提供两种主要的持久化策略：RDB快照和AOF日志。
   而memcached是不支持数据持久化操作的。
5.集群管理不同，Memcached本身并不支持分布式，因此只能在客户端通过像一致性哈希这样的分布式算法来实现Memcached的分布式存储。
```
138.redis中数据库默认是多少个db 及作用？
```text
Redis默认支持16个数据库，可以通过配置databases来修改这一数字。客户端与Redis建立连接后会自动选择0号数据库，不过可以随时使用SELECT命令更换数据库
Redis支持多个数据库，并且每个数据库的数据是隔离的不能共享，并且基于单机才有，如果是集群就没有数据库的概念。
```
139.python操作redis的模块？
```text
- 连接
- 直接连接：
    import redis 
    r = redis.Redis(host='10.211.55.4', port=6379)
    r.set('foo', 'Bar')
    print r.get('foo')
- 连接池：
    import redis
    pool = redis.ConnectionPool(host='10.211.55.4', port=6379)
    r = redis.Redis(connection_pool=pool)
    r.set('foo', 'Bar')
    print r.get('foo')
```
140.如果redis中的某个列表中的数据量非常大，如果实现循环显示每一个值？
```text
- 如果一个列表在redis中保存了10w个值，我需要将所有值全部循环并显示，请问如何实现？
一个一个取值，列表没有iter方法，但能自定义
def list_scan_iter(name,count=3):
    start = 0
    while True:
        result = conn.lrange(name, start, start+count-1)
        start += count
        if not result:
            break
        for item in result:
            yield item

    for val in list_scan_iter('num_list'):
        print(val)
　　场景：投票系统，script-redis
```
141.redis如何实现主从复制？以及数据同步机制？
```text
优势：
    - 高可用
    - 分担主压力
注意： 
    - slave设置只读

从的配置文件添加以下记录，即可：
    slaveof 1.1.1.1 3306 
```
142.redis中的sentinel的作用？
```text
帮助我们自动在主从之间进行切换
检测主从中 主是否挂掉，且超过一半的sentinel检测到挂了之后才进行进行切换。
如果主修复好了，再次启动时候，会变成从。
启动主redis:
redis-server /etc/redis-6379.conf  启动主redis
redis-server /etc/redis-6380.conf  启动从redis
在linux中：
    找到 /etc/redis-sentinel-8001.conf  配置文件，在内部：
        - 哨兵的端口 port = 8001
        - 主redis的IP，哨兵个数的一半/1
    
    找到 /etc/redis-sentinel-8002.conf  配置文件，在内部：
        - 哨兵的端口 port = 8002
        - 主redis的IP, 1 
    启动两个哨兵   
```
143.如何实现redis集群？
```text
 redis集群、分片、分布式redis     
    redis-py-cluster
    集群方案：
        - redis cluster 官方提供的集群方案。
        - codis，豌豆荚技术团队。
        - tweproxy，Twiter技术团队。
    redis cluster的原理？
        - 基于分片来完成。
        - redis将所有能放置数据的地方创建了 16384 个哈希槽。
        - 如果设置集群的话，就可以为每个实例分配哈希槽：
            - 192.168.1.20【0-5000】
            - 192.168.1.21【5001-10000】
            - 192.168.1.22【10001-16384】
        - 以后想要在redis中写值时，
            set k1 123 
将k1通过crc16的算法，将k1转换成一个数字。然后再将该数字和16384求余，如果得到的余数 3000，那么就将该值写入到 192.168.1.20 实例中。
```
144.redis中默认有多少个哈希槽？
```text
16384
```
145.简述redis的有哪几种持久化策略及比较？
```text

RDB：每隔一段时间对redis进行一次持久化。
      - 缺点：数据不完整
      - 优点：速度快
AOF：把所有命令保存起来，如果想到重新生成到redis，那么就要把命令重新执行一次。
      - 缺点：速度慢，文件比较大
      - 优点：数据完整
```
146.列举redis支持的过期策略。
```text
  voltile-lru：    从已设置过期时间的数据集（server.db[i].expires）中挑选最近频率最少数据淘汰
  volatile-ttl：   从已设置过期时间的数据集（server.db[i].expires）中挑选将要过期的数据淘汰
  volatile-random：从已设置过期时间的数据集（server.db[i].expires）中任意选择数据淘汰

  
  allkeys-lru：       从数据集（server.db[i].dict）中挑选最近最少使用的数据淘汰
  allkeys-random：    从数据集（server.db[i].dict）中任意选择数据淘汰
  no-enviction（驱逐）：禁止驱逐数据
```
147.MySQL 里有 2000w 数据，redis 中只存 20w 的数据，如何保证 redis 中都是热点数据？ 
```text

  相关知识：redis 内存数据集大小上升到一定大小的时候，就会施行数据淘汰策略（回收策略）。redis 提供 6种数据淘汰策略：

  volatile-lru：从已设置过期时间的数据集（server.db[i].expires）中挑选最近最少使用的数据淘汰
  volatile-ttl：从已设置过期时间的数据集（server.db[i].expires）中挑选将要过期的数据淘汰
  volatile-random：从已设置过期时间的数据集（server.db[i].expires）中任意选择数据淘汰
  allkeys-lru：从数据集（server.db[i].dict）中挑选最近最少使用的数据淘汰
  allkeys-random：从数据集（server.db[i].dict）中任意选择数据淘汰
  no-enviction（驱逐）：禁止驱逐数据
```
148.写代码，基于redis的列表实现 先进先出、后进先出队列、优先级队列。
```text
 参看script—redis源码
from scrapy.utils.reqser import request_to_dict, request_from_dict

  from . import picklecompat


  class Base(object):
      """Per-spider base queue class"""

      def __init__(self, server, spider, key, serializer=None):
          """Initialize per-spider redis queue.

          Parameters
          ----------
          server : StrictRedis
              Redis client instance.
          spider : Spider
              Scrapy spider instance.
          key: str
              Redis key where to put and get messages.
          serializer : object
              Serializer object with ``loads`` and ``dumps`` methods.

          """
          if serializer is None:
              # Backward compatibility.
              # TODO: deprecate pickle.
              serializer = picklecompat
          if not hasattr(serializer, 'loads'):
              raise TypeError("serializer does not implement 'loads' function: %r"
                              % serializer)
          if not hasattr(serializer, 'dumps'):
              raise TypeError("serializer '%s' does not implement 'dumps' function: %r"
                              % serializer)

          self.server = server
          self.spider = spider
          self.key = key % {'spider': spider.name}
          self.serializer = serializer

      def _encode_request(self, request):
          """Encode a request object"""
          obj = request_to_dict(request, self.spider)
          return self.serializer.dumps(obj)

      def _decode_request(self, encoded_request):
          """Decode an request previously encoded"""
          obj = self.serializer.loads(encoded_request)
          return request_from_dict(obj, self.spider)

      def __len__(self):
          """Return the length of the queue"""
          raise NotImplementedError

      def push(self, request):
          """Push a request"""
          raise NotImplementedError

      def pop(self, timeout=0):
          """Pop a request"""
          raise NotImplementedError

      def clear(self):
          """Clear queue/stack"""
          self.server.delete(self.key)


  class FifoQueue(Base):
      """Per-spider FIFO queue"""

      def __len__(self):
          """Return the length of the queue"""
          return self.server.llen(self.key)

      def push(self, request):
          """Push a request"""
          self.server.lpush(self.key, self._encode_request(request))

      def pop(self, timeout=0):
          """Pop a request"""
          if timeout > 0:
              data = self.server.brpop(self.key, timeout)
              if isinstance(data, tuple):
                  data = data[1]
          else:
              data = self.server.rpop(self.key)
          if data:
              return self._decode_request(data)


  class PriorityQueue(Base):
      """Per-spider priority queue abstraction using redis' sorted set"""

      def __len__(self):
          """Return the length of the queue"""
          return self.server.zcard(self.key)

      def push(self, request):
          """Push a request"""
          data = self._encode_request(request)
          score = -request.priority
          # We don't use zadd method as the order of arguments change depending on
          # whether the class is Redis or StrictRedis, and the option of using
          # kwargs only accepts strings, not bytes.
          self.server.execute_command('ZADD', self.key, score, data)

      def pop(self, timeout=0):
          """
          Pop a request
          timeout not support in this queue class
          """
          # use atomic range/remove using multi/exec
          pipe = self.server.pipeline()
          pipe.multi()
          pipe.zrange(self.key, 0, 0).zremrangebyrank(self.key, 0, 0)
          results, count = pipe.execute()
          if results:
              return self._decode_request(results[0])


  class LifoQueue(Base):
      """Per-spider LIFO queue."""

      def __len__(self):
          """Return the length of the stack"""
          return self.server.llen(self.key)

      def push(self, request):
          """Push a request"""
          self.server.lpush(self.key, self._encode_request(request))

      def pop(self, timeout=0):
          """Pop a request"""
          if timeout > 0:
              data = self.server.blpop(self.key, timeout)
              if isinstance(data, tuple):
                  data = data[1]
          else:
              data = self.server.lpop(self.key)

          if data:
              return self._decode_request(data)


  # TODO: Deprecate the use of these names.
  SpiderQueue = FifoQueue
  SpiderStack = LifoQueue
  SpiderPriorityQueue = PriorityQueue
```
150.如何基于redis实现发布和订阅？以及发布订阅和消息队列的区别？
```text
 发布和订阅，只要有任务就给所有订阅者没人一份
  发布者：
      import redis

      conn = redis.Redis(host='127.0.0.1',port=6379)
      conn.publish('104.9MH', "hahaha")
  订阅者：
      import redis

      conn = redis.Redis(host='127.0.0.1',port=6379)
      pub = conn.pubsub()
      pub.subscribe('104.9MH')

      while True:
          msg= pub.parse_response()
          print(msg)
```
151.什么是codis及作用？
```text
 Codis 是一个分布式 Redis 解决方案, 对于上层的应用来说, 连接到 Codis Proxy 和连接原生的 Redis Server 没有明显的区别 
(不支持的命令列表), 上层应用可以像使用单机的 Redis 一样使用, Codis 底层会处理请求的转发, 不停机的数据迁移等工作,
 所有后边的一切事情, 对于前面的客户端来说是透明的, 可以简单的认为后边连接的是一个内存无限大的 Redis 服务.
```
152.什么是twemproxy及作用？
```text
  twemproxy是 Twtter 开源的一个 Redis 和 Memcache 代理服务器，主要用于管理 Redis 和 Memcached 集群，
减少与Cache 服务器直接连接的数量。
```
153.写代码实现redis事务操作。
```text
  import redis
  pool = redis.ConnectionPool(host='10.211.55.4', port=6379)
  conn = redis.Redis(connection_pool=pool)
  # pipe = r.pipeline(transaction=False)
  pipe = conn.pipeline(transaction=True)
  # 开始事务
  pipe.multi()

  pipe.set('name', 'bendere')
  pipe.set('role', 'sb')

  # 提交
  pipe.execute()
  
  注意：咨询是否当前分布式redis是否支持事务
```
154.redis中的watch的命令的作用？
```text
在Redis的事务中，WATCH命令可用于提供CAS(check-and-set)功能。
假设我们通过WATCH命令在事务执行之前监控了多个Keys，倘若在WATCH之后有任何Key的值发生了变化，
EXEC命令执行的事务都将被放弃，同时返回Null multi-bulk应答以通知调用者事务执行失败。
  
  面试题：你如何控制剩余的数量不会出问题？
      方式一：- 通过redis的watch实现
          import redis
          conn = redis.Redis(host='127.0.0.1',port=6379)

          # conn.set('count',1000)
          val = conn.get('count')
          print(val)

          with conn.pipeline(transaction=True) as pipe:

              # 先监视，自己的值没有被修改过
              conn.watch('count')

              # 事务开始
              pipe.multi()
              old_count = conn.get('count')
              count = int(old_count)
              print('现在剩余的商品有:%s',count)
              input("问媳妇让不让买？")
              pipe.set('count', count - 1)

              # 执行，把所有命令一次性推送过去
              pipe.execute()
     方式二 - 数据库的锁 
```
155.基于redis如何实现商城商品数量计数器？
```text
import redis

conn = redis.Redis(host='192.168.1.41',port=6379)

conn.set('count',1000)

with conn.pipeline() as pipe:

    # 先监视，自己的值没有被修改过
    conn.watch('count')

    # 事务开始
    pipe.multi()
    old_count = conn.get('count')
    count = int(old_count)
    if count > 0:  # 有库存
        pipe.set('count', count - 1)

    # 执行，把所有命令一次性推送过去
    pipe.execute()
```
156.简述redis分布式锁和redlock的实现机制。
```text
在不同进程需要互斥地访问共享资源时，分布式锁是一种非常有用的技术手段。 
有很多三方库和文章描述如何用Redis实现一个分布式锁管理器，但是这些库实现的方式差别很大
，而且很多简单的实现其实只需采用稍微增加一点复杂的设计就可以获得更好的可靠性。 
用Redis实现分布式锁管理器的算法，我们把这个算法称为RedLock。

实现
- 写值并设置超时时间
- 超过一半的redis实例设置成功，就表示加锁完成。
- 使用：安装redlock-py 
from redlock import Redlock

dlm = Redlock(
    [
        {"host": "localhost", "port": 6379, "db": 0},
        {"host": "localhost", "port": 6379, "db": 0},
        {"host": "localhost", "port": 6379, "db": 0},
    ]
)

# 加锁，acquire
my_lock = dlm.lock("my_resource_name",10000)
if  my_lock:
    # J进行操作
    # 解锁,release
    dlm.unlock(my_lock)
else:
    print('获取锁失败')
复制代码

 redis分布式锁？
# 不是单机操作，又多了一/多台机器
# redis内部是单进程、单线程，是数据安全的(只有自己的线程在操作数据)
----------------------------------------------------------------
\A、B、C，三个实例(主)
1、来了一个'隔壁老王'要操作，且不想让别人操作，so，加锁；
    加锁：'隔壁老王'自己生成一个随机字符串，设置到A、B、C里(xxx=666)
2、来了一个'邻居老李'要操作A、B、C，一读发现里面有字符串，擦，被加锁了，不能操作了，等着吧~
3、'隔壁老王'解决完问题，不用锁了，把A、B、C里的key：'xxx'删掉；完成解锁
4、'邻居老李'现在可以访问，可以加锁了
# 问题：
1、如果'隔壁老王'加锁后突然挂了，就没人解锁，就死锁了，其他人干看着没法用咋办？
2、如果'隔壁老王'去给A、B、C加锁的过程中，刚加到Ａ，'邻居老李'就去操作C了，加锁成功or失败？
3、如果'隔壁老王'去给A、B、C加锁时，C突然挂了，这次加锁是成功还是失败？
4、如果'隔壁老王'去给A、B、C加锁时，超时时间为5秒，加一个锁耗时3秒，此次加锁能成功吗？
# 解决
1、安全起见，让'隔壁老王'加锁时设置超时时间，超时的话就会自动解锁(删除key：'xxx')
2、加锁程度达到（1/2）+1个就表示加锁成功，即使没有给全部实例加锁；
3、加锁程度达到（1/2）+1个就表示加锁成功，即使没有给全部实例加锁；
4、不能成功，锁还没加完就过期，没有意义了，应该合理设置过期时间
# 注意
    使用需要安装redlock-py
----------------------------------------------------------------
from redlock import Redlock
dlm = Redlock(
    [
        {"host": "localhost", "port": 6379, "db": 0},
        {"host": "localhost", "port": 6379, "db": 0},
        {"host": "localhost", "port": 6379, "db": 0},
    ]
)
# 加锁，acquire
my_lock = dlm.lock("my_resource_name",10000)
if  my_lock:
    # 进行操作
    # 解锁,release
    dlm.unlock(my_lock)
else:
    print('获取锁失败')
\通过sever.eval(self.unlock_script)执行一个lua脚本，用来删除加锁时的key
```
157.什么是一致性哈希？Python中是否有相应模块？
```text
 一致性哈希
一致性hash算法（DHT）可以通过减少影响范围的方式，解决增减服务器导致的数据散列问题，从而解决了分布式环境下负载均衡问题；
如果存在热点数据，可以通过增添节点的方式，对热点区间进行划分，将压力分配至其他服务器，重新达到负载均衡的状态。
Python模块--hash_ring，即Python中的一致性hash
```
158.如何高效的找到redis中所有以aaa开头的key？
```text
redis 有一个keys命令。
# 语法：KEYS pattern
# 说明：返回与指定模式相匹配的所用的keys。
该命令所支持的匹配模式如下：
1、?：用于匹配单个字符。例如，h?llo可以匹配hello、hallo和hxllo等；
2、*：用于匹配零个或者多个字符。例如，h*llo可以匹配hllo和heeeello等；
2、[]：可以用来指定模式的选择区间。例如h[ae]llo可以匹配hello和hallo，但是不能匹配hillo。同时，可以使用“/”符号来转义特殊的字符
# 注意
KEYS 的速度非常快，但如果数据太大，内存可能会崩掉，
如果需要从一个数据集中查找特定的key，最好还是用Redis的集合结构(set)来代替。
```