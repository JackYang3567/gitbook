# Redis应用

## 0、Redis运行中常见错误
### 0.1、MISCONF Redis is configured to save RDB snapshots
 **错误描述：** ReplyError: MISCONF Redis is configured to save RDB snapshots, but it is currently not able to persist on disk.   
 **解决方案：** 127.0.0.1:6379> config set stop-writes-on-bgsave-error no

---

## 1、Redis 数据类型

Redis是key-value存储, key键的命名显得比较重要，键分隔符和命名约定  

### 1.0、Redis 键（keys）
Redis key值是二进制安全的，这意味着可以用任何二进制序列作为key值，从形如”foo”的简单字符串到一个JPEG文件的内容都可以。空字符串也是有效key值。  
关于key的几条规则：  

#### 1.0.1、Redis key的设计规则：
 - 太长的键值不是个好主意，不仅因为消耗内存，而且在数据中查找这类键值的计算成本很高。
 - 太短的键值通常也不是好主意，如果你要用”u:1000:pwd”来代替”user:1000:password”，这没有什么问题，但后者更易阅读， 并且由此增加的空间消耗相对于key object和value object本身来说很小。当然，没人阻止您一定要用更短的键值节省一丁点儿空间。
 - 最好坚持一种模式。例如："object-type: id :field"就是个不错的注意，像这样"user:1000:password"。
 - Redis模式文档格式如下：以一个简单的图书应用来说。  

#### 1.0.2、 Redis模式形成文档，便于查阅
| Key 名称 | Redis数据类型 | 描述 | 关系 |
| :--------------- | :---------------- | :--------- |:-----------|
| book:{counter} | 哈希（Hashes） | 存储了书名、作者、ISBN、格式、版权日期、页码数、价格等图书元数据（或图书的一个对象实例/相当于关于数据中一条记录） | 键存储在体裁集合和销售排行有序集合中|
| books:{genre} | 集合（Sets) | 按照图书体裁进行分类的Redis键集合，例如通俗小说，推理、科幻、技术书籍 | 存储了所有按照单一体裁进行分类的图书键。与其他体裁集合一起，通过使用SINTERSTORE命令计算多体裁的图书，以及通过使用SDIFFSTORE计算单一体裁的图书|
| books:sales-rank | 有序集合(Sorted sets) | 存储每种图书的销售排行，以销售的名词作为有序集合的分值 |存储所有Redis图书键的排名 |



支持多种类型的数据结构，如 字符串（strings）， 散列（hashes）， 列表（lists）， 集合（sets）， 有序集合（sorted sets） 与范围查询， bitmaps， hyperloglogs 和 地理空间（geospatial） 索引半径查询

### 1.1、Redis 字符串（strings）数据类型
**strings** 是最简单Redis类型。当你使用用这种类型，Redis就像一个可以持久化的memcached服务器（注：memcache的数据仅保存在内存中，服务器重启后，数据将丢失）。  
在redis-cli中实践
* 1、set  和 get 来设置和获取字符串值。
  - **set** : 后跟key 和 value
  - **get** :后只跟key  

```
127.0.0.1:6379> set mykey somevalue
OK
127.0.0.1:6379> get mykey
"somevalue"
```

* 2、nx 当key存在时SET会失败，或相反的，xx 当key不存在时它只会成功。  
  - **nx** :前面是 set key  value
  - **xx** :前面是 set key  value 

```
> set mykey newval nx  
(nil)
> set mykey newval xx
OK
```
 * 3、**incr、incrby** 原子递增， 原子递减 **decr、decrby** 
   - **incr** : 后只跟key 且自动加1
   - **incrby** :后只跟key 且要指定相加的数字
   - **decr** : 后只跟key 且自动减1
   - **decrby** :后只跟key 且要指定相减的数字  

```
> set counter:book 100
OK
> incr counter:book
(integer) 101
> incr counter:book
(integer) 102
> incrby counter:book 50
(integer) 152
127.0.0.1:6379> decr counter:book
(integer) 151
127.0.0.1:6379> decrby counter:book 10
(integer) 141
```

 * 4、**mset 和 mget** 一次存储或获取多个key对应的值

