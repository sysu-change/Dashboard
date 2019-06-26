# 接口API设计

[TOC]

## 用户信息接口

### POST `/login` 登录账户

#### Parameters

- body (*required*) 顾客信息
  - example value
    ```json
    {
	    "phone_num": "13981153616",
	    "password": "123456"
    }    
    ```
  - parameter content type: `application/json`

#### Responses

- 200, OK
- 400, Bad Request


### POST `/register` 账户注册

#### Parameters

- body (*required*) 顾客信息
  - example value
    ```json
    {
      "sid": "15331111",
      "name": "阿柴",
      "age": 22,
      "sex": "0",
      "grade": "3",
      "major": "工程",
      "phone_num": "13991153616",
      "email":"1933611219@qq.com",
      "password": "123456"
    }    
    ```
  - parameter content type: `application/json`

#### Responses

- 200, OK
- 400, Bad Request
  

### DELETE `/logout` 注销登录

#### Parameters

- no parameters

#### Responses

- 200, OK
- 401, Unauthorized


### GET `/user/userinfo` 获取用户资料

#### Parameters

- no parameters

#### Responses

-  返回参数body (*required*) 顾客信息
  
  - example value
    ```json
    {
        "sid":"16340210",
        "age":18,
        "major":"计算机",
        "grade":"大三",
        "sex":"男",
        "phone_num":"15213554491",
	"email":"1933611219@qq.com",
	"Credibility":100,
        "balance":100
    }  
    ```
    
  - parameter content type: `application/json`  
  
  - Http状态码：
  
    - 200, OK
  
    - 400, null

### PUT `/user/userInfo` 修改用户信息

#### Parameters

- body (*required*) 顾客信息
  - example value
    ```json
    {
      "name": "阿柴",
      "age": 22,
      "sex": 1,
      "grade": 2,
      "major": "工程",
      "email":"1933611219@qq.com"
    }    
    ```
  - parameter content type: `application/json`

#### Responses

- 200, OK

- 400, Bad Request

- 示例：
   ```json
    {
    "code":200,
    "msg":"successful"
    } 
   ```
   

### POST `/recharge` 充值

#### Parameters

- body (*required*) 顾客信息
  - example value
    ```json
    {
	    "phone_num": "13981153616",
	    "money": 100
    }    
    ```
  - parameter content type: `application/json`

#### Responses

- 200, OK （服务端一切正常，需要用户输入支付宝银行卡密码和验证码用于后端进行验证）

- 400, Bad Request (输入的用户电话有误、未注册或则金额不在有效范围)

- 示例：
   ```json
    {
    "code":200,
    "msg":"successful"
    } 
   ```

### POST `/withdraw` 账户提现

#### Parameters

- body (*required*) 顾客信息
  - example value
    ```json
    {
	    "pay_phone": "13981153616",
	    "password":"123456",
      "money": 100
    }    
    ```
  - parameter content type: `application/json`

#### Responses

- 200, OK （服务端一切正常，需要用户输入支付宝银行卡密码和验证码用于后端进行验证）

- 400, Bad Request (输入的用户电话有误、未注册或则金额不在有效范围)

- 示例：
   ```json
    {
    "code":200,
    "msg":"successful"
    } 
   ```

### POST `/user/sent_verify` 发送邮箱验证码

#### Parameters

- body (*required*) 顾客信息

  - example value

    ```json
    {
      "email":"1933611219@qq.com"
    }    
    ```

  - parameter content type: `application/json`

#### Responses

- 200, OK 

- 400, failed

- 示例：

  ```json
  {
      "code":200,
      "msg":"successful",
      "verify_code":"RVjH"
  }
  ```



## 问卷接口
### POST `/user/create_questionnaire` 创建问卷

#### Parameters

- body (*required*) 问卷信息
  - example value
    ```json
    {
	    "type":1, //1表示问卷
	    "title": "中山大学睡眠情况调查",
      "description":"这是一份对中大学生进行的问卷调查",  
      "edit_status": 1,
      "reward": 1,
      "quantity": 100,
      "pub_time":"2019-05-12", 
      "content":[
            {
                "choice_type":1,
                "question":"您每晚几点睡",
                "choice_item":[
                    "8点",
                    "9点",
                    "10点"
                ],
                "must_edit":1
            },
            {
                "choice_type":1,
                "question":"您睡前看书吗",
                "choice_item":[
                    "看",
                    "不看"
                ],
                "must_edit":1
            },
            {
                "choice_type":1,
                "question":"您睡前习惯先喝一杯水吗",
                "choice_item":[
                    "习惯",
                    "不习惯"
                ],
                "must_edit":1
            }
        ]//choice_type:1表示单选，2表示多选，0便是答题者手动输入文本,must_edit:1代表必填，0可选
    }    
    ```
  - parameter content type: `application/json`

