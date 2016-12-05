# 用户账户接口

基本功能接口是广义的Obisoft接口，不针对单独BeautyTeam产品。所有Obisoft旗下业务均需要调用基本功能接口

### 登录API

#### 说明

本API可以把当前用户状态由匿名切换到已登录状态或待二重验证状态。必须搭载Token进行调用

#### 地址  
>[/api/Login](/api/Login)

#### 方法  

**POST**

#### 参数列表：	
<table class="table table-bordered table-striped">
  <tbody>
	  <tr>
		<th>参数名</th>
		<th>必选</th>
		<th>参数类型</th>
		<th>参数说明</th>
	  </tr>
	  <tr>
		<td>Email</td>
		<td>true</td>
		<td>Email</td>
		<td>用作Obisoft账号的邮箱号码</td>
	  </tr>
	  <tr>
		<td>Password</td>
		<td>true</td>
		<td>string, 最少6字符</td>
		<td>Obisoft账号的密码</td>
	  </tr>
	  <tr>
		<td>RememberMe</td>
		<td>true</td>
		<td>bool</td>
		<td>是否记住密码。若为true，则cookie将会在浏览器外保存，否则Cookie会随程序销毁而丢失。</td>
	  </tr>
	</tbody>
</table>

#### 返回值:
 
	{
	  "Result": "Successfully Signed in.",
	  "Code": 0
	}

#### 可能的返回值：
<table class="table table-bordered table-striped">
  <tbody>
	  <tr>
		<th>错误号</th>
		<th>含义</th>
	  </tr>
	  <tr>
		<td>0</td>
		<td>登录成功</td>
	  </tr>
	  <tr>
		<td>-3</td>
		<td>等待进行第二步认证</td>
	  </tr>
	  <tr>
		<td>-2</td>
		<td>账号已被封禁</td>
	  </tr>
	  <tr>
		<td>-1</td>
		<td>用户名或密码错误</td>
	  </tr>
	  <tr>
		<td>-10</td>
		<td>用户名不合法或密码太短</td>
	  </tr>
	</tbody>
</table>

#### 例如:

	{
	  "Result": "Wrong Account",
	  "Code": -1
	}

### 注册API

#### 说明

本API生成一个可用的Obisoft用户

#### 地址  
>[/api/Register](/api/Register)

#### 方法  

**POST**

#### 参数列表：	
<table class="table table-bordered table-striped">
  <tbody>
	  <tr>
		<th>参数名</th>
		<th>必选</th>
		<th>参数类型</th>
		<th>参数说明</th>
	  </tr>
	  <tr>
		<td>Email</td>
		<td>true</td>
		<td>Email</td>
		<td>用作Obisoft账号的邮箱号码</td>
	  </tr>
	  <tr>
		<td>Password</td>
		<td>true</td>
		<td>string, 最少6字符</td>
		<td>Obisoft账号的密码</td>
	  </tr>
	  <tr>
		<td>ConfirmPassword</td>
		<td>false</td>
		<td>string, 最少6字符, 必须和Password相同</td>
		<td>重复密码</td>
	  </tr>
	</tbody>
</table>

#### 返回值:
 
	{
	  "Result": "Successfully Registered",
	  "Code": 0
	}

#### 可能的返回值：
<table class="table table-bordered table-striped">
  <tbody>
	  <tr>
		<th>错误号</th>
		<th>含义</th>
	  </tr>
	  <tr>
		<td>0</td>
		<td>注册成功，并且已经完成登录，并发送了账户验证邮件。（不需要验证邮箱就可以登录）</td>
	  </tr>
	  <tr>
		<td>-7</td>
		<td>用于注册的邮箱已经注册过了</td>
	  </tr>
	  <tr>
		<td>-10</td>
		<td>邮箱不合法或密码不合法</td>
	  </tr>
	</tbody>
</table>

#### 示例： 

	{
	  "Errors": [
		{
		  "Code": "DuplicateUserName",
		  "Description": "User name 'mma@obisoft.com.cn' is already taken."
		}
	  ],
	  "Result": "It seems that the email has already been used.",
	  "Code": -7
	}

### 忘记密码

#### 说明

本API将会向用户注册的邮箱发送认证邮件。用户单击邮箱中的链接即可重置密码，不需要客户端二次干涉

>[/api/ForgotPassword](/api/ForgotPassword)

#### 方法

**POST**

#### 参数列表