```
> mset a 10 b 20 c 30
OK
> mget a b c
1) "10"
2) "20"
3) "30"
```
 * 5、**type、exists、 del** 修改或查询键空间  
   - **type** : 返回key对应的值的存储类型
   - **exists** :返回1或0标识给定key的值是否存在
   - **del** : 返回1或0标识给定key的值是否存在 

```
> type mykey  
string
> exists mykey
(integer) 1
> del mykey
(integer) 1
> exists mykey
(integer) 0
```   

 * 6、**expire** 对key设置一个超时时间，当这个时间到达后会被删除。精度可以使用毫秒或秒。   
   - **expire** : 对key设置一个超时时间
   - **persist** : 去除超时时间
   - **ex** :创建值的时候设置超时时间
   - **ttl** : 查看key对应的值剩余存活时间 

```
> set mykey "Hello"
OK
> expire mykey 10
(integer) 1
> ttl mykey
(integer) 10
> persist mykey
(integer) 1
> ttl mykey
(integer) -1
> set mykey "Hello" ex 50
```

### 1.2、Redis 散列（hashes数据类型
### 1.3、Redis 列表（lists）
### 1.4、Redis 集合（sets）
### 1.5、Redis 有序集合（sorted sets）
### 1.6、Redis  bitmaps
### 1.7、Redis  hyperloglogs 和 地理空间（geospatial） 索引半径查询
### 1.8、Redis  Redis 发布/订阅（Pub/Sub）



---

## 2、 Redis应用场景

Redis是一个key-value存储系统，现在在各种系统中的使用越来越多，大部分情况下是因为其高性能的特性，被当做缓存使用，这里介绍下Redis经常遇到的使用场景
 1. 每个服务每1s 从数据库获取数据，更新到缓存
 2. 所有的客户端请求都直接从 缓存里面读取
 3. 如果有人更新数据库，广播给所有客户端(redis publish), 立即更新缓存。
这样，即能保证用户永远能最快拿到数据， 性能也是最大化的

Redis在很多方面与其他数据库解决方案不同：它使用内存提供主存储支持，而仅使用硬盘做持久性的存储;它的数据模型非常独特，用的是单线程。另一个大区别在于，你可以在开发环境中使用Redis的功能，但却不需要转到Redis。
转向Redis当然也是可取的，许多开发者从一开始就把Redis作为首选数据库;但设想如果你的开发环境已经搭建好，应用已经在上面运行了，那么更换数据库框架显然不那么容易。另外在一些需要大容量数据集的应用，Redis也并不适合，因为它的数据集不会超过系统可用的内存。所以如果你有大数据应用，而且主要是读取访问模式，那么Redis并不是正确的选择。
然而我喜欢Redis的一点就是你可以把它融入到你的系统中来，这就能够解决很多问题，比如那些你<font color="red">现有的数据库处理起来感到缓慢的任务</font>。这些你就<font color="red">可以通过 Redis来进行优化</font>，或者为应用创建些新的功能。在本文中，我就想探讨一些怎样将Redis加入到现有的环境中，并利用它的原语命令等功能来解决 传统环境中碰到的一些常见问题。在这些例子中，Redis都不是作为首选数据库。
### 2.1、显示最新的项目列表
下面这个语句常用来显示最新项目，随着数据多了，查询毫无疑问会越来越慢。
SELECT * FROM foo WHERE … ORDER BY time DESC LIMIT 10
在Web应用中，“列出最新的回复”之类的查询非常普遍，这通常会带来可扩展性问题。这令人沮丧，因为项目本来就是按这个顺序被创建的，但要输出这个顺序却不得不进行排序操作。
类似的问题就可以用Redis来解决。比如说，我们的一个Web应用想要列出用户贴出的最新20条评论。在最新的评论边上我们有一个“显示全部”的链接，点击后就可以获得更多的评论。
我们假设数据库中的每条评论都有一个唯一的递增的ID字段。
我们可以使用分页来制作主页和评论页，使用Redis的模板，每次新评论发表时，我们会将它的ID添加到一个Redis列表：
LPUSH latest.comments
我们将列表裁剪为指定长度，因此Redis只需要保存最新的5000条评论：
LTRIM latest.comments 0 5000
每次我们需要获取最新评论的项目范围时，我们调用一个函数来完成(使用伪代码)：
```
FUNCTION get_latest_comments(start, num_items):
    id_list = redis.lrange(“latest.comments”,start,start+num_items – 1)
    IF id_list.length < num_items
       id_list = SQL_DB(“SELECT … ORDER BY time LIMIT …”)
    END
    RETURN id_list
END
```

