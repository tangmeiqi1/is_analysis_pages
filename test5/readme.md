# 实验五：图书管理系统数据库设计与页面设计
|    学号    |       班级       |      姓名     |       照片   |
|:-------:|:-------------:|:----------:|:----------:|
| 201710414316  |   17软工3班     |   唐美琪   |   无  |
## 1.数据库表设计
### 1.1 图书表
<table>
  <tr>
    <td>字段</td>
    <td>类型</td>
    <td>主键，外键</td>
    <td>可以为空</td>
    <td>默认值</td>
    <td>约束</td>
    <td>说明</td>
  </tr>
  <tr>
    <td>ISBN</td>
    <td>varchar2(100)</td>
    <td>主键</td>
    <td>否</td>
    <td></td>
    <td></td>
    <td>图书编号</td>
  </tr>
  <tr>
    <td>Name</td>
    <td>varchar2(100)</td>
    <td></td>
    <td>否</td>
    <td></td>
    <td></td>
    <td>图书名字</td>
  </tr>
  <tr>
    <td>Memo</td>
    <td>varchar2(100)</td>
    <td></td>
    <td>是</td>
    <td></td>
    <td></td>
    <td>著作人</td>
  </tr>
  <tr>
      <td>Price</td>
      <td>varchar2(100)</td>
      <td></td>
      <td>否</td>
      <td></td>
      <td></td>
      <td>图书价格</td>
    </tr>
    <tr>
        <td>Number</td>
        <td>varchar2(100)</td>
        <td></td>
        <td>否</td>
        <td>0</td>
        <td></td>
        <td>该图书的数量</td>
      </tr>
</table>

### 1.2 读者表
<table>
  <tr>
    <td>字段</td>
    <td>类型</td>
    <td>主键，外键</td>
    <td>可以为空</td>
    <td>默认值</td>
    <td>约束</td>
    <td>说明</td>
  </tr>
  <tr>
    <td>Stu_name</td>
    <td>varchar2(10)</td>
    <td></td>
    <td>否</td>
    <td></td>
    <td></td>
    <td>读者姓名</td>
  </tr>
  <tr>
    <td>Stu_ID</td>
    <td>varchar2(100)</td>
    <td>主键</td>
    <td>否</td>
    <td></td>
    <td></td>
    <td>读者身份证号</td>
  </tr>
  <tr>
    <td>Stu_id</td>
    <td>varchar2(100)</td>
    <td>外键</td>
    <td>否</td>
    <td></td>
    <td></td>
    <td>读者借书卡号</td>
  </tr>
   <tr>
      <td>Stu_pw</td>
      <td>varchar2(100)</td>
      <td>外键</td>
      <td>是</td>
      <td></td>
      <td></td>
      <td>读者借书卡号密码</td>
    </tr>
  <tr>
      <td>Book_sum</td>
      <td>varchar2(10)</td>
      <td></td>
      <td>否</td>
      <td>10</td>
      <td></td>
      <td>该生可借图书限额</td>
    </tr>
    <tr>
        <td>Book_borrow</td>
        <td>varchar2(100)</td>
        <td></td>
        <td>否</td>
        <td>0</td>
        <td></td>
        <td>该生已借图书数</td>
      </tr>
      <tr>
              <td>Data</td>
              <td>get</td>
              <td></td>
              <td>否</td>
              <td></td>
              <td></td>
              <td>图书借阅时间</td>
            </tr>
    
</table>

### 1.3 管理员表
<table>
  <tr>
    <td>字段</td>
    <td>类型</td>
    <td>主键，外键</td>
    <td>可以为空</td>
    <td>默认值</td>
    <td>约束</td>
    <td>说明</td>
  </tr>
  <tr>
    <td>Admin_name</td>
    <td>varchar2(10)</td>
    <td>外键</td>
    <td>否</td>
    <td></td>
    <td></td>
    <td>管理员姓名</td>
  </tr>
  <tr>
    <td>Admin_ID</td>
    <td>varchar2(100)</td>
    <td>主键</td>
    <td>否</td>
    <td></td>
    <td></td>
    <td>管理员职工号</td>
  </tr>
</table>

## 2.界面设计
### 2.1 登录页面设计
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test5/登录页面.png)
 * 功能：用于用户登录
 * 请求地址：https://tangmeiqi1.github.io/is_analysis_pages/index.html
 * 请求方式：post
 * 请求参数：
 <table>
   <tr>
     <td>参数名</td>
     <td>必填</td>
     <td>说明</td>
   </tr>

   <tr>
     <td>Stu_id</td>
     <td>是</td>
     <td>读者借书ID号</td>
   </tr> 
   <tr>
             <td>Stu_pw</td>
             <td>是</td>
             <td>用于读者登录</td>
           </tr>
   </table>
 * 返回实例
 
 ```
 {
 "info":"登录成功"
    "data":{
      "Stu_id":"123456789",
      "Stu_pw":"123"，
      "Stu_name":李三，
        }，
    "code":200
 }
 ```

 * 返回参数说明：
 <table>
   <tr>
     <td>参数名</td>
     <td>说明</td>
   </tr>
   <tr>
     <td>Stu_id</td>
     <td>读者卡号</td>
   </tr>
   <tr>
     <td>Stu_name</td>
     <td>读者姓名</td>
   </tr>
   </table>