#### Responses

- 200, OK 

- 400, Bad Request 

- 示例：
   ```json
    {
    "code":200,
    "msg":"successful"
    } 
   ```

### PUT `/user/edit_questionnaire` 编辑问卷

#### Parameters

- body (*required*) 顾客信息
  - example value
    ```json
    {
	    "qid":1, //问卷编号
	    "title": "中山大学睡眠情况调查",
      "description":"这是一份对中大学生进行的问卷调查",  
      "edit_status": 1,
      "reward": 1,
      "quantity": 100,
      "pub_time":"2019-05-12", 
      "content":[
            {
                "choice_type":1,
                "question":"您每晚几点睡",
                "choice_item":[
                    "8点",
                    "9点",
                    "10点"
                ],
                "must_edit":1
            },
            {
                "choice_type":1,
                "question":"您睡前看书吗",
                "choice_item":[
                    "看",
                    "不看"
                ],
                "must_edit":1
            },
            {
                "choice_type":1,
                "question":"您睡前习惯先喝一杯水吗",
                "choice_item":[
                    "习惯",
                    "不习惯"
                ],
                "must_edit":1
            }
        ]//choice_type:1表示单选，2表示多选，0便是答题者手动输入文本,must_edit:1代表必填，0可选
    }    
    ```
  - parameter content type: `application/json`

#### Responses

- 200, OK 

- 400, Bad Request

- 示例：
   ```json
    {
    "code":200,
    "msg":"successful"
    } 
   ```

### DELETE `/user/delete_questionnaire` 删除问卷

#### Parameters

- body (*required*) 
  ```json
    {
    "qid":1 //删除对应问卷编号的问卷
    } 
  ```
#### Responses

- 200, OK 

- 400, Bad Request (**还存在答卷未审核，不能删除**)

- 示例：
   ```json
    {
    "code":200,
    "msg":"successful"
    } 
   ```

### GET `/user/questionnaire_own` 获取用户创建的所有问卷

#### Parameters

- no parameters

#### Responses
```json
{
    "code":200,
    "msg":"successful",
    "number":3,
    "content":[
        {
            "qid":1234,
            "title":"中大学生睡眠情况调查",
            "description":"问卷调查",
            "reward":2,
            "quantity":300,
            "edit_status":1
        },
        {
            "qid":1235,
            "title":"中大学生睡眠情况调查",
            "description":"问卷调查",
            "reward":2,
            "quantity":300,
            "edit_status":1
        },
        {
            "qid":1236,
            "title":"中大学生睡眠情况调查",
            "description":"问卷调查",
            "reward":2,
            "quantity":300,
            "edit_status":1
        }
    ]
}
```

### GET `/user/questionnaire/{qid}` 请求具体一份问卷

#### Parameters
```json
    {
    "qid":1
    } 
```

#### Responses

```json
{
	"code":200, // 操作状态码
    "msg":"successful", //返回信息
    "content":{
        "qid":3,
        "sid":"16340209",
        "title":"中大学生调查问卷1",
        "description":"中大学生调查问卷1",
        "edit_status":1,
        "quantity":200,
        "reward":0.5,
        "pub_time":"2019-05-12",
        "content":[
            {
                "choice_type":1,
                "question":"您每晚几点睡",
                "choice_item":[
                    "8点",
                    "9点",
                    "10点"
                ],
                "must_edit":1
            },
            {
                "choice_type":1,
                "question":"您睡前看书吗",
                "choice_item":[
                    "看",
                    "不看"
                ],
                "must_edit":1
            },
            {
                "choice_type":1,
                "question":"您睡前习惯先喝一杯水吗",
                "choice_item":[
                    "习惯",
                    "不习惯"
                ],
                "must_edit":1
            }
        ]
	} 
}
```

### GET `/user/questionnaire_pre/?offset={value}&number={value}`

### 从当前偏移量开始，获取接下去n个数据库问卷，用户已经填写的不传，未发布的问卷不传

#### GET Parameters

