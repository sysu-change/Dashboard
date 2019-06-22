# REST API 设计规范

### 概况

REST -- REpresentational State Transfer，英语的直译就是“表现层状态转移”，直白的解释是：用URL定位资源，用HTTP动词（GET,POST,PUT,DELETE)描述操作

resource：资源，即数据
Representational：某种表现形式，比如用JSON，XML，JPEG等
State Transfer：状态变化。通过HTTP动词实现

RESTful API就是REST风格的API，是一套协议来规范多种形式的前端和同一个后台的交互方式。由后台也就是SERVER来提供前端来调用。前端调用API向后台发起HTTP请求，后台响应请求将处理结果反馈给前端。也就是说RESTful 是典型的基于HTTP的协议

### 1.资源

资源就是网络上的一个实体，一段文本，一张图片或者一首歌曲。资源总是要通过一种载体来反应它的内容。文本可以用TXT，也可以用HTML或者XML、图片可以用JPG格式或者PNG格式，JSON是现在最常用的资源表现形式。在本项目中，资源统一使用JSON

### 2.统一接口

RESTful风格的数据元操CRUD（create,read,update,delete）分别对应HTTP方法：GET用来获取资源，POST用来新建资源（也可以用于更新资源），PUT用来更新资源，DELETE用来删除资源，这样就统一了数据操作的接口

### 3.URI

可以用一个URI（统一资源定位符）指向资源，即每个URI都对应一个特定的资源。要获取这个资源访问它的URI就可以，因此URI就成了每一个资源的地址或识别符。一般的，每个资源至少有一个URI与之对应，最典型的URI就是URL

本项目中，URI使用URL

### 4. 协议

API与用户的通信协议，总是使用HTTPs协议。

### 5. 域名

应该尽量将API部署在专用域名之下。

`https://api.example.com`

如果确定API很简单，不会有进一步扩展，可以考虑放在主域名下。

`https://example.org/api/

### 6. 路径

路径又称"终点"（endpoint），表示API的具体网址。

在RESTful架构中，每个网址代表一种资源（resource），**所以网址中不能有动词，只能有名词**，而且所用的名词往往与数据库的表格名对应。

一般来说，数据库中的表都是同种记录的"集合"（collection），**所以API中的名词也应该使用复数。**

举例来说，有一个API提供动物园（zoo）的信息，还包括各种动物和雇员的信息，则它的路径应该设计成下面这样。

`https://api.example.com/v1/zoos`

`https://api.example.com/v1/animals`

`https://api.example.com/v1/employees`

不要使用：

`/getZoos`
`/createNewAnimals`
`/deleteAllEmployees`

### 6. HTTP动词

对于资源的具体操作类型，由HTTP动词表示

常用的HTTP动词有下面五个（括号里是对应的SQL命令）：

`GET（SELECT）`：从服务器取出资源（一项或多项）

`POST（CREATE）`：在服务器新建一个资源

`PUT（UPDATE）`：在服务器更新资源（客户端提供改变后的完整资源）

`PATCH（UPDATE）`：在服务器更新资源（客户端提供改变的属性）

`DELETE（DELETE）`：从服务器删除资源



还有两个不常用的HTTP动词：

`HEAD`：获取资源的元数据

`OPTIONS`：获取信息，关于资源的哪些属性是客户端可以改变的



下面是一些例子：

`GET /zoos`：列出所有动物园

`POST /zoos`：新建一个动物园

`PUT /zoos/ID`：更新某个指定动物园的信息（提供该动物园的全部信息）

`PATCH /zoos/ID`：更新某个指定动物园的信息（提供该动物园的部分信息）

`DELETE /zoos/ID`：删除某个动物园

**使用PUT, POST 和DELETE 方法 而不是 GET 方法来改变状态，不要使用GET 进行状态改变.**

`GET /users/711?activate`

`GET /users/711/activate`

### 7.过滤、排序、选择、分页

**过滤**

API应该提供参数，过滤返回结果

如：

http://api.example.com/zoos/ID/animals?limit=10: 指定返回的动物园的动物记录的数量