<table class="table table-bordered table-striped">
  <tbody>
	  <tr>
		<th>参数名</th>
		<th>必选</th>
		<th>参数类型</th>
		<th>参数说明</th>
	  </tr>
	  <tr>
		<td>Email</td>
		<td>true</td>
		<td>Email</td>
		<td>用作Obisoft账号的邮箱号码</td>
	  </tr>
	</tbody>
</table>

#### 返回值

	{
	  "Result": "Email Sent",
	  "Code": 0
	}
#### 可能的返回值：
<table class="table table-bordered table-striped">
  <tbody>
	  <tr>
		<th>错误号</th>
		<th>含义</th>
	  </tr>
	  <tr>
		<td>0</td>
		<td>认证邮件已经发送。请提醒用户前往邮箱。</td>
	  </tr>
	  <tr>
		<td>-4</td>
		<td>目标邮箱没有找到对应的用户。</td>
	  </tr>
	  <tr>
		<td>-10</td>
		<td>邮箱不合法</td>
	  </tr>
	</tbody>
</table>

### 发送认证邮件

#### 说明

本API可以向未完成邮箱认证的用户发送一封邮件。用户单击邮件中的链接即可完成邮箱认证

在邮箱认证完成前，我们不允许使用邮箱进行二重身份认证

#### 需要权限

已经登录Obisoft账户

#### 地址

>[/api/VerifyEmail](/api/VerifyEmail)

#### 方法

**POST**

#### 参数列表

无参数

#### 返回值

	{
	  "Result": "Email Sent",
	  "Code": 0
	}

#### 可能的返回值：
<table class="table table-bordered table-striped">
  <tbody>
	  <tr>
		<th>错误号</th>
		<th>含义</th>
	  </tr>
	  <tr>
		<td>0</td>
		<td>邮件发送成功。</td>
	  </tr>
	  <tr>
		<td>-6</td>
		<td>已经通过了验证。</td>
	  </tr>
	  <tr>
		<td>-8</td>
		<td>用户尚未登录。</td>
	  </tr>
	</tbody>
</table>

例如：

	{
	  "Result": "Already Confirmed your Email!",
	  "Code": -6
	}

### 查看我的个人信息

#### 所需权限

已经登录Obisoft账户

#### 地址

>[/api/UserInfo](/api/UserInfo)

#### 方法

GET

#### 参数列表

无

#### 返回值

	{
	  "Result": "Successfully Get.",
	  "Code": 0,
	  "user": {
		"id": "b649a816-9150-4aa3-8ac9-04eb59fc1301",
		"email": "mma@Obisoft.com.cn",
		"emailConfirmed": true,
		"phone": null,
		"phoneConfirmed": false,
		"nick": "mma",
		"icon": "https://www.gravatar.com/avatar/fcee50d4ba19f7c86c443df6a24378e9.png?s=160&d=https%3A%2F%2Fobisoft.oss-cn-beijing.aliyuncs.com%2FWebSiteIcon%2FIcon.jpg"
	  }
	}

#### 可能的返回值：
<table class="table table-bordered table-striped">
  <tbody>
	  <tr>
		<th>错误号</th>
		<th>含义</th>
	  </tr>
	  <tr>
		<td>0</td>
		<td>已经成功取得用户信息。</td>
	  </tr>
	  <tr>
		<td>-8</td>
		<td>用户尚未登录。</td>
	  </tr>
	</tbody>
</table>

### 查看特定用户的信息

#### 方法

GET

#### 地址
 
>[/api/Another](/api/Another)

#### 参数列表

<table class="table table-bordered table-striped">
  <tbody>
	  <tr>
		<th>参数名</th>
		<th>必选</th>
		<th>参数类型</th>
		<th>参数说明</th>
	  </tr>
	  <tr>
		<td>Id</td>
		<td>true</td>
		<td>string</td>
		<td>Obisoft ID</td>
	  </tr>
	</tbody>
</table>

#### 返回值

	{
	  "Result": "Successfully Get.",
	  "Code": 0,
	  "user": {
		"id": "b649a816-9150-4aa3-8ac9-04eb59fc1301",
		"email": "mma@Obisoft.com.cn",
		"nick": "mma",
		"icon": "https://www.gravatar.com/avatar/fcee50d4ba19f7c86c443df6a24378e9.png?s=160&d=https%3A%2F%2Fobisoft.oss-cn-beijing.aliyuncs.com%2FWebSiteIcon%2FIcon.jpg",
		"des": "Nothing to say"
	  }
	}

### 根据Email查询一个用户的ID

