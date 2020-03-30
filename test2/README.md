# 实验一：业务流程建模
|    学号    |       班级       |      姓名     |       照片   |
|:-------:|:-------------:|:----------:|
| 201710414316  |   17软工3班     |   唐美琪   |   无  |

## 1.图书管理系统的用例关系
### 1.1用例图PlantUML源码如下：
####
```
@startuml
left to right direction
skinparam packageStyle rectangle
actor 图书管理员
actor 读者
actor 系统管理员
rectangle 图书管理系统-用例图 {
    图书管理员 --> (借出图书)
    图书管理员 --> (归还图书)
    图书管理员 --> (维护书目)
    图书管理员 --> (维护读者信息)
    图书管理员 --> (增加图书)
  (查询书目) <-- 读者
  (查询借阅情况) <-- 读者
  (预定图书) <-- 读者
  (归还图书) <-- 读者
  (维护书目) .> (查询书目):《include》
  (预定图书) .> (取消预定):《extend》
    系统管理员 --> (维护读者信息)
  (预定图书) .> (查询书目):《include》
  (修改密码) <-- 读者
  (修改密码) <-- 图书管理员
    系统管理员 --> (修改密码) 
    系统管理员 --|> 图书管理员
    图书管理员 --> (修改详细信息)
  (修改详细信息)<--读者
}
@enduml
```

### 1.2用例图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test2/1.png)

## 2.参与者说明：
### 2.1 图书管理员
#### 主要职责是：借出图书、归还图书、维护书目、维护读者信息、修改详细信息、增加图书
### 2.2读者
#### 主要职责是：查询书目、查询借阅情况、预定图书、取消预定、修改详细信息
### 2.3其他类型用户
#### 主要职责是：维护管理员信息、维护读者信息

## 3.用例规约表
### 3.1 "借出图书"用例
<table>
  <caption align="center">"借出图书"用例规约</caption>
  <tr>
    <td>用例名称</td>
    <td>借出图书</td>
  </tr>
  <tr>
    <td>参与者</td>
    <td>图书管理员</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>用户发出借书请求</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>更新图书与用户借书记录信息</td>
  </tr>
  <tr>
    <td colspan="2" align="center">主事件流</td>
  </tr>
  <tr>
    <td>参与者动作</td>
    <td>系统行为</td>
  </tr>
  <tr>
    <td>
		1. 查询图书<br>
		5. 借出图书<br>
		6. 更新用户借阅信息<br>
		7. 更新书库信息<br>
	</td>
    <td>
		2. 传递给管理员相应图书信息<br>
		3. 显示图书借阅情况<br>
		4. 确认图书库存<br>
		8. 将书库信息更新<br>		
   </td>
  </tr>
  <tr>
    <td colspan="2" align="center">备选事件流</td>
  </tr>
  <tr>
    <td colspan="2">当图书库存已为0<br>1.提示没有图书，结束用例</td>
  </tr>
  <tr>
    <td colspan="2" align="center">业务规则</td>
  </tr>
  <tr>
    <td colspan="2">更新借书后的信息等</td>
  </tr>
</table>

#### "借出图书"用例流程图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test2/2.png)
#### "借出图书"用例流程图源码如下：
```
@startuml
start
	:登录;
	:输入图书编号;
	if (图书存在？) then (no)
		:输入有误，该图书不存在;
		end
	else (yes)
		:显示库存量;
	if (库存量充足？) then (no)
		:借书失败，提供库存不足;
		end
	else (yes)
		:借阅成功;
	endif
	:借出图书结束;
stop
@enduml
```
### 3.2 "购入图书"用例
<table>
<caption align="center">"归还图书"用例规约</caption>
<tr>
  <td>用例名称</td>
  <td>归还图书</td>
</tr>
<tr>
  <td>参与者</td>
  <td>图书管理员</td>
</tr>
<tr>
  <td>前置条件</td>
  <td>用户发出还书请求</td>
</tr>
<tr>  
  <td>后置条件</td>
  <td>更新图书与用户信息</td>
</tr>
<tr>
  <td colspan="2" align="center">主事件流</td>
</tr>
<tr>
  <td>参与者动作</td>
  <td>系统行为</td>
