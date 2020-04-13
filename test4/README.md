# 实验四：图书管理系统顺序图绘制
|    学号    |       班级       |      姓名     |       照片   |
|:---------:|:----------------:|:-------------:|:---------:|
| 201710414316  |   17软工3班     |   唐美琪   |   无  |

## 1.图书管理系统的顺序图
### 1.1借书用例PlantUML源码如下：
####
```
@startuml
actor 图书管理员
participant "登录成功" as A
participant "图书存在" as B
participant "显示图书库存" as C
participant "显示新的图书库存" as D
participant "借书失败" as E
participant "借书成功" as F

图书管理员 -> A: 登录
activate A
A -> B: 输入图书编号
activate B
B -> C: 是
activate C
B -->E:否
activate E
deactivate B
deactivate E
C -> D:更新库存
activate D
deactivate C
D -> F: 借阅成功
activate F
deactivate A
deactivate D
deactivate F
@enduml

```

### 1.2借书用例顺序图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test4/4.1.png)

### 1.3借书用例顺序图说明：
#### 
```
1.图书管理员登录成功
2.输入图书编号
3.若图书不存在，则显示输入有误
4.若图书存在，则显示库存量
5.若库存量充足，则借出该图书；若库存量不充足，则借书失败

```

### 1.2借书用例顺序图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test4/4.1.png)

### 1.3借书用例顺序图说明：
#### 
```
1.
2.
3.
4.
5.

```
### 2.1归还图书用例顺序图PlantUML源码如下：
####
```
@startuml
actor 读者
participant "借阅记录" as A
participant "是否逾期" as B
participant "缴纳罚款" as C
participant "图书信息" as D
participant "用户信息" as E

读者 -> A: 归还图书
 activate A
A -> B: 查看借阅记录
 activate B
B -> C: 是
 activate C
B ->D:否,更新库存
 activate D
 deactivate B
C -> D:更新库存
 activate D
 deactivate C
D -> E: 更新
 activate E
 deactivate D
 E ->A : 返回信息
 deactivate E
 deactivate A
@enduml

```

### 2.2归还图书用例顺序图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test4/4.2.png)

### 2.3归还图书用例顺序图说明：
#### 
```
1.读者登录成功
2.查询借阅记录，选择需要归还的书目
3.若该本借阅图书已逾期，则计算罚款金额，交付罚款后，还书成功
4.若该本图书未逾期，则直接还书成功
```
### 3.1借书用例PlantUML源码如下：
####
```
@startuml
actor 图书管理员
participant "登录成功" as A
participant "图书库存信息" as B
participant "需要维护的图书" as C
participant "书目信息" as D
participant "更新书目信息" as E
participant "显示无该书目" as F

图书管理员 -> A: 登录
activate A
A -> B: 查看
activate B
B -> C: 选择
activate C
deactivate B
C ->D:查看
activate D
D ->E:存在
activate E
deactivate D
D -> F:不存在
activate D
deactivate E
deactivate C
activate F
deactivate A
deactivate D
deactivate F
@enduml

```

### 3.2借书用例顺序图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test4/4.3.png)

### 3.3借书用例顺序图说明：
#### 
```
1.图书管理员登录成功
2.查询所有图书书目
3.选择需要维护的图书种类
4.若存在，显示其书目信息
5.若不存在，则显示该图书不存在

```
### 4.1维护读者信息用例顺序图PlantUML源码如下：
####
```
@startuml
actor 图书管理员
participant "登录成功" as A
participant "读者信息" as B
participant "填写读者信息" as C
participant "更新信息" as D

图书管理员 -> A: 登录
activate A
A -> B: 列出
activate B
B -> C: 选择读者
activate C
deactivate B
C -> D:
activate D
D -> A:返回信息
deactivate C
deactivate A
deactivate D

@enduml

```

### 4.2维护读者信息用例顺序图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test4/4.4.png)