```json
    {
    "offset":1, //偏移量
    "number":5 //请求数量
    } 
```
#### Responses
```json
    {
    "code":200, // 操作状态码
    "msg":"successful", //返回信息
    "number":5,  //实际返回数目
    "content":[
        {
            "qid":1234,
            "title":"中大问卷调查",
            "description":"问卷",
            "status":1,
            "quantity":300,
            "reward":2.2
        },
        {
            "qid":1235,
            "title":"中大问卷调查",
            "description":"问卷",
            "status":1,
            "quantity":300,
            "reward":2.2
        },
        {
            "qid":1236,
            "title":"中大问卷调查",
            "description":"问卷",
            "status":1,
            "quantity":300,
            "reward":2.2
        },
        {
            "qid":1237,
            "title":"中大问卷调查",
            "description":"问卷",
            "status":1,
            "quantity":300,
            "reward":2.2
        },
        {
            "qid":1238,
            "title":"中大问卷调查",
            "description":"问卷",
            "status":1,
            "quantity":300,
            "reward":2.2
        }
    ]
}
```



## 答卷接口

### POST `/user/answer_put_forward` 答卷提交

#### Parameters
```json
    {
    "ID":1, //问卷id
    "sid":"16340007", //答卷人学号
    "ans_time":"2019-05-12", //时间
    "content":[["hahs","shcas"],["suuw"],["hcshihoiw"]]
    } 
```
#### Responses

- 200, OK
- 400, Bad Request 
- 示例：

```json
   {
    "code":200,
    "msg":"successful"
   }
```

### PUT `/user/answer_review` 答卷审核

#### Parameters
```json
    {
    "qid":1234, //问卷id
    "sid":"16340007", //答卷人学号
    "verify":1, //未审核0，审核通过1，审核不通过2
    } 
```
#### Responses

- 200, OK
- 400, Bad Request 
- 示例：

```json
{
    "code":200,
    "msg":"successful"
}
```



### GET `/user/answer_get/{qid}` 获取所有答卷

#### GET Parameters
```json
    {
    "qid":1234 //问卷id
    } 
```
#### Responses

- 200, OK 
- 400, Bad Request
- 示例：

```json
   {
    "code":200,
    "msg":"successful",
    "content":[
        {
            "sid":"16340209",
            "ans_time":"2015-05-11",
            "verify":0
        },
        {
            "sid":"16340210",
            "ans_time":"2015-05-11",
            "verify":0
        },
        {
            "sid":"16340211",
            "ans_time":"2015-05-11",
            "verify":0
        },
        {
            "sid":"16340212",
            "ans_time":"2015-05-11",
            "verify":0
        },
        {
            "sid":"16340213",
            "ans_time":"2015-05-11",
            "verify":0
        }
    ]
}
```
### GET `/user/get_sid_answer?qid={value}&sid={value}` 

### 查看一份具体的答卷

#### GET Parameters
```json
    {
    "qid":1234, //问卷id
    "sid":"16340007" //学号
    } 
```
#### Responses

- 200, OK

- 400, Bad Request 

- 示例：
```json
{
    "code":200,
    "msg":"successful",
    "content":
        {
            "sid":"16340209",
            "ans_time":"2015-05-11",
            "verify":0,
            "content":[["hahs","shcas"],["suuw"],["hcshihoiw"]]
        }
}
```



## 其他任务接口

### 奶牛端部分接口

### POST `/user/create_task` 奶牛端创建发布任务

**(后端做的时候添加status, int类型，0：初始值刚发布未完成 1：已完成)**

#### Parameters

```json
   {
    "type":2,
    "description":"这是一份求帮拿快递任务",
    "detail":"6月4号下午有没有人帮忙拿下快递",
    "deadline":"2019-06-09",
    "phone_num":"13719927319",
    "wechat":"cxg723",
    "quantity":1,
    "reward":0.5
}
```

#### Responses

- 200, OK 
- 400, Bad Request 
- 示例：

```json
{
    "code":200,
    "msg":"successful"
}
```

### DELETE `/user/delete_task` 奶牛端删除任务

#### Parameters

```json
{
    "tid":2
}
```

#### Responses

- 200, OK 
- 400, Bad Request 
- 示例：

```json
{
    "code":200,
    "msg":"successful"
}
```

### GET `/user/provider_task_done` 奶牛端查看已完成的任务

**（全部已审核通过的任务)**

#### Parameters

- no parameters

#### Responses

- 200, OK 
- 400, Bad Request
- 示例：

```json
{
    "code":200,
    "msg":"successful",
    "number":3,
    "content":[
        {
            "tid":1,
            "type":2,
            "reward":1.5,
            "sid":"16340007",
            "accept_status":1,
            "verify":0
        },
        {
            "tid":2,
            "type":2,
            "reward":1.5,
            "sid":"16340209",
            "accept_status":1,
            "verify":1
        },
        {
            "tid":3,
            "type":2,
            "reward":1.5,
            "sid":"16340209",
            "accept_status":1,
            "verify":2
        }
    ]
}
```