</tr>
<tr>
  <td>
		1. 获取归还图书信息<br>
		2. 将图书归入入库<br>
		3. 更新用户借阅信息<br>
		4. 更新书库信息<br>
	</td>
  <td>
		1. 传递给管理员归还图书信息<br>
		2. 显示图书借阅情况<br>
		3. 更新图书库存<br>
		4. 对图书借阅时间进行核对<br>
	</td>
</tr>
<tr>
  <td colspan="2" align="center">备选事件流</td>
</tr>
<tr>
  <td colspan="2">当归还时间已逾期<br>1.提示超出归还时间，需要进行罚款</td>
</tr>
 <tr>
  <td colspan="2" align="center">业务规则</td>
</tr>
<tr>
  <td colspan="2">更新归还书籍的信息</td>
</tr>
</table>
#### "购入图书"用例流程图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test2/3.png)
#### "购入图书"用例流程图源码如下：
```
@startuml
start
:归还图书信息;
:查看借阅记录信息;
:获取借书时间;
if (归还日期是否逾期?) then (是)
    :还书成功;
else (否)
    :还书失败，需要缴纳罚款;
endif
    :更新图书信息;
    :更新用户信息;
stop
@enduml
```
### 3.3 "维护书目"用例
<table>
<caption align="center">"维护书目"用例规约</caption>
<tr>
  <td>用例名称</td>
  <td>维护书目</td>
</tr>
<tr>
  <td>参与者</td>
  <td>图书管理员</td>
</tr>
<tr>
  <td>前置条件</td>
  <td>1.成功登陆该系统<br>2.查询图书书目<br>3.选择维护的图书种类<br>4.操作具体的维护信息的表单或相应的操作</td>
</tr>
<tr>  
  <td>后置条件</td>
  <td>1.提交维护信息的表单后根据维护的种类在数据库中进行相应的数据表的更新操作<br>2.提示维护书目是否成功<br>3.显示维护书目的具体信息</td>
</tr>
<tr>
  <td colspan="2" align="center">主事件流</td>
</tr>
<tr>
  <td>参与者动作</td>
  <td>系统行为</td>
</tr>
<tr>
  <td>
		1. 图书管理员维护图书<br>
		2. 查询此图书<br>
	</td>
  <td>
		1. 显示图书<br>
		2. 返回给管理员对应的提示信息<br>
	</td>
</tr>
<tr>
  <td colspan="2" align="center">备选事件流</td>
</tr>
<tr>
  <td colspan="2">当没有该书籍时，提示无该书本内容<br></td>
</tr>
<tr>
  <td colspan="2" align="center">业务规则</td>
</tr>
<tr>
  <td colspan="2">1.图书管理员对图书进行日常维护</td>
</tr>
</table>
#### "维护书目"用例流程图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test2/4.png)
#### "维护书目"用例流程图源码如下：
```
@startuml
start
    :图书管理员登录;
    :列出所有图书;
    :选择所需要维护的图书;
    :维护书目;
if(是否有书目信息？) then (yes)
    :填写书目新信息;
else (no)
    :提示该图书没有书目信息;
stop
endif
    :更新信息;
stop
@enduml
```

### 3.4 "维护读者信息"用例
<table>
<caption align="center">"维护读者信息"用例规约</caption>
<tr>
  <td>用例名称</td>
  <td>维护读者信息</td>
</tr>
<tr>
  <td>参与者</td>
  <td>图书管理员</td>
</tr>
<tr>
  <td>前置条件</td>
  <td>1.身份位图书管理员<br>2.存在此读者<br></td>
</tr>
<tr>  
  <td>后置条件</td>
  <td>1.修改对应读者的信息，提示管理员维护读者信息成功<br></td>
</tr>
<tr>
  <td colspan="2" align="center">主事件流</td>
</tr>
<tr>
  <td>参与者动作</td>
  <td>系统行为</td>
</tr>
<tr>
  <td>
		1. 图书管理员查询出对应的读者信息<br>
		2. 图书管理员将更新后的读者信息提交给系统<br>
		3. 图书管理员重复步骤1，2，直到退出<br>
	</td>
  <td>
		1. 系统展示所有读者<br>
		2. 系统显示最新的读者信息<br>
		3. 系统提示图书管理员读者信息维护成功<br>
	</td>
</tr>
<tr>
  <td colspan="2" align="center">备选事件流</td>
</tr>
<tr>
  <td colspan="2">无</td>
</tr>
<tr>
  <td colspan="2" align="center">业务规则</td>
</tr>
<tr>
  <td colspan="2">图书管理员对读者信息进行维护</td>
