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

### GET `/user/questionnaire_pre`从当前偏移量开始，获取接下去n个数据库问卷，用户已经填写的不传，未发布的问卷不传

#### Parameters

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

- 200, OK (服务器接受并存储了该问卷答案：)
- 400, Bad Request (问卷已达上限、服务器出错、问卷已被下架等)
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

- 200, OK (服务器接受并存储了该问卷答案：)
- 400, Bad Request (问卷已达上限、服务器出错、问卷已被下架等)
- 示例：

```json
   {
    "code":200,
    "msg":"successful"
}
```



### GET `/user/answer_get` 获取所有答卷

#### Parameters
```json
    {
    "qid":1234 //问卷id
    } 
```
#### Responses

- 200, OK (服务器接受并存储了该问卷答案)
- 400, Bad Request (问卷已达上限、服务器出错、问卷已被下架等)
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
### GET `/user/get_sid_answer` 查看一份具体的答卷

#### Parameters
```json
    {
    "qid":1234, //问卷id
    "sid":"16340007" //学号
    } 
```
#### Responses

- 200, OK (服务器接受并存储了该问卷答案)

- 400, Bad Request (问卷已达上限、服务器出错、问卷已被下架等)

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