### GET `/user/provider_task_in_progress` **奶牛端查看正在进行中的任务**

**（**任务未全部审核通过即正在进行**)**

#### Parameters

- no parameters

#### Responses

- 200, OK 
- 400, Bad Request
- 示例：

```json
{
    "code":200,
    "msg":"successful",
    "number":3,
    "content":[
        {
            "tid":1,
            "type":2,
            "deadline":"2019-06-12",
            "reward":1.5,
            "quantity":1,
            "accept_num":1
        },
        {
            "tid":1,
            "type":3,
            "deadline":"2019-06-12",
            "reward":1.5,
            "quantity":15,
            "accept_num":3
        },
        {
            "tid":1,
            "type":2,
            "deadline":"2019-06-12",
            "quantity":1,
            "accept_num":1
        }
    ]
}
```

### GET `/user/contact_receiver/{sid}` 奶牛端联系接单者（获取接单者部分用户信息）

#### Parameters

```json
sid: 16340007
```

#### Responses

- 200, OK
- 400, Bad Request 
- 示例：

```json
{
    "code": 200,
    "msg":"successful",
    "content":{
        "name": "蔡湘国",
        "sid": "16340007",
        "phone_num": "13719927319",
        "email": "1933611219@qq.com"
    }
}
```

### PUT `/user/task_verify` 奶牛端审核任务(审核成功与否都将通过邮箱告知任务接受者)

#### Parameters

```json
{
	"tid":20,
	"sid":"16340007",
	"verify":1
}
```

verify参数  0：未审核 1：审核通过 2：审核不通过

#### Responses

- 200, OK 
- 400, Bad Request
- 示例：

```json
{
    "code":200,
    "msg":"successful"
}
```

### 学生端部分接口

### POST `/user/apply` 学生端申请任务（需求量从数据库调用减1，发送邮件给发起者和接收者，申请接单接单状态accept_status=0）

#### Parameters

```json
{
	"tid":20
}
```

verify参数  0：未审核 1：审核通过 2：审核不通过

#### Responses

- 200, OK 
- 400, Bad Request
- 示例：

```json
{
    "code":200,
    "msg":"successful"
}
```

### POST `/user/task_finish` 学生端完成任务（更新接单状态accept_status=1，邮件通知任务发起者，提醒审核）

#### Parameters

```json
{
	"tid":20
}
```

verify参数  0：未审核 1：审核通过 2：审核不通过

#### Responses

- 200, OK 
- 400, Bad Request
- 示例：

```json
{
    "code":200,
    "msg":"successful"
}
```

### GET `/user/select_task?offset={value}&number={value}`

### 学生端挑选任务，查看到目前系统所有的其他类型任务（要做分页）

#### GET Parameters

```json
    {
    "offset":1, //偏移量
    "number":3 //请求数量
    } 
```

#### Responses

```json
   {
    "code":200,
    "msg":"successful",
    "number":3,
    "content":[
        {
            "tid":1,
            "type":2,
            "description":"帮拿快递受到至二楼下",
            "quantity":1,
            "reward":2.2
        },
        {
            "tid":2,
            "type":2,
            "description":"帮拿快递受到至三楼下",
            "quantity":1,
            "reward":2.2
        },
        {
            "tid":3,
            "type":2,
            "description":"帮拿快递受到至四楼下",
            "quantity":1,
            "reward":2.2
        }
    ]
}
```

### POST `/user/task_give_up` 学生端放弃任务（需求量回退一步,邮件告知任务发起者 ）

#### Parameters

```json
{
	"tid":20
}
```

verify参数  0：未审核 1：审核通过 2：审核不通过

#### Responses

- 200, OK 
- 400, Bad Request
- 示例：

```json
{
    "code":200,
    "msg":"successful"
}
```

### GET `/user/student_task_done` 学生端查看已完成的任务（

（注意是学生端标记任务完成，而不是奶牛端整个任务结束，奶牛端在学生标记任务完成之后还要进行审核）

#### Parameters

- no parameters

#### Responses

- 200, OK 
- 400, Bad Request
- 示例：

