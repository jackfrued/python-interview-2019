### Python开发工程师笔试题1参考答案

> **答题要求**：将该项目从[地址1](<https://github.com/jackfrued/python-interview-2019>)或[地址2](<https://gitee.com/jackfrued/python-interview-2019>)**fork**到自己的[GitHub](<https://github.com/>)或[Gitee](https://gitee.com)仓库并在线填写答案，完成后以发送合并请求（**Pull Request**）的方式提交自己的工作成果，时间120分钟。

#### 答题人：骆昊

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
   {1: item1, 3: item9}
   6
   ```

2. 下面的Python代码会输出什么。

   ```Python
   from functools import reduce
   
   items = [11, 12, 13, 14] 
   print(reduce(int.__mul__, map(lambda x: x // 2, filter(lambda x: x ** 2 > 150, items))))
   # print(reduce(int.__mul__, [item // 2 for item in items if item ** 2 > 150]))
   ```

   答案：

   ```
   42
   ```

3. 有一个通过网络获取数据的Python函数（可能会因为网络或其他原因出现异常），写一个装饰器让这个函数在出现异常时可以重新执行，但尝试重新执行的次数不得超过指定的最大次数。

   答案：

   ```Python
   from functools import wraps
   
   
   def retry(*, tries=1, errors=(Exception, )):
   
       def outer(func):
       
           @wraps(func)
           def inner(*args, **kwargs):
               for _ in range(tries):
                   try:
                       return func(*args, **kwargs)
                   except errors:
                       pass
   
           return inner
      
       return outer
   ```

4. 下面的字典中保存了某些公司今日的股票代码及价格，用一句Python代码从中找出价格最高的股票对应的股票代码，用一句Python代码创建股票价格大于100的股票组成的新字典。

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
   max(zip(prices.values(), prices.keys()))[1] 
   {key: value for key, value in prices.items() if value > 100} 
   ```

5. 写一个函数，传入的参数是一个列表，如果列表中的三个元素`a`、`b`、`c`相加之和为`0`，就将这个三个元素组成一个三元组，最后该函数返回一个包含了所有这样的三元组的列表。例如：

   > 参数：`[-1, 0, 1, 2, -1, -4]`
   >
   > 返回：`[(-1, 0, 1), (-1, 2, -1), (0, 1, -1)]`

   答案：

   ```Python
   from itertools import combinations
   
   
   def foo(nums): 
       result = [] 
       for a, b, c in combinations(nums, 3): 
           if a + b + c == 0: 
               result.append((a, b, c)) 
       return result 
   ```

6. 写一个函数，传入的参数是一个列表（列表中的元素可能也是一个列表），返回该列表最大的嵌套深度，例如：

   > 参数：`[1, 2, 3]`
   >
   > 返回：`1`
   >
   > 参数：`[[1], [2, [3]]]`
   >
   > 返回：`3`

   答案：

   ```Python
   def depth_of_list(items):
       if isinstance(items, list):
           max_depth = 1
           for item in items:
               curr_depth = depth_of_list(item)
               if curr_depth + 1 > max_depth:
                   max_depth = curr_depth + 1
           return max_depth
       return 0
   ```

7. 写一个函数，实现将输入的长链接转换成短链接，每个长链接对应的短链接必须是独一无二的且每个长链接只应该对应到一个短链接，假设短链接统一以`http://t.cn/`开头。例如：

   > 参数：`http://jackfrued.xyz/api/users/10001`
   >
   > 返回：`http://t.cn/E6MUth1`

   答案：

   ```Python
   seq_num = 10000000
   url_maps = {}
   
   
   def to_base62(num):
       chars = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz'
       result = []
       while num > 0:
           result.append(chars[num % 62])
           num //= 62
       return ''.join(reversed(result))
   
   
   def to_short(url):
       if url in url_maps:
           return url_maps[url]
       global seq_num
       seq_num += 1
       short_url = f'http://t.cn/{to_base62(seq_num)}'
       url_maps[url] = short_url
       return short_url
   ```

8. 用5个线程，将1~100的整数累加到一个初始值为0的变量上，每次累加时将线程ID和本次累加后的结果打印出来。

   答案：

   ```Python
   from threading import get_ident, Thread, Lock
   from concurrent.futures import ThreadPoolExecutor
   
   result, i = 0, 1
   locker = Lock()
   
   
   def calc():
       global result, i
       while True:
           with locker:
               if i > 100:
                   break
               result, i = result + i, i + 1
               print(get_ident(), result)
   
   
   with ThreadPoolExecutor(max_workers=5) as pool:
       pool.submit(calc)
   ```

9. 请阐述Python是如何进行内存管理的。

   答案：

   ```
   
   ```

10. 在MySQL数据库中有名为`tb_result`的表如下所示，请写出能查询出如下所示结果的SQL。

    `tb_result`表：

    | rq         | shengfu |
    | ---------- | ------- |
    | 2017-04-09 | 胜      |
    | 2017-04-09 | 胜      |
    | 2017-04-09 | 负      |
    | 2017-04-09 | 负      |
    | 2017-04-10 | 胜      |
    | 2017-04-10 | 负      |
    | 2017-04-10 | 负      |

    查询结果：

    | rq         | 胜   | 负   |
    | ---------- | ---- | ---- |
    | 2017-04-09 | 2    | 2    |
    | 2017-04-10 | 1    | 2    |

    答案：

    ```SQL
    
    ```

11. 列举出你知道的HTTP请求头选项并说明其作用。

    答案：

    ```
    
    ```

12. 阐述Web应用中的Cookie和Session到底有什么区别和联系。

    答案：

    ```
    
    ```

13. 请阐述访问一个用Django或Flask开发的Web应用，从用户在浏览器中输入网址回车到浏览器收到Web页面的整个过程中，到底发生了哪些事情，越详细越好。

    答案：

    ```
    
    ```

14. 请阐述HTTPS的工作原理，并说明该协议与HTTP之间的区别。

    答案：

    ```
    
    ```

15. 简述你认为新浪微博是如何让订阅者在第一时间获得博主发布的消息。

    答案：

    ```
    
    ```

16. 简述如何检查数据库是不是系统的性能瓶颈以及你在工作中是如何优化数据库操作性能的。

    答案：

    ```
    
    ```

17. 在Linux系统中，假设Nginx的访问日志位于`/var/log/nginx/access.log`，该文件的每一行代表一条访问记录，每一行都由若干列（以制表键分隔）构成，其中第1列记录了访问者的IP地址。请用一条命令找出最近的100000次访问中，访问频率最高的IP地址及访问次数。

    答案：

    ```Shell
    tail -10000 /var/log/nginx/access.log | awk '{print $1}' | sort | uniq -c | sort -nr | head -1
    ```

18. 请阐述跨站脚本攻击（XSS）、跨站身份伪造（CSRF）和SQL注射攻击的原理及防范措施。

    答案：

    ```
    
    ```