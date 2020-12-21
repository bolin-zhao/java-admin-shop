# **后台在线银行管理系统 **jdbc-admin-system

1. ### 业务需求文档

   > 三层架构 :
   >
   > * 1.客户管理
   >
   > > - 1.1添加客户
   > >
   > >   ```
   > >   添加客户资料，其包括客户名称、密码、注册日期、上次登录时间、地址、电子邮箱、电话
   > >   备注：添加的客户名称不能相同
   > >   ```
   > >
   > > - 1.2客户登录
   > >
   > >   ```
   > >   检查客户输入名称和密码进行登录验证
   > >   ```
   > >
   > > - 1.3查看客户个人资料(密码不要显示)
   > >
   > >   ```java
   > >   根据客户名称查看客户资料信息，其包括内容有客户名称、地址、电子邮箱、电话、上次登录时间
   > >   备注：密码信息不需要显示
   > >   ```
   > >
   > > - 1.4更新客户个人资料(客户名不能修改)
   > >
   > >   ```
   > >   根据客户名称修改客户资料，其包括（地址、电子邮箱、电话）
   > >   备注：客户名称不能修改
   > >   ```
   > >
   > > - 1.5修改客户密码()
   > >
   > >   ```
   > >   根据客户名称修改密码
   > >   备注：客户修改密码，先输入旧密码，正确后才能修改密码
   > >   ```
   > >
   > > - 1.6查询客户
   > >
   > >   ```
   > >   根据客户名称进行模糊查询符合条件的客户列表
   > >   符合条件：1、vvip账号(存款余额大于1000W)。2、vip账号(存款余额1000W-100W)。3、一般客户账号(100W以下)。1000W)。2、vip账号(存款余额1000W-100W)。3、一般客户账号(100W以下)。
   > >   ```
   >
   > * 2.卡号(账号管理)
   >
   >   >- 2.1 添加账号
   >   >
   >   >  ```
   >   >  用户登录后，客户可以为自己的一个或者多个账号
   >   >  备注：添加的账号由系统自动生成且账号余额默认为0
   >   >  ```
   >   >
   >   >- 2.2 查看账户资料
   >   >
   >   >  ```
   >   >  客户可以根据账号查看当前账号的信息。如:余额、账号状态等.
   >   >  ```
   >   >
   >   >- 2.3 存款
   >   >
   >   >  ```
   >   >  客户可以为自己账号存钱操作(当用户的账号余额满足1.6符合条件时，自动提升或降低客户等级)
   >   >  ```
   >   >
   >   >- 2.4 取款
   >   >
   >   >  ```
   >   >  客户可以根据自己的账号进行取钱操作
   >   >  备注：余额不足，不能完成取款操作
   >   >  ```
   >   >
   >   >- 2.5 转账
   >   >
   >   >  ```
   >   >  客户可以根据不同账号进行转账操作
   >   >  (根据客户等级收取相应的手续费.vvip，vip免收，一般用户0.2%)
   >   >  备注：余额不足，不能完成转账操作
   >   >  ```
   >   >
   >   >- 2.6 注销账号
   >   >
   >   >  ```
   >   >  客户可以注销其下账号。账号注销之后，不是删除，而是修改其状态。（注销的时候要判断一下账号金额哦！难道都想把钱给银行？并且在存款、取款、转账时候要判断是否是已注销账号）
   >   >  ```
   >   >
   >   >- 2.7 激活账号
   >   >
   >   >  ```
   >   >  该登录用户其下注销账号恢复正常使用，并缴纳10元手续费。
   >   >  ```
   >
   > * 3.交易日志管理
   >
   >   > 3.1 添加日志记录
   >   >
   >   > ```
   >   > 当客户进行存款、取款、转账操作成功后，添加对应交易日志管理记录
   >   > 备注：交易记录不能单独添加
   >   > ```
   >   >
   >   > 3.2 查看账号交易记录
   >   >
   >   > ```
   >   > 客户根据账号查看对应账号交易记录
   >   > ```

   1. 客户表 custinfo

   ![image-20201218133059759](C:\Users\16670\AppData\Roaming\Typora\typora-user-images\image-20201218133059759.png)

   2. 账户表 account

      ![image-20201218133329067](C:\Users\16670\AppData\Roaming\Typora\typora-user-images\image-20201218133329067.png)

   ​			c. 日志表 log

   ![image-20201218133357837](C:\Users\16670\AppData\Roaming\Typora\typora-user-images\image-20201218133357837.png)

2. ### 开发准备

   ```java
   	使用Java SE 课程内容开发
   	掌握构造方法的定义及使用
   	掌握继承、重载与重写并灵活应用
   	熟练处理异常
   	掌握常用集合类的使用
   	掌握JDBC的运用
   	项目概要
   ```

3. ### 技术需求

   ```java
   1. 开发工具: IDEA 
   2. 数据库: MySQL + sqlyog
   3. 技术储备: JDBC + MYSQL + 集合,异常处理, + Javase   
   ```

4. ### 项目代码

   > 1. [点击去我的 github]: https://github.com/bolin-zhao/jdbc-admin-system.git
   >
   > 2. 项目结构: 1. Dao层(封装了一个 jdbc 连接数据库和对数据库增删改查的方法)
   >
   > 3. Customer.java里封装了所有的业务逻辑方法
   >
   > 4. BankUI .java层是用户 UI界面,也是测试类.
   >
   > 5. jdbc.properties 里包含用户来连接数据库的driver/user/pwd/url
   >
   > ![image-20201221140737016](C:\Users\16670\AppData\Roaming\Typora\typora-user-images\image-20201221140737016.png)
   >
   > 

5. ### 答辩环节

   ```java
   谈一谈遇到的问题和解决办法:
   	1. 由于项目比较简单,就没有使用MVC设计模式
       2. 答辩时,声音不够洪亮,像自说自话,不够自信,显得自己很weak!
       3. 建表时: 通过sqlyog直接建表,主外键关系,使用sqlyog定义.
       4. 未解决问题: 如何让cname姓名不重复?  建表时列设为unique可以解决,也可以通过查询判断
       5. 还有一些不足,比如没有定义返回上级菜单方法,导致有些操作需要重新登陆,时间紧迫,难度也低,这里不再花费太多的的时间去完善.   
   ```

   

6. ### 项目总结

   ```java
   谈一谈个人感想和反思:
   	身为编程人员,沟通和交流也是一项很重要的能力,不但要把项目做好,跑起来,还要用业务的思想去演示项目,单纯的实现每个方法固然重要,但是要把所有的方法串联起来,形成一个完整的闭环,则显得更加重要.
   	技术再好,说不出来也是徒劳,就算把项目做好,在沟通环节出了问题那只会让我们显得很low,无法获得leader的认可,更无法说服客户,卖出自己的产品!
   	本次银行项目,给我一次警醒,重业务逻辑的同时,要分配一些精力到测试和项目解读上面,更要在极短的时间内,获取自己想要的结果,根据项目的重点和面向的用户群体,制定出讲解的流程和思路.    
   ```

   