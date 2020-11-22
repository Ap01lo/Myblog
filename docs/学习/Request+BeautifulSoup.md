#### Request库七个主要方法

| 方法        | 说明                                          |
| ----------- | --------------------------------------------- |
| .requests() | 构造一个请求，支撑以下个方法的基础方法        |
| .get()      | 获取HTML网页的主要方法，对应于HTTP的GET       |
| .head()     | 获取HTML网页信息头的方法，对应于HTTP的HEAD    |
| .post()     | 向HTML提交POST请求的方法，对应于HTTP的POST    |
| .put()      | 向HTML网页提交PUT请求的方法，对应于HTTP的PUT  |
| .patch()    | 向HTML网页提交局部修改请求，对应于HTTP的PATCH |
| .delete()   | 向HTTP网页提交删除请求，对应于HTTP的DELETE    |

+ get()

  ```python
  requests.get(url,params=None,**kwargd)
  ```

  `url` 拟获取页面的url链接

  `params` url中的额外参数，字典或字节流格式，可选

  `**kwargs` 12个控制访问的参数

  > 这七个方法都是调用requestd方法实现的，也就是说，可以认为只有一个requests方法，**他会返回一个 response 对象**

  那么 response 对象的常用属性有：

  | 属性                | 说明                                                 |
  | ------------------- | ---------------------------------------------------- |
  | r.status_code       | HTTP请求的返回状态，200表示连接成功，404表示连接失败 |
  | r.text              | HTTP相应内容的字符串形式，即，url对应的页面内容      |
  | r.encoding          | 从HTTP header中猜测的相应内容编码方式                |
  | r.apparent_encoding | 从内容中分析出的相应内容编码方式(备选编码方式)       |
  | r.content           | HTTP相应内容的二进制形式                             |



#### 爬取网页的通用代码框架

**理解Request库的异常**

| 异常                        | 说明                                        |
| --------------------------- | ------------------------------------------- |
| requests.ConnectionError    | 网络连接错误异常，入DNS查询失败、拒绝连接等 |
| requests.HTTPError          | HTTP错误异常                                |
| requests.URLRequired        | URL缺失异常                                 |
| requests.d=TooManyRedirects | 超过最大重定向次数，产生重定向异常          |
| requests.ConnerTimedout     | 连接远程服务器超时异常                      |
| requests.Timeout            | 请求URL超时，产生超时异常                   |

 ```python
def getHTMLText(url):
    try:
        r = requests.get(url,timeout = 30)
        r.raise_fot_status()
        r.encoding = r.apparent_encoding
        return r.text
    except:
        return "产生异常"
    
if __name__ == "__main__":
    url = "http://www.baidu.com"
    print(getHTMLText(url))
 ```



#### http协议

> http 超文本传输协议
>
> 是一个基于“请求与相应”模式的、无状态的应用层协议
>
> 采用url作为定位网络资源的标识

url格式： http://host[:post][path]

host:合法的internet主机域名或ip地址

port:端口号，缺省时为80

path:请求资源的路径

**http协议对资源的操作对应这requests的六个方法**



#### requests的方法的主要参数

+ params  字典或字节序列，作为参数增加到url中
+ data  字典、字节序列或文件对象。作为requests的内容
+ json   json格式的数据，作为requests的内容
+ headers  字典，http定制头

> 以上三个灵活掌握

+ cookies  字典或者cookie
+ files 字典类型，传输文件
+ auth  元组，支持http认证功能
+ timeout  设定超时时间
+ proxies  字典类型，设定访问代理服务器
+ allow_redirects  True/False 默认为True 重定向开关
+ stream  True/False  默认为True 获取内容立即下载开关
+ verify  True/False 默认为True 认证ssl证书开关
+ cert  本地ssl证书路径



> 爬虫来讲，掌握get就行。偶尔用head



#### BeautifulSoup库使用

```python
from bs4 import BeautifulSoup
demp = r.text
soup = BeautifulSoup(demo,"html.parser")
```

| 解析器           | 使用方法                        | 条件                 |
| ---------------- | ------------------------------- | -------------------- |
| bs4的html解析器  | BeautifulSoup(mk,‘html.parser’) | 安装bs4库            |
| lxml的html解析器 | BeautifulSoup(mk,‘lxml’)        | pip install lxml     |
| lxml的xml解析器  | BeautifulSoup(mk,‘xml’)         | pip install lxml     |
| html5lib的解析器 | BeautifulSoup(mk,‘html5lib’)    | pip install html5lib |

**BeautifulSoup类的基本元素**

| 基本元素        | 说明                                                     |
| --------------- | -------------------------------------------------------- |
| Tag             | 标签，最基本的信息组织单元。分别用<>与</>表明开头结尾    |
| Name            | 标签的名字，<p>...</p>的名字是 p ，格式：<tag>.name      |
| Attributes      | 标签的属性，字典形式组织，格式：<tag>.attrs              |
| NavigabelString | 标签内非属性字符串，<>...</>中字符串，格式：<tag>.string |
| Comment         | 标签内字符串的注释部分，一种特殊的Comment类型            |