这里我们做的很简单。在Redis中我们的最新ID使用了常驻缓存，这是一直更新的。但是我们做了限制不能超过5000个ID，因此我们的获取ID函数会一直询问Redis。只有在start/count参数超出了这个范围的时候，才需要去访问数据库。
我们的系统不会像传统方式那样“刷新”缓存，Redis实例中的信息永远是一致的。SQL数据库(或是硬盘上的其他类型数据库)只是在用户需要获取“很远”的数据时才会被触发，而主页或第一个评论页是不会麻烦到硬盘上的数据库了。
### 2.2、删除与过滤
我们可以使用LREM来删除评论。如果删除操作非常少，另一个选择是直接跳过评论条目的入口，报告说该评论已经不存在。
有些时候你想要给不同的列表附加上不同的过滤器。如果过滤器的数量受到限制，你可以简单的为每个不同的过滤器使用不同的Redis列表。毕竟每个列表只有5000条项目，但<font color="red">Redis却能够使用非常少的内存来处理几百万条项目</font>。
### 2.3、排行榜相关
另一个很普遍的需求是各种数据库的数据并非存储在内存中，因此在按得分排序以及实时更新这些几乎每秒钟都需要更新的功能上数据库的性能不够理想。
典型的比如那些在线游戏的排行榜，比如一个Facebook的游戏，根据得分你通常想要：

- 列出前100名高分选手
- 列出某用户当前的全球排名
这些操作对于Redis来说小菜一碟，即使你有几百万个用户，每分钟都会有几百万个新的得分。

模式是这样的，每次获得新得分时，我们用这样的代码：

ZADD leaderboard

你可能用userID来取代username，这取决于你是怎么设计的。

得到前100名高分用户很简单：ZREVRANGE leaderboard 0 99。

用户的全球排名也相似，只需要：ZRANK leaderboard 。