</tr>
</table>

#### "维护读者信息"用例流程图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test2/5.png)
#### "维护读者信息"用例流程图源码如下：
```
@startuml
start
    :图书管理员登录;
    :列出所有读者信息;
    :选择读者;
    :填写读者新信息;
    :更新信息;
stop
@enduml
```

### 3.5 "查询书目"用例
<table>
<caption align="center">"查询书目"用例规约</caption>
<tr>
  <td>用例名称</td>
  <td>查询书目</td>
</tr>
<tr>
  <td>参与者</td>
  <td>读者</td>
</tr>
<tr>
  <td>前置条件</td>
  <td>成功登陆该系统</td>
</tr>
<tr>  
  <td>后置条件</td>
  <td>显示出对应查询的图书信息</td>
</tr>
<tr>
  <td colspan="2" align="center">主事件流</td>
</tr>
<tr>
  <td>参与者动作</td>
  <td>系统行为</td>
</tr>
<tr>
  <td>
		1. 读者输出查询图书<br>
		2. 点击查询书目的按钮	
	</td>
  <td>
		1. 系统根据图书信息查询数据库<br>
		2. 显示图书信息<br>
	</td>
</tr>
<tr>
  <td colspan="2" align="center">备选事件流</td>
</tr>
<tr>
  <td colspan="2">没有查询的图书时，要提示用户没有</td>
</tr>
<tr>
  <td colspan="2" align="center">业务规则</td>
</tr>
<tr>
  <td colspan="2">登陆身份为读者，输入图书信息查询读书</td>
</tr>
</table>

#### "查询书目"用例流程图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test2/6.png)
#### "查询书目"用例流程图源码如下：
```
@startuml 
start 
    :读者登录; 
    :查询图书;  
    :输入所需要查询的图书; 
if(是否有该图书？) then (是) 
    :显示该图书信息; 
else (否) 
    :提示不存在该图书; 
stop 
endif 
    :查看图书; 
stop
@enduml 
```

### 3.6 "查询借阅情况"用例
<table>
<caption align="center">"查询借阅情况"用例规约</caption>
<tr>
  <td>用例名称</td>
  <td>查询借阅情况</td>
</tr>
<tr>
  <td>参与者</td>
  <td>读者</td>
</tr>
<tr>
  <td>前置条件</td>
  <td>成功登陆该系统，点击查询借阅情况链接</td>
</tr>
<tr>  
  <td>后置条件</td>
  <td>显示出对应的读者的借阅情况的信息</td>
</tr>
<tr>
  <td colspan="2" align="center">主事件流</td>
</tr>
<tr>
  <td>参与者动作</td>
  <td>系统行为</td>
</tr>
<tr>
  <td>
		1. 读者登陆该<br>
		2. 查询借阅信息
	</td>
  <td>
		1. 系统查询数据库<br>
		2. 借阅图书信息<br>
	</td>
</tr>
<tr>
  <td colspan="2" align="center">备选事件流</td>
</tr>
<tr>
  <td colspan="2">不存在该借阅信息<br></td>
</tr>
<tr>
  <td colspan="2" align="center">业务规则</td>
</tr>
<tr>
  <td colspan="2">读者查询借阅信息</td>
</tr>
</table>
#### "查询借阅情况"用例流程图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test2/7.png)
#### "查询借阅情况"用例流程图源码如下：
```
@startuml
start
    :读者登录;
    :查询借阅情况;
    :列出读者借阅信息;
if(是否存在借阅信息？) then (是)
    :显示借阅信息;
stop
else (否)
    :提示不存在任何借阅信息;
stop

@enduml
```

### 3.7 "预定图书"用例
<table>
<caption align="center">"预定图书"用例规约</caption>
<tr>
  <td>用例名称</td>
  <td>预定图书</td>
</tr>
<tr>
  <td>参与者</td>
  <td>读者</td>
</tr>
<tr>
  <td>前置条件</td>
  <td>
  	1. 读者登陆<br>
  	2. 选择预定图书功能
  </td>
</tr>
<tr>  
  <td>后置条件</td>
  <td>
  	1. 返回预定结果
	</td>
</tr>
<tr>
  <td colspan="2" align="center">主事件流</td>
</tr>
<tr>
  <td>参与者动作</td>
  <td>系统行为</td>