#### 说明

很多情况下无法得到目标用户ID而仅仅取得了他的Email。本API能够直接将一个Email换为用户ID。

#### 方法

GET

#### 地址

>[/api/EmailToId](/api/EmailToId)

#### 参数列表

<table class="table table-bordered table-striped">
  <tbody>
	  <tr>
		<th>参数名</th>
		<th>必选</th>
		<th>参数类型</th>
		<th>参数说明</th>
	  </tr>
	  <tr>
		<td>Email</td>
		<td>true</td>
		<td>Email</td>
		<td>邮箱地址，必须是已经存在的Obisoft账户对应的邮箱账号</td>
	  </tr>
	</tbody>
</table>

#### 返回值

	{
	  "Result": "Successfully Found!",
	  "Id": "b649a816-9150-4aa3-8ac9-04eb59fc1301",
	  "Code": 0
	}

#### 可能的返回值：
<table class="table table-bordered table-striped">
  <tbody>
	  <tr>
		<th>错误号</th>
		<th>含义</th>
	  </tr>
	  <tr>
		<td>0</td>
		<td>已经成功取得目标用户。</td>
	  </tr>
	  <tr>
		<td>-10</td>
		<td>邮箱地址不合法。</td>
	  </tr>
	  <tr>
		<td>-4</td>
		<td>没有找到目标用户</td>
	  </tr>
	</tbody>
</table>

### 修改密码

#### 所需权限

已经登录

#### 地址

>[/api/ChangePass](/api/ChangePass)

#### 方法

POST

#### 参数列表

<table class="table table-bordered table-striped">
  <tbody>
	  <tr>
		<th>参数名</th>
		<th>必选</th>
		<th>参数类型</th>
		<th>参数说明</th>
	  </tr>
	  <tr>
		<td>OldPassword</td>
		<td>true</td>
		<td>string</td>
		<td>账户的旧密码</td>
	  </tr>
	  <tr>
		<td>NewPassword</td>
		<td>true</td>
		<td>string</td>
		<td>账户的新密码</td>
	  </tr>
	  <tr>
		<td>ConfirmPassword</td>
		<td>true</td>
		<td>string</td>
		<td>账户密码确认，必须和NewPassword完全一致</td>
	  </tr>
	</tbody>
</table>

#### 返回值

	{
		Result : "Successfully Changed your password",
		Code : 0 
	}

#### 可能的返回值：
<table class="table table-bordered table-striped">
  <tbody>
	  <tr>
		<th>错误号</th>
		<th>含义</th>
	  </tr>
	  <tr>
		<td>0</td>
		<td>密码已经成功修改</td>
	  </tr>
	  <tr>
		<td>-1</td>
		<td>旧密码错误</td>
	  </tr>
	  <tr>
		<td>-8</td>
		<td>未登录</td>
	  </tr>
	  <tr>
		<td>-10</td>
		<td>两次输入的密码不相同</td>
	  </tr>
	</tbody>
</table>

### 查看当前登录状态

#### 说明

很多API需要已经登录的权限。对于此类API，可能会由于长时间未登录而产生Cookie过期的现象，这将会产生-8返回值。一旦发现此返回值务必马上重新静默登录。登录失败时应重新定向到登录页。

#### 地址

>[/api/SignInStatus](/api/SignInStatus)

#### 方法

GET

#### 参数列表

无

#### 返回值

	{
		Result : "Signed in",
		Code : 0
	}

#### 可能的返回值：
<table class="table table-bordered table-striped">
  <tbody>
	  <tr>
		<th>错误号</th>
		<th>含义</th>
	  </tr>
	  <tr>
		<td>0</td>
		<td>已经登录</td>
	  </tr>
	  <tr>
		<td>-3</td>
		<td>未登录</td>
	  </tr>
	</tbody>
</table>

### 注销

#### 说明

这将会把已登录的权限转换为未登录的权限

#### 需要权限

已经登录

#### 地址

>[/api/LogOff](/api/LogOff)

#### 方法

POST

#### 参数列表

无

#### 返回值

	{
	  "Result": "Signed out",
	  "Code": 0
	}

#### 可能的返回值：
<table class="table table-bordered table-striped">
  <tbody>
	  <tr>
		<th>错误号</th>
		<th>含义</th>
	  </tr>
	  <tr>
		<td>0</td>
		<td>已经注销</td>
	  </tr>
	  <tr>
		<td>-8</td>
		<td>未登录</td>
	  </tr>
	</tbody>
</table>