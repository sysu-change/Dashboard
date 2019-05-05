## 技术选型

### 编程语言：[Python](https://docs.python.org/)

选择Python 3.7版本，Python 3.7最重要的添加和改进之处包括如下：
- 用类处理数据时减少样板代码的数据类。
- 一处可能无法向后兼容的变更涉及处理生成器中的异常。
- 面向解释器的“开发模式”。
- 具有纳秒分辨率的时间对象。
- 环境中默认使用UTF-8编码的UTF-8模式。
- 触发调试器的一个新的内置函数。

### 基本框架：[Flask](http://docs.jinkan.org/docs/flask/)
- Flask框架是Python开发的一个基于Werkzeug和Jinja 2的web开发微框架，它的优势就是极其简洁，但又非常灵活，而且容易学习和应用。因此Flask框架是Python新手快速开始web开发最好的选择，此外，使用Flask框架的另一个好处在于你可以非常轻松地将基于Python的机器学习算法或数据分析算法集成到web应用中。
- 可以用Flask框架实现很多应用。有很多库可以直接使用，例如flask-sockets，flask-google-maps等，而且Flask框架支持MySQL、Postgresql、MongoDB等诸多数据库。用Flask框架实现的web应用类型有：博客应用、聊天应用、仪表盘应用、RESTAPI、管理页面、邮件服务等。

### 持久数据库：[MySQL]()

Flask框架下，在flask2.0中不再支持MySQLdb，因此选用pymysql。用python3 引入pymysql库，实现对mysql数据库的操作，支持数据库的读写分离配置。 可参考如下链接：[FLask框架下Python3连接mysql](https://github.com/houxiaozhao/python3-flask-mysql)



## 持续集成

### CI平台：[Github](https://github.com/)

Github是一个代码托管平台和开发者社区，开发者可以在Github上创建自己的开源项目并与其他开发者协作编码。创业公司可以用它来托管软件项目，开源项目可以免费托管，私有项目需付费。GitHub可以托管各种git库，并提供一个web界面，但与其它像 [SourceForge](http://baike.baidu.com/view/1091461.htm)或[Google Code](http://baike.baidu.com/view/2252816.htm)这样的服务不同，GitHub的独特卖点在于从另外一个项目进行分支的简易性。为一个项目贡献代码非常简单：首先点击项目站点的“fork”的按钮，然后将代码检出并将修改加入到刚才分出的代码库中，最后通过内建的“pull request”机制向项目负责人申请代码合并。GitHub对于团队间合作开发来说尤为方便。

### 代码提交改动分析：[Github](https://github.com/)

代码提交，添加，修改变动，以及团队成员贡献分析一目了然。



## 架构设计

项目目录示例：(完善中)

```sh
.
├── app # 项目App源码目录
│   ├── app.py # App入口
│   ├── match # 配置文件解析源码
│   │   └── __init__.py
│   │   └── match.py # 处理密码加密以及手机号等格式匹配问题
│   ├── dbTools # 数据库操作
│   │   └── __init__.py
│   │   └── dbConfig.py		#数据库配置文件
│   │   ├── dbInit.py		#数据库初始化
│   │   └── dbOperators.py # 数据库操作函数
│   │   └── dbPool.py
│   │   └── tools.py
│   │   └── __pycache__ #缓存
├── setup.md 
├── README.md 
```
