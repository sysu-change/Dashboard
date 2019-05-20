# 数据库设计

## ER模型

![Database1](Database1.png)

## 关系模型

## 数据库物理模型

- account-存储账号

    | Field     | Type        | Key  | Description                                                  |
    | --------- | ----------- | ---- | ------------------------------------------------------------ |
    | sid       | VARCHAR(8)  | PRI  | 学号，作为主键                                               |
    | name      | VARCHAR(16) |      | 姓名，不能为NULL                                             |
    | age       | INT         |      | 年龄                                                         |
    | sex       | VARCHAR(2)  |      | 性别，只能是’男‘或’女‘                                       |
    | grade     | VARCHAR(4)  |      | 年级，只能是‘大一’，‘大二’，‘大三’，‘大四’，‘研一’，‘研二’，‘研三’，不能为NULL |
    | major     | VARCHAR(40) |      | 专业，不能为NULL                                             |
    | phone_num | VARCHAR(11) |      | 电话号码，在表中必须是唯一的，不能为NULL                     |
    | password  | VARCHAR(20) |      | 密码，不少于6位，不能为NULL                                  |
    | balance   | INT         |      | 账户余额，不能为NULL，默认值为0                              |
    

- questionnaire-存储问卷表的元数据

    | Field       | Type         | Key                                | Description                                            |
    | ----------- | ------------ | ---------------------------------- | ------------------------------------------------------ |
    | qid         | INT          | PRI                                | 问卷id号，作为主键                                     |
    | sid         | VARCHAR(8)   | FOREIGN KEY REFERENCES account.sid | 发布问卷的账户sid，不能为NULL                          |
    | titile      | VARCHAR(100) |                                    | 问卷标题，不能为NULL                                   |
    | description | VARCHAR(200) |                                    | 问卷描述，默认为空                                     |
    | edit_status | INT          |                                    | 编辑状态，0:未编辑完全，1：正在审核或发布中，2：已发布 |
    | pub_time    | DATETIME     |                                    | 发布时间，默认值为NULL，当为NULL的时候表示还没有发布   |
    | quantity    | INT          |                                    | 回收的问卷总数，不能为NULL                             |
    | reward      | FLOAT        |                                    | 回答问卷的赏金，不能为NULL                             |

- que_item-存储问卷表中的问题

    | Field       | Type         | Key                                             | Description                                                 |
    | ----------- | ------------ | ----------------------------------------------- | ----------------------------------------------------------- |
    | qid         | INT          | PRI && FOREIGN KEY REFERENCES questionnaire.qid | 问卷id号，作为主键对之一                                    |
    | i_num       | INT          | PRI                                             | 问题序号，作为主键对之一                                    |
    | i_type      | INT          |                                                 | 问题类型，暂定0表示单选，1表示多选，2表示文本题，不能为NULL |
    | description | VARCHAR(100) |                                                 | 问题的描述，不能为NULL                                      |

- que_option-存储问卷表问题中的选项

    | Field       | Type         | Key                                                          | Description                               |
    | ----------- | ------------ | ------------------------------------------------------------ | ----------------------------------------- |
    | qid         | INT          | PRI && 和i_num一起 FOREIGN KEY REFERENCES que_item.qid, que_item.i_num | 问卷id号，作为主键对之一                  |
    | i_num       | INT          | PRI && 和did一起 FOREIGN KEY REFERENCES que_item.qid, que_item.i_num | 问题序号，作为主键对之一                  |
    | o_num       | INT          | PRI                                                          | 选项序号，作为主键对之一（文字题时作为1） |
    | description | VARCHAR(100) |                                                              | 问题的描述，默认为空                      |

- que_answer-存储问卷表的回答元数据

    | Field  | Type       | Key                                             | Description                                       |
    | ------ | ---------- | ----------------------------------------------- | ------------------------------------------------- |
    | qid    | INT        | PRI && FOREIGN KEY REFERENCES questionnaire.qid | 问卷id号，作为主键对之一                          |
    | sid    | VARCHAR(8) | PRI && FOREIGN KEY REFERENCES account.sid       | 回答问卷的账户的sid，作为主键对之一               |
    | verify | INT        |                                                 | 审核状态，0表示未审核，1表示审核通过，2表示未通过 |

- que_answer_option-存储问卷表的回答的详细内容（选项）

    | Field       | Type         | Key                                                          | Description                                       |
    | ----------- | ------------ | ------------------------------------------------------------ | ------------------------------------------------- |
    | qid         | INT          | PRI && 和sid一起 FOREIGN KEY REFERENCES que_answer.qid, que_answer.sid | 问卷id号，作为主键对之一                          |
    | sid         | VARCHAR(8)   | PRI && 和qid一起 FOREIGN KEY REFERENCES que_answer.qid, que_answer.sid | 回答问卷的账户的sid，作为主键对之一               |
    | i_num       | INT          | PRI                                                          | 问题序号，作为主键对之一                          |
    | o_num       | INT          | PRI                                                          | 选择的选项序号，作为主键对之一（文字题时设为为1） |
    | word_answer | VARCHAR(100) |                                                              | 文字题的回答，默认为空                            |