### 4.3维护读者信息用例顺序图说明：
#### 
```
1.图书管理员登录
2.显示所有读者信息
3.选择需要更新信息的读者
4.填写新的读者信息
5.更新读者信息

```
### 5.1查询书目用例PlantUML源码如下：
####
```
@startuml
actor 读者
participant "登录成功" as A
participant "图书存在" as B
participant "图书信息" as C
participant "查看该书" as D
participant "不存在该书" as E

读者 -> A: 登录
activate A
A -> B: 输入图书信息
activate B
B -> C: 是
activate C
B -->E:否
activate E
deactivate B
destroy E
C -> D:
activate D
deactivate E
deactivate C
deactivate A
deactivate D
@enduml

```

### 5.2查询书目用例顺序图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test4/4.5.png)

### 5.3查询书目用例顺序图说明：
#### 
```
1.读者登录成功
2.读者输入需要查询的书目
3.若该图书存在，显示图书信息
4.若该图书不存在，则提示不存在该图书
```
### 6.1查询借阅情况用例PlantUML源码如下：
####
```
@startuml
actor 读者
participant "登录成功" as A
participant "借阅情况" as B
participant "借阅信息" as C
participant "无借阅信息" as D

读者 -> A: 登录
activate A
A -> B: 查询
activate B
B -> C: 是,显示
activate C
B -->D:否
activate D
deactivate B
deactivate C
deactivate A
deactivate D
@enduml

```

### 6.2查询借阅情况用例顺序图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test4/4.6.png)

### 6.3查询借阅情况用例顺序图说明：
#### 
```
1.读者登录成功
2.查询该读者的借阅信息
3.若该读者有借阅信息，则显示其借阅信息
4.若没有借阅信息，则显示没有借阅信息
```
### 7.1预定图书用例PlantUML源码如下：
####
```
@startuml
actor 读者
participant "登录成功" as A
participant "图书信息" as B
participant "预定图书" as C
participant "预定单" as D
participant "预定失败" as E
participant "预定信息" as F
participant "预定成功" as G

读者 -> A: 登录
activate A
A -> B: 显示
activate B
B -> C: 选择
activate C
C ->D:填写
activate D
deactivate B
D -> E:无库存
activate E
deactivate E
deactivate C
D -> F: 有库存，确定
activate F
deactivate D
F -> G:
activate G
deactivate F
deactivate G
deactivate A
@enduml

```

### 7.2预定图书用例顺序图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test4/4.7.png)

### 7.3预定图书用例顺序图说明：
#### 
```
1.读者登录成功
2.选择预定图书
3.查询图书被预定的信息
4.若被预定完，则显示预定失败
5.若还有库存，则显示预定成功
```
### 8.1取消预定图书用例PlantUML源码如下：
####
```
@startuml
skinparam sequenceArrowThickness 2
skinparam roundcorner 20
skinparam maxmessagesize 60
skinparam sequenceParticipant underline

actor 读者
participant "登录成功" as A
participant "预定单" as B
participant "取消成功" as C
participant "预定单更新" as D

读者 -> A: 登录
activate A
A -> B: 查看
activate B
B -> C: 取消
activate C
C ->D:填写
activate D
D ->A:
deactivate B
deactivate C
deactivate D
deactivate A
@enduml

```

### 8.2取消预定图书用例顺序图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test4/4.8.png)

### 8.3取消预定图书用例顺序图说明：
#### 
```
1.读者登录成功
2.查看预定图书信息
3.选择需要取消预定的图书
4.更新图书预订单
5.返回新的信息

```
### 9.1借书用例PlantUML源码如下：
####
```
@startuml
actor 用户
participant "登录成功" as A
participant "修改密码页面" as B
participant "旧密码" as C
participant "修改失败" as D
participant "修改成功" as E

用户 -> A: 登录
activate A
A -> B:选择
activate B
B -> C: 输入
activate C
C ->D:输入错误
activate D
D ->E:输入正确
activate E
E ->A:
deactivate B
deactivate C
deactivate D
deactivate A
deactivate E
@enduml

```

### 9.2修改密码用例顺序图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test4/4.9.png)

### 9.3修改密码用例顺序图说明：
#### 
```
1. 用户登录吃饭
2. 用户选择跳转到修改密码的页面 
3. 用户填写旧密码及新密码 
4. 旧密码输入错误，提示错误
5. 旧密码输入正确，系统保存新密码，返回新的密码信息，用例结束

```


