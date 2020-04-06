# 实验二：图书管理系统用例建模
|    学号    |       班级       |      姓名     |       照片   |
|:---------:|:----------------:|:-------------:|:---------:|
| 201710414316  |   17软工3班     |   唐美琪   |   无  |

## 1.图书管理系统的类图
### 1.1用例图PlantUML源码如下：
####
```
@startuml
class 馆藏目录 {
}
馆藏目录 "1.."--"1..*" 馆藏资源品种

class  馆藏资源品种{
  资源名称
  国际出版号
  价格
  简介
  馆藏数量
  可借数量
}

馆藏资源品种 <|-- 碟片品种
馆藏资源品种 <|-- 图书品种
class 碟片品种{
碟片类型
碟片数
制作公司
}
class 图书品种{
作者
出版社
出版日期
}

class 馆藏资源品种 {
}
馆藏资源品种 "1"-- "*" 预定记录:被预定

class 预定记录
{
预定日期
}

预定记录 "*"-- "1" 读者
class 读者{
姓名
身份证号
借书卡号
图书限额
已借图书数
碟片限额
已借图片数
}

读者 -- 借书记录
class 借书记录{
借书日期
归还日期
}

借书记录 "0..1"-- "1" 资源项
借书记录 "1"-- "0..1" 逾期记录
class 逾期记录{
逾期天数
}

逾期记录"*"--"0..1"罚款明细 : 使用

馆藏资源品种*-- 资源项 : 拥有
class 资源项{
馆藏流水号
状态
}

借书记录 "*"-- "1" 图书管理员:登记
class 图书管理员{
职工号
姓名
}
@enduml
```

### 1.2类图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test3/1.png)

### 1.3类图说明：
#### 
```
1.馆藏目录连接馆藏资源品种，且一个馆藏目录对应多个馆藏资源品种
2.馆藏资源品种可扩展为碟片品种和图书品种
3.馆藏资源品种可以被预定，且一个馆藏资源品种可以对应任意个预定记录
4.馆藏资源品种与资源项是组合的关系，资源项拥有馆藏资源品种
5.一个读者可以有一个或者多个预定记录
6.不论一本书有无借书记录，在图书馆中，其一定会有其对应的资源项
7.某本书的借书记录可能会有逾期记录，也可能没有
8.某本书逾期后，可能会产生罚款，也可能不会
9.一个图书管理员可以登记多个借书记录
```
## 2.图书管理系统对象图
### 2.1 类馆藏目录的对象图
#### 源码如下
````
@startuml
object 馆藏目录
@enduml
````
#### 对象图如下
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test3/2.png)

### 2.2 类馆藏资源品种的对象图
#### 源码如下
````
object 馆藏资源品种
    object 碟片品种
    object 图书品种
    
    馆藏资源品种 <|-- 碟片品种
    馆藏资源品种 <|-- 图书品种
    馆藏资源品种*-- 资源项 : 拥有
    
    object 馆藏资源品种{
    资源名称
    国际出版号
    价格
    简介
    馆藏数量
    可借数量
    }
    object 资源项{
    馆藏流水号
    状态
    }
    object 图书品种{
    作者
    出版社
    出版日期
    }
    object 碟片品种{
    碟片类型
    碟片数
    制作公司
    }
````
#### 对象图如下
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test3/3.png)

### 2.3 类预定记录的对象图
#### 源码如下
````
@startuml
object 预定记录

object 预定记录{
预定日期
}
@enduml
````
#### 对象图如下
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test3/4.png)

### 2.4 类读者的对象图
#### 源码如下
````
@startuml
object 读者

object 读者{
姓名
身份证号
借书卡号
图书限额
已借图书数
碟片限额
已借碟片数
}

@enduml
````
#### 对象图如下
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test3/5.png)

### 2.5 类借书记录的对象图
#### 源码如下
````
@startuml
object 借书记录{
借书日期
归还日期
}
@enduml
````
#### 对象图如下
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test3/6.png)

### 2.6 类资源项的对象图
#### 源码如下
````
@startuml
object 资源项

馆藏资源品种*-- 资源项 : 拥有

object 资源项{
馆藏流水号
状态
}
object 馆藏资源品种{
资源名称
国际出版号
价格
简介
馆藏数量
可借数量
}

@enduml
````
#### 对象图如下
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test3/7.png)

### 2.7 类逾期记录的对象图
#### 源码如下
````
@startuml
object 逾期记录{
逾期天数
}
@enduml
````
#### 对象图如下
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test3/8.png)

### 2.8 类罚款明细的对象图
#### 源码如下
````
object 罚款明细
````
#### 对象图如下
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test3/9.png)

### 2.9 类图书管理员的对象图
#### 源码如下
````
@startuml
object 图书管理员{
职工号
姓名
}
@enduml
````
#### 对象图如下
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test3/10.png)

### 2.10 类图书品种的对象图
#### 源码如下
````
@startuml
object 馆藏资源品种
object 碟片品种

馆藏资源品种 <|-- 碟片品种

object 馆藏资源品种{
资源名称
国际出版号
价格
简介
馆藏数量
可借数量
}
object 碟片品种{
碟片类型
碟片数
制作公司
}
@enduml
````
#### 对象图如下
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test3/11.png)

### 2.11 类碟片品种的对象图
#### 源码如下
````
@startuml
object 馆藏资源品种
object 图书品种

馆藏资源品种 <|-- 图书品种

object 馆藏资源品种{
资源名称
国际出版号
价格
简介
馆藏数量
可借数量
}
object 图书品种{
作者
出版社
出版日期
}
@enduml
````
#### 对象图如下
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test3/12.png)


