# 关于项目

## 1.项目简介

闲钱宝是大学生通过做任务挣钱的云平台，它属于以运营为中心的服务软件，也可以理解为面向大学生的专业“众包”系统。系统非常简单：有一个云服务中心，其业务在不断完善中；每个学生都装有“挣闲钱”客户端；一些机构，称为“奶牛”，他们提供任务给平台。基本业务是，奶牛发布任务要求与薪酬，系统推送到客户端，学生完成任务可获得系统内部的“闲钱币”，“闲钱币”可用于发布任务或提现。系统不支持零元交易。

- 奶牛发布任务，并给予一定的悬赏别人来完成自己发布的任务，
- 学生端登陆系统，选择自己感兴趣并且能做到的任务完成，完成后通过审核获得奶牛提供的赏金，赏金积累到一定的金额后能够提现。
- （待补充）

## 2.重要分析设计文档

- 产品需求设计文档

- 数据库设计文档

- 产品原型图设计和UI图输出

- api设计文档

- 产品测试文档和项目demo

  ​

## 3.敏捷开发迭代管理与大事纪

#### 初始准备阶段

- 时间：第9, 10 周

- 目标：

  - 明确项目需求，完成初步需求分析设计
  - 前后端完成技术选型，实现初步开发架构
  - UI设计师提交部分UI设计（在产品经理原型图基础上）
  - 实现用户注册，登陆，注销等逻辑功能

- 具体任务与提交制品：

  |        任务         |          人员          |    时间    |                     提交物                     |
  | :-----------------: | :--------------------: | :--------: | :--------------------------------------------: |
  | 需求分析 原型图输出 |         唐育涛         | 第9周周末  |              需求分析文档，原型图              |
  |  前端界面初步设计   |         王鹏钦         | 第10周周二 |                   UI设计原稿                   |
  |  前端架构初步设计   |         王德超         |   第10周   |         前端软件架构文档，代码规范说明         |
  |  后端架构初步设计   |         蔡湘国         |   第10周   | 后端软件架构文档，代码规范说明，数据库设计文档 |
  |  前端代码部分编码   | 王德超，王广浩，王鹏钦 |   第10周   |                      代码                      |
  |  后端代码部分编码   | 蔡湘国，唐育涛，陈笑儒 |   第10周   |     代码，部分API接口说明（建议eolinker）      |


#### 第0轮迭代项目需求

- 需求范围/优先级

|               功能模块               | 优先级 |
| :----------------------------------: | :----: |
|     用户注册，用户登录，用户注销     |   P0   |
| 支持更多用户信息（如用户昵称，头像） |   P1   |

- 需求设计

用户登录逻辑：

