### Python开发工程师笔试题3

> **答题要求**：将该项目从[地址1](<https://github.com/jackfrued/python-interview-2019>)或[地址2](<https://gitee.com/jackfrued/python-interview-2019>)**fork**到自己的[GitHub](<https://github.com/>)或[Gitee](https://gitee.com)仓库并在线填写答案，完成后以发送合并请求（**Pull Request**）的方式提交自己的工作成果，时间120分钟。

#### 答题人：何川

#### 题目：

1. 下面的Python代码会输出什么。

   ```Python
   print([(x, y) for x, y in zip('abcd', (1, 2, 3, 4, 5))])
   print({x: f'item{x ** 2}' for x in range(5) if x % 2})
   print(len({x for x in 'hello world' if x not in 'abcdefg'}))
   ```

   答案：

   ```
   [('a', 1), ('b', 2), ('c', 3), ('d', 4)]
   {1: 'item1', 3: 'item9'}
   8
   ```

2. 下面的Python代码会输出什么。

   ```Python
   from functools import reduce
   
   items = [11, 12, 13, 14] 
   print(reduce(int.__add__, map(lambda x: x // 2, filter(lambda x: x ** 2 > 150, items))))
   ```

   答案：

   ```
   1
   
   ```

3. 对于第2题的代码，如果要实现相同的功能，用生成式应该怎么写？

   答案：

   ```Python
   print(reduce(int.__add__, [x//2, for x in (for x in items if x ** 2> 150)]))
   
   ```

4. 用一行代码实现将字符串`k1:v1|k2:v2|k3:v3`处理成字典`{'k1': 'v1', 'k2': 'v2', 'k3': 'v3'}`。

   答案：

   ```Python
   {key: value for k_v.split(':', 0), k_v.split(':', 1) in [for k_v in 'k1:v1|k2:v2|k3:v3'.split('|', 0)]}
   ```

5. 写一个装饰函数的装饰器，实现如果函数的返回值是字符串类型，就将该字符串每个单词的首字母大写（不用考虑非英文字符串的情况）。

   答案：

   ```Python
   def Upper_case(func):
       if type(func) == str:
           new_str = ''
           for i in str.split(' '):
               i.capitalize()
               new_str += i
           return new_str 
                   
   ```

6. 下面的字典中保存了某些公司股票的代码（字典中的键）及价格（字典中的值，以美元为单位），用一行代码从中找出价格最高的股票对应的股票代码，再用一行代码将股价高于100美元的股票创建成一个新的字典。

   > 说明：美股的股票代码是指英文字母代码，如：AAPL、GOOG。

   ```Python
   prices = {
       'AAPL': 191.88,
       'GOOG': 1186.96,
       'IBM': 149.24,
       'ORCL': 48.44,
       'ACN': 166.89,
       'FB': 208.09,
       'SYMC': 21.29
   }
   ```

   答案：

   ```Python
   new_dict = sorted(prices.items, 'value')
   highest_stock = new_dict[-1]
   new_dict = {k: v for k, v in prices if v >= 100}

   ```

7. 写一个函数，返回删除列表中重复元素后的新列表，要求保留原有列表元素的顺序。

   答案：

   ```Python
   def foo(list1)
       list2 = []
       for i in list1:
           if i not in list2:
               list2.append(i)
       return list2
   ```

8. 写一个函数，该函数的参数是一个保存字符串的列表，列表中某个字符串出现次数占列表元素总数的半数以上，找出并返回这个字符串。

   答案：

   ```Python
   from collections import Counter
   def find_str(list):
       c = Counter(list)
       for item in c:
           if item.value >= len(list)/2:
               return item.key
   
   ```

9. MySQL关系型数据库中有三张表分别表示用户、房源和租房记录，表结构如下所示。

   用户表（`tb_user`）：

   ```
   +----------+-------------+------+-----+---------+----------------+
   | Field    | Type        | Null | Key | Default | Comment        |
   +----------+-------------+------+-----+---------+----------------+
   | userid   | int(11)     | NO   | PRI | NULL    | 用户编号        |
   | username | varchar(31) | NO   |     | NULL    | 用户姓名        |
   | usertel  | char(11)    | YES  |     | NULL    | 用户手机        |
   +----------+-------------+------+-----+---------+----------------+
   ```

   房源表（`tb_house`）

   ```
   +---------+--------------+------+-----+---------+----------------+
   | Field   | Type         | Null | Key | Default | Comment        |
   +---------+--------------+------+-----+---------+----------------+
   | houseid | int(11)      | NO   | PRI | NULL    | 房源编号        |
   | title   | varchar(255) | NO   |     | NULL    | 房源标题        |
   | area    | decimal(5,1) | NO   |     | NULL    | 房源面积        |
   | addr    | varchar(511) | NO   |     | NULL    | 房源地址        |
   | rented  | tinyint(1)   | YES  |     | 0       | 是否租出        |
   +---------+--------------+------+-----+---------+----------------+
   ```

   租房记录表（`tb_record`）

   ```
   +---------+---------+------+-----+---------+----------------+
   | Field   | Type    | Null | Key | Default | Comment        |
   +---------+---------+------+-----+---------+----------------+
   | recid   | int(11) | NO   | PRI | NULL    | 记录编号        |
   | userid  | int(11) | NO   | MUL | NULL    | 用户编号        |
   | houseid | int(11) | NO   | MUL | NULL    | 房源编号        |
   | indate  | date    | NO   |     | NULL    | 租赁日期        |
   | outdate | date    | YES  |     | NULL    | 退租日期        |
   +---------+---------+------+-----+---------+----------------+
   ```

   - 查询租过编号为1055的房源的用户姓名。
   - 查询租过三套以上房子且登记了手机号码的用户姓名。
   - 查询2018年被租过两次以上目前仍然处于出租状态且面积超过50平米的房源编号和标题。

   答案：

   ```SQL
   select t1.username 
   from tb_user t1 
   join tb_record t2 on t1.userid = t2.userid 
   where houseid = 1055;
   select t1.username from tb_user t1
   where usertrl <> null 
   join tb_record t2 on t1.userid = t2.userid
   where count(t2.userid)>=3;
   select t1.houseid, title
   from tb_house t1
   where area>=50 and rented=0
   join 
   (select houseid, indate
   from tb_record t2 
   where indate between 2018-1-1 and 2018-12-31) t3
   on t1.houseid = t3.houseid
   where count(t3.indate)>=2 
   ```

10. 请阐述访问一个用Django或Flask开发的Web应用，从用户在浏览器中输入网址回车到浏览器收到Web页面的整个过程中，到底发生了哪些事情，越详细越好。

    答案：

    ```
    1.浏览器对域名解析，找到对应的一个或多个IP地址，访问相关端口（一般是80/443）
    2.服务端监听相应端口的服务器或者代理服务器（uwsgi/nginx等）收到请求，将相关任务分发到
    a.静态服务器（nginx/apache等）获取静态资源b.通过视图调用数据库数据
    3.通过代理服务器返回数据到浏览器
    ```

11. 请阐述HTTPS的工作原理以及TCP是如何保证端到端可靠传输的。

    答案：

    ```
    
    ```

12. 在Linux系统中，假设Nginx的访问日志位于`/var/log/nginx/access.log`，该文件的每一行代表一条访问记录，每一行都由若干列（以制表键分隔）构成，其中第1列记录了访问者的IP地址，如下所示。请用一行命令找出最近的100000次访问中，访问频率最高的IP地址及访问次数。

    ```
    221.228.143.52 - - [23/May/2019:08:57:42 +0800] ""GET /about.html HTTP/1.1"" 206 719996
    218.79.251.215 - - [23/May/2019:08:57:44 +0800] ""GET /index.html HTTP/1.1"" 206 2350253
    220.178.150.3 - - [23/May/2019:08:57:45 +0800] ""GET /index.html HTTP/1.1"" 200 2350253
    218.79.251.215 - - [23/May/2019:08:57:52 +0800] ""GET /index.html HTTP/1.1"" 200 2350253
    219.140.190.130 - - [23/May/2019:08:57:59 +0800] ""GET /index.html HTTP/1.1"" 200 2350253
    221.228.143.52 - - [23/May/2019:08:58:08 +0800] ""GET /about.html HTTP/1.1"" 206 719996
    221.228.143.52 - - [23/May/2019:08:58:08 +0800] ""GET /news.html HTTP/1.1"" 206 713242
    221.228.143.52 - - [23/May/2019:08:58:09 +0800] ""GET /products.html HTTP/1.1"" 206 1200250
    ```

    答案：

    ```Shell
    
    ```