```json
{
    "code":200,
    "msg":"successful",
    "number":3,
    "content":[
        {
            "tid":1,
            "type":2,
            "sid":"16340007",
            "deadline":"2019-06-12",
            "reward":1.5,
            "reward_status":"是"
        },
        {
            "tid":1,
            "type":2,
            "sid":"16340209",
            "deadline":"2019-06-12",
            "reward":1.5,
            "reward_status":"是"
        },
        {
            "tid":1,
            "type":2,
            "sid":"16340023",
            "deadline":"2019-06-12",
            "reward":1.5,
            "reward_status":"是"
        }
    ]
}
```

### GET `/user/student_task_in_progress` **学生端查看正在进行中的任务**

**（**任务未全部审核通过即正在进行**)**

#### Parameters

- no parameters

#### Responses

- 200, OK 
- 400, Bad Request
- 示例：

```json
{
    "code":200,
    "msg":"successful",
    "number":3,
    "content":[
        {
            "tid":1,
            "type":2,
            "sid":"16340007",
            "deadline":"2019-06-12",
            "reward":1.5
        },
        {
            "tid":2,
            "type":2,
            "sid":"16340017",
            "deadline":"2019-06-12",
            "reward":1.5
        },
        {
            "tid":3,
            "type":2,
            "sid":"16340207",
            "deadline":"2019-06-12",
            "reward":1.5
        }
    ]
}
```

### GET `/user/task/{id}` **奶牛端和学生端查看具体任务详情**

#### Parameters

- id: 1

#### Responses

- 200, OK 
- 400, Bad Request
- 示例：

```json
{
    "code":200,
    "msg":"successful",
    "content":{
        "tid":1,
        "type":2,
    	"description":"代取一份快递放到至二楼下宿管处",
    	"detail":"本人由于不在学校需要找人帮忙拿下快递，放到楼下宿管阿姨处，快递编号和手机号码请联系本人，必须六点前取件，不能做到的不要接单",
    	"deadline":"2019-06-12",
        "phone_num":"13719927319",
        "wechat":"cxg723"
    }
}
```

### 投诉相关接口

### POST `/user/complaint` 奶牛端和学生端投诉，发送邮件告知被投诉者

#### Parameters

```json
{
	"tid":3,
    "sid1":"16340207",
    "sid2":"16340209",
    "reason":"任务完成不符合要求"
}
```

#### Responses

- 200, OK 
- 400, Bad Request
- 示例：

```json
{
    "code":200,
    "msg":"successful"
}
```

### POST `/picture/upload` 投诉图片上传（图片一张一张上传）

#### Parameters

```json
{
	"tid":24,
	"sid1":"16340209",
	"sid2":"16340007",
	"photo":"data:image/png;base64,图片base64的转化编码"
}
```

#### Responses

- 200, OK 
- 400, Bad Request
- 示例：

```json
{
    "code":200,
    "msg":"successful"
}
```

### GET `/user/get_complaint/{cid}` **获取具体的投诉单**

#### Parameters

- cid: 1

#### Responses

- 200, OK 
- 400, Bad Request
- 示例：

```json
{
    "code": 200,
    "msg": "successful",
    "tid": 24,
    "sid1": "16340209",
    "sid2": "16340007",
    "reason": "用户态度非常不好！",
    "number": 4,
    "photo": [
        {
            "photo0": "data:image/png;base64,图片0的base64编码串"
        },
        {
            "photo1": "data:image/png;base64,图片1的base64编码串"
        },
        {
            "photo2": "data:image/png;base64,图片2的base64编码串"
        },
        {
            "photo3": "data:image/png;base64,图片3的base64编码串"
        }
    ]
}
```

### PUT `/user/complaint_handle` **审核某个投诉单**

#### Parameters

```json
{
    "cid":1,
    "verify":1
}
```

verify 参数 0:未审核 1：审核通过 2：审核不通过

#### Responses

- 200, OK 
- 400, Bad Request
- 示例：

```json
{
    "code":200,
    "msg":"successful"
}
```

### GET `/user/get_complaint/all` **获取所有未审核的投诉单信息（不包含图片）**

#### Parameters

- no parameters

#### Responses

- 200, OK 
- 400, Bad Request
- 示例：

```json
{
    "code": 200,
    "msg": "successful",
    "number": 3,
    "content": [
        {
            "cid": 1,
            "tid": 24,
            "sid1": "16340209",
            "sid2": "16340399"
        },
        {
            "cid": 2,
            "tid": 19,
            "sid1": "16340209",
            "sid2": "16340399"
        },
        {
            "cid": 3,
            "tid": 24,
            "sid1": "16340209",
            "sid2": "16340287"
        }
    ]

```