**标签树的下行遍历**

| 属性         | 说明                                                   |
| ------------ | ------------------------------------------------------ |
| .contents    | 子节点的列表，将tag所有儿子节点存入列表                |
| .children    | 子节点的迭代类型，与contents类似，用于循环遍历儿子节点 |
| .descendants | 子孙节点的迭代类型，包含所有子孙节点，用于循环遍历     |

**标签树的上行遍历**

| 属性     | 说明                                 |
| -------- | ------------------------------------ |
| .parent  | 节点的父亲节点                       |
| .parents | 节点的先辈标签，用于循环遍历先辈节点 |

**标签树的平行遍历**

| 属性               | 说明                                                 |
| ------------------ | ---------------------------------------------------- |
| .next_sibling      | 返回按照html文本顺序的下一个平行节点标签             |
| .previous_sibling  | 返回按照html文本顺序的上一个平行节点标签             |
| .next_siblings     | 迭带类型，返回按照html文本顺序的后续所有平行节点标签 |
| .previous_siblingd | 迭带类型，返回按照html文本顺序的前续所有平行节点标签 |

> 所有的平行便利必须发生在同一个父节点之下



#### 基于bs4库的html输出

```python
soup.prettify()
```



#### 四种信息标记形式

+ html  （xml一种）
+ xml  internet上的信息交互
+ json  移动应用云端和节点的信息通信，无注释
+ yaml  各类系统的配置文件，有注释，易读

> way1.  完整解析信息的标记形式，在提取关键信息
>
> way2.  无视任何标记形式，直接搜索关键信息
>
> way3.  结合形式解析与搜索方法，提取关键信息

示例：

提取html中所有的url链接

1. 搜索到所有的<a>标签
2. 解析<a>标签格式。提取herf后的链接内容

```python
for link in soup.find_all('a'):
    print(link.get('href'))
```



#### 正则表达式

> 简洁表达一组字符串的表达式



**常用操作字符**

![image-20200705102715475](C:\Users\Dell\AppData\Roaming\Typora\typora-user-images\image-20200705102715475.png)

![image-20200705102923162](C:\Users\Dell\AppData\Roaming\Typora\typora-user-images\image-20200705102923162.png)

**IP地址的正则表达式**

![image-20200705103445594](C:\Users\Dell\AppData\Roaming\Typora\typora-user-images\image-20200705103445594.png)



#### RE库的主要功能函数

![image-20200705103956127](C:\Users\Dell\AppData\Roaming\Typora\typora-user-images\image-20200705103956127.png)

**等价用法**

![image-20200705105803777](C:\Users\Dell\AppData\Roaming\Typora\typora-user-images\image-20200705105803777.png)

**返回的match对象的属性**

| 属性    | 说明                                  |
| ------- | ------------------------------------- |
| .string | 待匹配的文本                          |
| .re     | 匹配时使用的pattern对象（正则表达式） |
| .pos    | 正则表达式搜索文本的开始位置          |
| .endpos | 正则表达式搜索文本的结束位置          |



> 贪婪匹配： Re库默认使用贪婪匹配，即输出匹配最长的子串
>
> 最小匹配： 输出最短的子串

**最小匹配操作符**<u>加问号</u>

![image-20200705110753362](C:\Users\Dell\AppData\Roaming\Typora\typora-user-images\image-20200705110753362.png)



#### scripy爬虫框架

5+2结构

![image-20201122160809377](C:\Users\Dell\AppData\Roaming\Typora\typora-user-images\image-20201122160809377.png)

五个主体：SPIDERS,ENGINE,SCHEDULER,DOWNLOADER,ITEM PIPELINES

两个中间键：SPIDERS<-->ENGING, ENGINE<--> DOWNLOADER

路径：

1. spiders发出request请求给engine，这个request是一个url,即目标网址
2. 请求通过engine后，转发给scheduler进行调动
3. engine从scheduler获取请求，这个请求是真实请求，即要爬取的东西
4. engine获取请求之后发给downloader进行爬取
5. downloader爬取结束后形成一个响应对象，封装爬取的结果发给engine
6. engine收到响应后返回给spider
7. spider处理响应后产生两个数据类型 items/requests ，发送给engine
8. engine收到后，将item发给item pipeline，将request发给scheduler进行调动

> 其中 1->2为一条路径
>
> 3->4->5->6为一条路径
>
> 7->8为一条路径

最后一条路径是为了解决，我们在爬取过程中对网页中的其他链接产生了兴趣，可以在scrapy中设置新的功能进行爬取，7 中产生的item为爬取项，request为该爬取项的爬取请求，可以让scheduler重新发起调用。



**在这个框架中，engine，downloader，还有scheduler是已经包装好的模块，用户只需要编写配置spider与item pipeline模块**

+ Spider负责发送url，同时解析爬取的内容
+ item pipeline 负责对提取的信息进行处理



downloader middleware中间键：

目的：实施engine,scheduler和downloader之间进行用户可配置的控制

功能：修改，丢弃，新增请求或响应

spider middleware中间键

目的：对请求和爬取项的再处理

功能：修改，丢弃，新增请求或爬取项