### 2.4、按照用户投票和时间排序
排行榜的一种常见变体模式就像Reddit或Hacker News用的那样，新闻按照类似下面的公式根据得分来排序：
score = points / time^alpha
因此用户的投票会相应的把新闻挖出来，但时间会按照一定的指数将新闻埋下去。下面是我们的模式，当然算法由你决定。
模式是这样的，开始时先观察那些可能是最新的项目，例如首页上的1000条新闻都是候选者，因此我们先忽视掉其他的，这实现起来很简单。
每次新的新闻贴上来后，我们将ID添加到列表中，使用LPUSH + LTRIM，确保只取出最新的1000条项目。
有一项后台任务获取这个列表，并且持续的计算这1000条新闻中每条新闻的最终得分。计算结果由ZADD命令按照新的顺序填充生成列表，老新闻则被清除。这里的关键思路是排序工作是由后台任务来完成的。
### 2.5、处理过期项目
另一种常用的项目排序是按照时间排序。我们使用unix时间作为得分即可。
模式如下：
– 每次有新项目添加到我们的非Redis数据库时，我们把它加入到排序集合中。这时我们用的是时间属性，current_time和time_to_live。
– 另一项后台任务使用ZRANGE…SCORES查询排序集合，取出最新的10个项目。如果发现unix时间已经过期，则在数据库中删除条目。
### 2.6、计数
Redis是一个很好的计数器，这要感谢INCRBY和其他相似命令。
我相信你曾许多次想要给数据库加上新的计数器，用来获取统计或显示新信息，但是最后却由于写入敏感而不得不放弃它们。
好了，现在使用Redis就不需要再担心了。有了原子递增(atomic increment)，你可以放心的加上各种计数，用GETSET重置，或者是让它们过期。
例如这样操作：
```
INCR user: EXPIRE
user: 60
```
你可以计算出最近用户在页面间停顿不超过60秒的页面浏览量，当计数达到比如20时，就可以显示出某些条幅提示，或是其它你想显示的东西。
### 2.7、特定时间内的特定项目
另一项对于其他数据库很难，但Redis做起来却轻而易举的事就是统计在某段特点时间里有多少特定用户访问了某个特定资源。比如我想要知道某些特定的注册用户或IP地址，他们到底有多少访问了某篇文章。
每次我获得一次新的页面浏览时我只需要这样做：
SADD page:day1:
当然你可能想用unix时间替换day1，比如time()-(time()%3600*24)等等。
想知道特定用户的数量吗?只需要使用SCARD page:day1: 。
需要测试某个特定用户是否访问了这个页面?SISMEMBER page:day1: 。
### 2.8、实时分析正在发生的情况，用于数据统计与防止垃圾邮件等
我们只做了几个例子，但如果你研究Redis的命令集，并且组合一下，就能获得大量的实时分析方法，有效而且非常省力。使用Redis原语命令，更容易实施垃圾邮件过滤系统或其他实时跟踪系统。
### 2.9、Pub/Sub
Redis的Pub/Sub非常非常简单，运行稳定并且快速。支持模式匹配，能够实时订阅与取消频道。
### 2.10、高并发频繁写入场景——（聊天系统、作为不同进程间传递消息的队列）使用 队列
你应该已经注意到像list push和list pop这样的Redis命令能够很方便的执行队列操作了，但能做的可不止这些：比如Redis还有list pop的变体命令，能够在列表为空时阻塞队列。
现代的互联网应用大量地使用了消息队列(Messaging)。消息队列不仅被用于系统内部组件之间的通信，同时也被用于系统跟其它服务之间的交互。消息队列的使用可以增加系统的可扩展性、灵活性和用户体验。非基于消息队列的系统，其运行速度取决于系统中最慢的组件的速度(注：短板效应)。而基于消息队列可以将系统中各组件解除耦合，这样系统就不再受最慢组件的束缚，各组件可以异步运行从而得以更快的速度完成各自的工作。
此外，<font color="red">当服务器处在高并发操作的时候，比如频繁地写入日志文件。可以利用消息队列实现异步处理。从而实现高性能的并发操作</font>。
### 2.11、缓存
Redis的缓存部分值得写一篇新文章，我这里只是简单的说一下。Redis能够替代memcached，让你的缓存从只能存储数据变得能够更新数据，因此你不再需要每次都重新生成数据了。

---

## 3、 Redis在编程语言中的应用

### 3.1、 Redis在Node.js中应用
#### 3.1.1、 Redis在Egg中应用
 * 1、安装ioredis、egg-redis

```
 yarn add ioredis
 yarn add egg-redis
```

 * 2、开启插件，/config/plugin.js

```
 exports.redis = {
  enable: true,
  package: 'egg-redis',
};
```

* 3、配置应用，/config/config.default.js

```
config.redis = {
    client: {
      port: 6379,          // Redis port
      host: '127.0.0.1',   // Redis host
      password: '',
      db: 0,
    },
};
```

* 4、Redis命令实例

```
async captcha() {
    const { ctx, logger, app  } = this    
    const { type } = {...ctx.params, ...ctx.query} 
    const captcha = svgCaptcha.create({
        noise:5, color: true, 
        background: '#cc9966',
        ignoreChars: '0o1i'})
    const captchaText = (captcha.text).toLowerCase()
     if ( 1 == parseInt(type)) {
        <font color="green">//把登录验证码保存到redis中</font>
        await app.redis.setex(`captcha:signin:${captchaText}`,180, captchaText)        
    } else {
         <font color="green">// 注册验证码保存到redis中</font>
        await app.redis.setex(`captcha:signup:${captchaText}`,180,  captchaText)
    }
    //req.session.captcha = captcha.text;   
    ctx.status = 200
  	ctx.type = 'svg'
    ctx.body = captcha.data
}
```

#### 3.1.2、 Redis在Koa中应用 

#### 3.1.3、 Redis在Express中应用

### 3.2、 Redis在Go Web中应用


### 3.3、 Redis在PHP中应用