参数的设计允许存在冗余，即允许API路径和URL参数偶尔有重复

比如，`GET /zoo/ID/animals` 与 `GET /animals?zoo_id=ID` 的含义是相同的



**排序**

API允许针对多个字段排序

`GET /cars?sort=-manufactorer,+model`

这是返回根据生产者降序和模型升序排列的car集合

`GET /tickets?sort=-priority,created_at`

复杂的排序规则应该通过组合实现，排序规则有多个rule以逗号间隔组合而成



**选择**：

有时候API使用者不需要所有的结果，在进行横向限制的时候（例如值返回API结果的前十项）还应该可以进行纵向限制。并且这个功能能有效的提高网络带宽使用率和速度

可以使用fields查询参数来限制返回的域例如：

`GET /cars?fields=manufacturer,model,id,color`



**分页**：

将分页信息放到link header里面：

http://tools.ietf.org/html/rfc5988#page-6

来自github的文档：

Link: 

<https://api.github.com/user/repos?page=3&per_page=100>; rel="next"

<https://api.github.com/user/repos?page=50&per_page=100>; rel="last"

### 8. 状态码

服务器向用户返回的状态码和提示信息，常见的有以下一些（方括号中是该状态码对应的HTTP动词）：

`200 – OK` – 一切正常

`201 – OK` – 新的资源已经成功创建

`204 – OK` – 资源已经成功擅长

`304 – Not Modified` – 客户端使用缓存数据

`400 – Bad Request` – 请求无效，需要附加细节解释如 "JSON无效"

`401 – Unauthorized` – 请求需要用户验证

`403 – Forbidden` – 服务器已经理解了请求，但是拒绝服务或这种请求的访问是不允许的

`404 – Not found` – 没有发现该资源

`422 – Unprocessable Entity` – 只有服务器不能处理实体时使用，比如图像不能被格式化，或者重要字段丢失

`500 – Internal Server Error` – API开发者应该避免这种错误

**更新和创建操作应该返回对应的状态码，防止用户多次的API调用。**

### 9. 错误处理

如果状态码是4xx，就应该向用户返回出错信息。一般来说，返回的信息中将error作为键名，出错信息作为键值即可。
使用详细的错误包装错误：

```json
{
  "errors": [
   {
    "userMessage": "Sorry, the requested resource does not exist",
    "internalMessage": "No car found in the database",
    "code": 34,
    "more info": "http://dev.mwaysolutions.com/blog/api/v1/errors/12345"
   }
  ]
}
```

### 10.返回结果

针对不同操作，服务器向用户返回的结果应该符合以下规范。

`GET /collection`：返回资源对象的列表（数组）

`GET /collection/resource`：返回单个资源对象

`POST /collection`：返回新生成的资源对象

`PUT /collection/resource`：返回完整的资源对象

`PATCH /collection/resource`：返回完整的资源对象

`DELETE /collection/resource`：返回一个空文档

### 11. 使用Http头声明序列化格式

在客户端和服务端，双方都要知道通讯的格式，格式在HTTP-Header中指定

`Content-Type` 定义请求格式

`Accept` 定义系列可接受的响应格式

### 12. 基于验证的缓存

**不要在服务端存储应用状态**

RESTful HTTP的交互必须是无状态的，这表明每一次请求要包含处理该请求所需的一切信息，每一次请求都应该包含鉴权证明

客户端负责维护应用状态，RESTful服务端不需要在请求间保留应用状态，服务端负责维护资源状态而不是应用状态

通过使用ssl我们可以不用每次都提供用户名和密码：我们可以给用户返回一个随机产生的token

这样可以极大的方便使用浏览器访问API的用户

这种方法适用于用户可以首先通过一次用户名-密码的验证并得到token，并且可以拷贝返回的token到以后的请求中

如果不方便，可以使用OAuth 2来进行token的安全传输

### 13.其他

（1）使用JSON进行数据传递

（2）使用蛇形命令（下划线和小写）

（3）URL不能使用大写字母