### 2.2 学生主页页面设计
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test5/学生主页.png)
* 功能：用于显示读者主页
 * 请求地址：https://tangmeiqi1.github.io/is_analysis_pages/student.html
 * 请求方式：post
 * 请求参数：
 <table>
   <tr>
     <td>参数名</td>
     <td>必填</td>
     <td>说明</td>
   </tr>

   <tr>
     <td>Stu_id</td>
     <td>是</td>
     <td>读者借书ID号</td>
   </tr> 
   <tr>
             <td>Stu_pw</td>
             <td>是</td>
             <td>用于读者登录</td>
           </tr>
   </table>
 * 返回实例
 
 ```
 {
 "info":"登录成功"‘
    "data":{
      "Stu_id":"123456789",
      "Stu_name":李三,
      "Stu_sum":8,
      "Stu_borroe":4,
    },
    "code":200
 }
 ```

 * 返回参数说明：
 <table>
   <tr>
     <td>参数名</td>
     <td>说明</td>
   </tr>
   <tr>
     <td>Stu_id</td>
     <td>读者卡号</td>
   </tr>
   <tr>
     <td>Stu_name</td>
     <td>读者姓名</td>
   </tr>
   <tr>
        <td>Book_sum</td>
        <td>借阅书籍总数</td>
      </tr>
      <tr>
           <td>Book_borrow</td>
           <td>未还借阅书籍</td>
         </tr>
         </table>


### 2.3 借书页面设计
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test5/借书页面.png)
 * 功能：用于用户借阅图书
 * 请求地址：https://tangmeiqi1.github.io/is_analysis_pages/borrow.html
 * 请求方式：post
 * 请求参数：
 <table>
   <tr>
     <td>参数名</td>
     <td>必填</td>
     <td>说明</td>
   </tr>
   <tr>
     <td>ISBN</td>
     <td>是</td>
     <td>用于确定该图书</td>
   </tr>
   <tr>
     <td>Name</td>
     <td>是</td>
     <td>读书名字</td>
   </tr>
    <tr>
        <td>Data</td>
        <td>是</td>
        <td>借书时间</td>
      </tr>
   </table>
 * 返回实例
 
  ```
  {
  "info":"借阅成功"‘
     "data":{
       "Stu_id":"123456789",
       "Stu_name":李三,
       "Stu_sum":8,
       "Stu_borrow":4,
       "ISBN":"987-654-321"
       "Name":"鲁宾逊漂流记"
       "Data":"2020-04-20",
     },
     "code":200
  }
  ```
  
 * 返回参数说明：
 <table>
   <tr>
     <td>参数名</td>
     <td>说明</td>
   </tr>
   <tr>
     <td>ISBN</td>
     <td>图书编号</td>
   </tr>
   <tr>
     <td>Name</td>
     <td>图书名字</td>
   </tr>
 

### 2.4 还书页面设计
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test5/还书页面.png)
 * 功能：用于用户还书
 * 请求地址：https://tangmeiqi1.github.io/is_analysis_pages/return.html
 * 请求方式：post
 * 请求参数：
 <table>
   <tr>
     <td>参数名</td>
     <td>必填</td>
     <td>说明</td>
   </tr>
   <tr>
     <td>ISBN</td>
     <td>是</td>
     <td>用于确定该图书</td>
   </tr>
   <tr>
     <td>Stu_id</td>
     <td>是</td>
     <td>读者借书ID号</td>
   </tr>
   </table>
   
 * 返回实例
   ```
   {
   "info":"还书成功"‘
      "data":{
        "Stu_id":"123456789",
        "Stu_name":李三,
        "ISBN":"987-654-322"
        "Name":"红楼梦"
        "Data":"2020-02-20",
      },
      "code":200
   }
   ```
   
 * 返回参数说明：
 <table>
   <tr>
     <td>参数名</td>
     <td>说明</td>
   </tr>
   <tr>
     <td>ISBN</td>
     <td>图书编号</td>
   </tr>
   <tr>
     <td>Name</td>
     <td>图书名字</td>
   </tr>
   <tr>
        <td>Data</td>
        <td>借书时间</td>
      </tr>
   </table>
 

### 2.5 个人信息页面设计
![CSDN图标](https://github.com/tangmeiqi1/is_analysis/blob/master/test5/个人信息.png)
 * 功能：用于修改密码
 * 请求地址：https://tangmeiqi1.github.io/is_analysis_pages/personage.html
 * 请求方式：post
 * 请求参数：
 <table>
    <tr>
      <td>参数名</td>
      <td>必填</td>
      <td>说明</td>
    </tr>
    <tr>
      <td>Stu_id</td>
      <td>是</td>
      <td>读者借书ID号</td>
    </tr> 
    <tr>
              <td>Stu_pw</td>
              <td>是</td>
              <td>用于读者登录</td>
            </tr>
             <tr>
                  <td>Stu_name</td>
                  <td>是</td>
                  <td>读者姓名</td>
                </tr> 
    </table>
  * 返回实例
  
  ```
  {
  "info":"修改密码成功"‘
     "data":{
       "Stu_id":"123456789",
       "Stu_pw":"123456"，
       "Stu_name":李三，
         }，
     "code":200
  }
  ```
 
  * 返回参数说明：
  <table>
    <tr>
      <td>参数名</td>
      <td>说明</td>
    </tr>
    <tr>
      <td>Stu_id</td>
      <td>读者卡号</td>
    </tr>
    <tr>
      <td>Stu_name</td>
      <td>读者姓名</td>
    </tr>
    <tr>
          <td>Stu_pw</td>
          <td>读者新密码</td>
        </tr>
</table>
</table>