</tr>
<tr>
  <td>
		1. 读者登录 <br>
		2. 预定图书
	</td>
  <td>
		1. 系统显示所有图书<br>
		2. 查询库存<br>
		3. 返回预定结果
	</td>
</tr>
<tr>
  <td colspan="2" align="center">备选事件流</td>
</tr>
<tr>
  <td colspan="2">
  	该图书库存为0
  </td>
</tr>
<tr>
  <td colspan="2" align="center">业务规则</td>
</tr>
<tr>
  <td colspan="2">若无库存，则不能预定</td>
</tr>
</table>
#### "预定图书"用例流程图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test2/8.png)
#### "预定图书"用例流程图源码如下：
```
@startuml
start
    :读者登录;
    :列出所有图书;
    :选择预定图书;
    :预定图书;
    :填写预定单;
if(该图书是否还有库存？) then (是)
    :图书已全部借出，不能进行预定;
stop
else (否)
    :确认预定信息;
    :预定成功;
stop
@enduml
```

### 3.8 "取消预定图书"用例
<table>
<caption align="center">"取消预定"用例规约</caption>
<tr>
  <td>用例名称</td>
  <td>取消预定</td>
</tr>
<tr>
  <td>参与者</td>
  <td>读者</td>
</tr>
<tr>
  <td>前置条件</td>
  <td>
  	1. 读者登陆<br>
  	2. 存在预定图书的信息<br>
  </td>
</tr>
<tr>  
  <td>后置条件</td>
  <td>
  	1. 返回预定结果<br>
	    2. 更新预订单<br>
	</td>
</tr>
<tr>
  <td colspan="2" align="center">主事件流</td>
</tr>
<tr>
  <td>参与者动作</td>
  <td>系统行为</td>
</tr>
<tr>
  <td>
		1. 读者登录 <br>
		2. 取消预订<br>
		3. 选择图书
	</td>
  <td>
		1. 更新图书预订单<br>
		2. 返回结果
	</td>
</tr>
<tr>
  <td colspan="2" align="center">备选事件流</td>
</tr>
<tr>
  <td colspan="2">
  	无
  </td>
</tr>
<tr>
  <td colspan="2" align="center">业务规则</td>
</tr>
<tr>
  <td colspan="2">预订单取消后更新预订单</td>
</tr>
</table>
#### "取消预定图书"用例流程图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test2/9.png)
#### "取消预定图书"用例流程图源码如下：
```
@startuml
start
    :用户登录;
    :查看预订单;
    :选择取消图书的预定单;
    :取消预定;
    :预定单更新;
stop
@enduml
```

### 3.9 "修改密码"用例
<table>
<caption align="center">"修改密码"用例规约</caption>
<tr>
  <td>用例名称</td>
  <td>修改密码</td>
</tr>
<tr>
  <td>参与者</td>
  <td>系统管理员、图书管理员、读者</td>
</tr>
<tr>
  <td>前置条件</td>
  <td>
  	系统管理员、图书管理员或读者登录到系统<br>
  </td>
</tr>
<tr>  
  <td>后置条件</td>
  <td>
  	产生并保存修改记录和修改后的密码
	</td>
</tr>
<tr>
  <td colspan="2" align="center">主事件流</td>
</tr>
<tr>
  <td>参与者动作</td>
  <td>系统行为</td>
</tr>
<tr>
  <td>
		1. 系统管理员、图书管理员或读者跳转到修改密码的页面 <br>
		2. 系统管理员、图书管理员或读者填写旧密码及新密码 <br>
	</td>
  <td>
		1. 系统保存新密码，用例结束
	</td>
</tr>
<tr>
  <td colspan="2" align="center">备选事件流</td>
</tr>
<tr>
  <td colspan="2">
  	当旧密码输入错误，系统提示旧密码输入错误<br>
  </td>
</tr>
<tr>
  <td colspan="2" align="center">业务规则</td>
</tr>
<tr>
  <td colspan="2">1.用户的编号不能修改<br>2.登录才能修改</td>
</tr>
</table>

#### "取消预定图书"用例流程图如下：
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test2/10.png)
#### "取消预定图书"用例流程图源码如下：
```
@startuml
start
    :登录;
    :跳转到修改用户密码页面;
    :输入旧密码和新密码;
if (旧密码错误) then (yes)
    :提示旧密码错误;
else (no)
    :显示“修改密码成功”;
endif
stop
@enduml
```