![户逻辑闭](https://github.com/sysu-change/Dashboard/blob/master/image/%E7%94%A8%E6%88%B7%E9%80%BB%E8%BE%91%E9%97%AD%E7%8E%AF.jpg?raw=true)

 根据上图：我们可以把0轮迭代中PC端任务简单拆解为：首页，登录页，注册页，注册之后返回用户操作页面

我们在0轮迭代中实现首页，登录页，注册页，同时实现用户登录，注册，注销等相关逻辑.

PC端交互逻辑

|   模块   | 原型图 |                             描述                             |
| :------: | :----: | :----------------------------------------------------------: |
| 首页初版 |        | 1. 主⻚⾯配图进⾏产品介绍 2. 提供登陆、注册按钮，点击跳转相应页面 |
|  登录页  |        | 1. 登陆页面仅提供「手机号+密码」一种登陆方式。2. 「手机号+密码」登录时，提供「账户」、「密码」、「图形验证码」三个输⼊框。三个框均对应正确时即登陆成功，否则登陆失败。     3. 在完成P0迭代之后视需求决定是否加入手机号+验证码的登录方式   4. 最终存储到后台数据库的木马必须加密处理 |
|  注册页  |        | 1.提供「学号」「姓名」「年龄」「性别」「年级」「专业」「手机号」、「密码」、「再次输入密码」、「图形验证码」10个输⼊框。  2.每个输⼊框均有⼀定的输⼊限制条件，「学号」为8位数字学号，且为必填，非法输入需要重新输入。「姓名」允许英汉两种形式，必填。「年级」为选择选项，大一，大二，大三，大四，研一，研二，研三，必填。「专业」必填。「手机号」11位数字，格式不正确提供提示并重新输入，后端需要进行手机号匹配，「密码」、「再次输入密码」两次密码必须相同，不同不予通过，「图形验证码」必须正确匹配。 |

前端异常提示

|  模块  |         操作信息         |                          交互与提示                          |
| :----: | :----------------------: | :----------------------------------------------------------: |
| 注册页 |     手机号格式不正确     | 输入框自动判断，如果无效，输入框变红，给出提示。提交的icon按钮变灰，点击无反应 |
|        | 第二次密码与此一次不一致 | 输入框自动判断，如果无效，输入框变红，给出提示。提交的icon按钮变灰，点击无反应 |
|        |     图形验证码不正确     | 输入框自动判断，如果无效，输入框变红，给出提示。提交的icon按钮变灰，点击无反应 |
| 登录页 |      账号密码不匹配      | 点击登陆时判断，弹窗提示「对不起，用户名或密码有误！」，清空密码栏输入，保留账号栏输⼊。 |
|        |     图形验证码不正确     | 输入框自动判断，如果无效，输入框变红，给出提示。提交的icon按钮变灰，点击无反应 |



#### 第1轮迭代项目需求

- 时间：第11, 12, 13 周
- 目标：
  - 在第0轮迭代兼准备会议的过程中，我们实现了基础的用户登录，注册，注销等相关逻辑。此次一轮迭代，我们聚焦于用户管理系统和任务管理系统以及交易管理系统，力求在0轮迭代的基础上实现用户发布任务，提交任务，查看任务，获得赏金，编辑用户资料，充值服务，提现服务7个目标。

- 需求范围/优先级

|                         功能模块                         | 优先级 |
| :------------------------------------------------------: | :----: |
|                 奶牛发放任务（问卷形式）                 |   P0   |
|         奶牛查看问卷数据结果，编辑问卷，删除问卷         |   P0   |
|                 学生端填写问卷，获得赏金                 |   P0   |
|                  用户查看，修改个人资料                  |   P0   |
|                       用户账户充值                       |   P0   |
|                       用户赏金提现                       |   P0   |
| 答卷详细数据分析（具体到每一个选项有有多少比例的人选择） |   P1   |
|     指定任务面对对象（如大三以上的学生才能填写问卷）     |   P2   |

（P0级代表紧急度最高，P1级在P0级基本完成之后考虑开始实现，P2级最后看情况实现）

##### 用例设计：

用户相关逻辑：

- 修改个人信息：用户可以点击`资料编辑`进行用户名、年龄、专业、等个人信息的完善和修改。
- 账户充值：用户点击充值，选择充值金额，扫码二维码付款，付款成功就可以获得等量闲钱币。
- 账户提现：用户点击提现，选择提现金额，输入支付宝绑定手机号码，可以将闲钱币提现到支付宝账户。
- 邮箱验证：用户使用邮箱绑定账号，注册时系统后台往用户邮箱发送四位验证码，用户填写验证码以通过验证。


任务相关逻辑：

- 发布任务：用户点击`发布任务`进行任务发布，第一轮迭代支持的任务类型为问卷调查类型，用户需要创建和编辑问卷，设置回收问卷份数，设置单份悬赏金额后可以发放问卷，问卷发布的同时平台扣除相应的赏金币，若余额不足，问卷发布不成功。问卷一经发布，不允许再编辑，但可删除，将返回剩余的赏金币，已经被答题者获得的赏金币不做返还。
- 接受任务：用户点击`兼职任务`进入兼职任务页面，可以接受任务，第一轮迭代只提供问卷调查服务，故学生端只能填写问卷，每次填写问卷将获得一定的回报。每一份问卷有一定的点击进入任务详情，点击接单按钮可以开始执行任务，完成任务后会获得一定闲钱币。

问卷相关逻辑：

除了上文提到的发布问卷和填写问卷，还应该包括以下逻辑：

- 预览问卷：奶牛端能对编辑后保存的问卷或者发布中的问卷进行预览，以校正自己编辑的部分错误。

- 查看问卷数据：奶牛端用户点击`查看数据`进入问卷数据页面，页面显示该问卷的所有有效作答情况，具体包括{答卷编号，答题者，答题时间，作答答案}，点击作答答案跳转到具体问卷答案页面，供用户进行数据分析。

- 编辑问卷：可对已创建但未发布的问卷进行修改，可增加，删减问题，设置是否必答，修改回收份数，修改单份悬赏金额等功能，已经处于发布中的问卷没有这项功能。

- 删除问卷：删除问卷的前提是所有的作答都被审核过，也就是不存在债务关系的前提下可以删除问卷，如若问卷还有一定的赏金币，则返还给奶牛用户。

- 问卷审核：奶牛端用户点击`查看数据`进入问卷数据页面，页面显示该问卷的所有有效作答情况，具体包括{答卷编号，答题者，答题时间，作答答案}，点击作答答案跳转到具体问卷答案页面，用户查看答卷，选择是否通过审核，通过审核将发放一定的赏金币给作答者。

- 查看答卷：奶牛端用户点击`查看数据`进入问卷数据页面，点击每一份答卷的答案部分能够进入详细的答卷页面，答卷页面显示学生端的答卷信息。



#### 第2轮迭代项目需求

- 时间：第14，15，16 周
- 目标：在第0轮迭代兼准备会议的过程中，我们实现了基础的用户登录，注册，注销等相关逻辑。此后的第1轮迭代，我们聚焦于用户管理系统和任务管理系统以及交易管理系统，在0轮迭代的基础上实现问卷业务和充值提现业务以及编辑用户资料功能，第二轮迭代，我们主要目标有三个：
  - 增加其他任务功能，包括取快递业务，运动相关业务，学习相关业务，求夸夸业务等其他业务功能
  - 增加信誉系统，用于对用户信誉的评估和检测。
  - 增加投诉系统，用户对不满意的交易单能够进行投诉，由超级管理员审核投诉单是否成立，成立的情况下将对用户的信誉值做出扣分，用户信誉值低于一定层次将无法接受任务

需求范围/优先级

|                           功能模块                           | 优先级 |
| :----------------------------------------------------------: | :----: |
|            用户信誉系统，初始化用户信誉都为100分             |   P0   |
|   奶牛端发布其他任务，查看进行中的任务，删除未被接受的任务   |   P0   |
|      学生端接受任务，查看接受的任务，完成任务，放弃任务      |   P0   |
|            奶牛端审核学生端任务完成情况，发放赏金            |   P0   |
|            奶牛端和学生端对不满意的交易单进行投诉            |   P0   |
|       超级管理员审核投诉单，投诉单成立扣除用户信誉积分       |   P0   |
| 邮箱告知用户任务状态信息（有人接单，接单，放弃接单，审核交易单，投诉单） |   P0   |
|           多种类的惩罚力度，如扣除信誉积分先低后高           |   P1   |

（P0级代表紧急度最高，P1级在P0级基本完成之后考虑开始实现，P2级最后看情况实现）

##### 用例设计

此前我们已经有完整的用户系统，交易系统，账户系统了，这次的任务侧重于完善任务系统（其他类型任务），新增投诉系统，用户信誉系统。

奶牛端相关逻辑：

- 总体用例说明：奶牛点击`其他任务`进入其他类型任务页面，点击`问卷任务`切换到问卷任务页面，之所以将两者独立，是因为问卷具有更复杂的逻辑，更长的时效性，而普通任务一般只发放单次，短期限的一种模式。用户进入其他类型任务页面，能够实现发布任务，查看任务详情信息，跟进任务状态（发布中，接单中，已完成），审核已经完成的接单，删除未被接单的任务，投诉已经审核的任务。

学生端相关逻辑

- 总体用例说明：学生点击`其他任务`将展示所有的非问卷类型任务，点击`问卷任务`切换到问卷类型任务。用户进入其他类型任务页面，能够实现接受任务，查看任务详情信息等，点击`我的任务`能够查看正在进行中的任务，能够选择完成任务，查看任务详情，放弃任务；查看已完成的任务，能够查看赏金是否到账，能够对交易单进行投诉。

超级管理员相关逻辑

- 超级管理员账号登陆进入超级管理员系统，超级管理员系统目前只设计一个页面， 即投诉单审核页面，管理员能够查看投诉单具体信息，审核投诉成功，投诉失败。

具体用例说明：

奶牛端：

- 发布任务：奶牛端点击创建任务，能够实现创建普通任务，选择任务类型（取快递业务，运动业务，学习业务，求夸业务，其他业务），填写任务简介，任务详情，选择任务截止时间，填写联系方式（手机号，微信号，都必填），设置发布份数和单任务赏金，即可发布任务
- 删除任务：奶牛端创建任务之后，可以点击删除任务，对于未被接单的任务，则能直接删除，给出提示信息（任务删除成功），对于已经被接单的任务，给出提示信息（任务已经被接单，不能单向删除任务）
- 查看任务详情：用户争对具体的任务，点击查看任务详情能够查看该任务的详细情况信息
- 查看正在进行的任务：用户点击其他任务，将显示用户创建的正在进行中的任务，显示任务编号，任务信息，任务接单人数，任务需求人数，任务赏金。点击`查看任务详情`能看到详细的任务信息。
- 查看已完成的任务：用户查看已完成的任务，将能显示所有自己发布的并且学生端标记已经完成的任务。（注意只有已完成的任务才能进行审核，所以这个完成指的是学生端标记任务完成，而不是奶牛端整个任务结束，奶牛端在学生标记任务完成之后还要进行审核）
- 联系接单者：获得接单者的个人信息资料，非全部用户资料（昵称，学号，手机号，邮箱）
- 审核任务：学生端完成任务之后，任务状态标记为已完成，奶牛通过查看已完成的任务，可以对任务进行审核，审核允许通过和不通过，任务审核状态有三种（未审核，审核通过，审核不通过），审核成功与否都将通过邮箱告知任务接受者
- 投诉交易单：奶牛对已经完成的任务能够进行投诉，填写投诉的任务编号（前端自动写进），投诉人（前端自动写进），被投诉人，投诉内容，上传先关证据图片，之后即可点击投诉。用户发起投诉时，系统将通过邮箱的方式告知被投诉者。

学生端：

- 挑选任务：学生能够查看到目前系统所有的其他类型任务（任务编号，业务类型，业务简介，业务需求量，业务赏金），
- 查看任务详情：用户争对具体的任务，点击查看任务详情能够查看该任务的详细情况信息（任务编号，业务类型，业务简介，业务详情，业务截止时间，业务联系人手机号，业务联系人微信）
- 申请任务：用户可以对任务进行任务申请，对于需求量只有一份的任务，当任务被申请时，其他用户将不能获得该任务信息，用户需求量为多份时，对应需求量减1，其他用户可以获得该任务信息。任务被申请时，将通过邮箱的方式告知任务发起者，同时也发送一份邮箱信息给任务接受者提醒记得完成任务
- 放弃任务：用户可以放弃完成不了的任务， 放弃任务不需要审核，同时也不获得赏金，放弃任务之后，任务的需求量应该回退一步，可以重新出现在用户的挑选任务列表里面，放弃任务将通过邮箱的方式告知任务发起者
- 完成任务：用户点击完成任务，更新任务状态，标记成已完成的任务，之后奶牛端对其进行审核，决定是否发放赏金。完成任务将通过邮箱的方式告知任务发起者，提醒其记得进行任务审核
- 查看正在进行的任务：用户点击`正在进行`按钮，查看自己正在进行的任务，可以再该页面选择查看任务信息，放弃任务，完成任务
- 查看已完成的任务：用户点击`已完成`按钮，查看已完成的任务，查看赏金是否到账，决定是否投诉。
- 投诉交易单：用户对已经完成的任务能够进行投诉，填写投诉的任务编号（前端自动写进），投诉人（前端自动写进），被投诉人，投诉内容，上传先关证据图片，之后即可点击投诉。用户发起投诉时，系统将通过邮箱的方式告知被投诉者。

超级管理员：

- 投诉单审核：对用户填写的投诉单进行审核，审核可以通过与不通过，审核通过将对被投诉人进行扣除信誉积分的惩罚，并且邮箱告知被投诉人。审核不通过要邮箱告知投诉者。