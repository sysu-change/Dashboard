# 接口API设计
<<<<<<< Updated upstream
API文档
## 顾客账号

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
      "sex": "男",
      "grade": "大四",
      "major": "工程",
      "phone_num": "13991153616",
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
  