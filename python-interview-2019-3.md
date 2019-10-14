### Python开发工程师笔试题3

> **答题要求**：将该项目从[地址1](<https://github.com/jackfrued/python-interview-2019>)或[地址2](<https://gitee.com/jackfrued/python-interview-2019>)**fork**到自己的[GitHub](<https://github.com/>)或[Gitee](https://gitee.com)仓库并在线填写答案，完成后以发送合并请求（**Pull Request**）的方式提交自己的工作成果，时间120分钟。

#### 答题人：

#### 题目：

1. 下面的Python代码会输出什么。

   ```Python
   print([(x, y) for x, y in zip('abcd', (1, 2, 3, 4, 5))])
   print({x: f'item{x ** 2}' for x in range(5) if x % 2})
   print(len({x for x in 'hello world' if x not in 'abcdefg'}))
   ```

   答案：

   ```
   (1) ('a', 1) , ('b', 2), ('c', 3), ('d', 4)
   (2) 0, 4, 16
   (3) 9
   ```

2. 下面的Python代码会输出什么。

   ```Python
   from functools import reduce

   items = [11, 12, 13, 14] 
   print(reduce(int.__add__, map(lambda x: x // 2, filter(lambda x: x ** 2 > 150, items))))
   ```

   答案：

   ```
   13
   ```

3. 对于第2题的代码，如果要实现相同的功能，用生成式应该怎么写？

   答案：

   ```Python
   from functools import reduce
   items = [11, 12, 13, 14]
   print([reduce(item) for item in items if item % 2 == 0 or (item ** 2 > 150 and item % 2 == 0)])
   ```

4. 用一行代码实现将字符串`k1:v1|k2:v2|k3:v3`处理成字典`{'k1': 'v1', 'k2': 'v2', 'k3': 'v3'}`。

   答案：

   ```Python
   new_dict = 
   ```

5. 写一个装饰函数的装饰器，实现如果函数的返回值是字符串类型，就将该字符串每个单词的首字母大写（不用考虑非英文字符串的情况）。

   答案：

   ```Python
   def decoretor(func):
       def wraps(*args, **kwargs):
           content = func(*args, **kwargs)
           if isinstance(content, str):
               content.title()
           return content
       return wraps
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
   print([items for items in prices.items() if items[1] == max(prices.values())])
   print(dict([items for items in prices.items() if items[1] > 100]))
   ```

7. 写一个函数，返回删除列表中重复元素后的新列表，要求保留原有列表元素的顺序。

   答案：

   ```Python
   def remove_list(l):
       l1 = l
       l1 = list(set(l1))
       return l1
   ```

8. 写一个函数，该函数的参数是一个保存字符串的列表，列表中某个字符串出现次数占列表元素总数的半数以上，找出并返回这个字符串。

   答案：

   ```Python
   from collections import Counter
   def check(str_list):
       count = Counter([item for item in str_list])
       m = max(count.values())
       return sorted([x for (x, y) in count.items() if y == m])[0]
   print(check(['a', 'af', 'a', 'a', 'b', 'c']))
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
   (1) select username from tb_user where userid=(select userid from tb_record where houseid=1055);
   (2) select username from tb_user u left join() tb_record r group by u.userid having count(select recid from tb_record) > 3 and u.usertel not null;
   ```

10. 请阐述访问一个用Django或Flask开发的Web应用，从用户在浏览器中输入网址回车到浏览器收到Web页面的整个过程中，到底发生了哪些事情，越详细越好。

  答案：

  ```
  用户输入网址回车后，解析域名，并发送http请求给后端服务器，后端服务器接收请求后，对请求做出响应，后端渲染相应的数据和页面后发送给前端，然后展示给用户。
  ```

11. 请阐述HTTPS的工作原理以及TCP是如何保证端到端可靠传输的。

    答案：

    ```
    https是添加了ssl协议的加密的传输协议，相较于http协议有着更好的安全性，客户端发送请求给服务端，服务端进行加密和返回公钥，客户端进行加密和向服务端发送该密钥的密文。服务端通过私钥来解密该密文，拿到对称加密的密钥，通过该密钥来进行加密通信。
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