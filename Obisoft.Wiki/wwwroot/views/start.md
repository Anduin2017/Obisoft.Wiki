# 开始开发

服务器采用HTTPS通信  

参数编码采用URL编码，可以使用jQuery直接编码

**客户端采用Cookie保持状态。目前仅允许向域：http://localhost:9000/ 共享Cookie。使用Cordova技术开发的客户端务必工作在该域下。**  

请注意开启通信的认证开关，保证Cookie状态可以保持

服务器地址：[https://www.obisoft.com.cn](https://www.obisoft.com.cn)

### Hello World API
本API用于让开发者学习调用Obisoft API。

地址：
>[/api](/api/)   

方法：GET  

返回值：  
 
	{  
		"Result":"Hello World!",  
		"Code":0  
	} 

**本API不需要Token即可调用。可以采用本API检查Obisoft服务器是否处于工作状态**

### 换取Token
本API用于将AppId和AppSecret换取Token  

不要在每次调用都换取。请注意留存Token。Token生存期两小时

更多重要内容请在‘开始前必读’中了解

#### 地址：  

>[/api/token](/api/Token?AppId=22222&AppSecret=3333)  

#### 方法：

GET

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
		<td>AppId</td>
		<td>true</td>
		<td>string</td>
		<td>申请应用时分配的AppId</td>
	  </tr>
	  <tr>
		<td>AppSecret</td>
		<td>true</td>
		<td>string</td>
		<td>申请应用时分配的AppSecret</td>
	  </tr>
	</tbody>
</table>


#### 返回值

	{
	  "Result": "611d2044535e97d72d1a3cbf7e4abda5",
	  "Code": 0,
	  "Life": 7200
	}

#### 其中： 
<table class="table table-bordered table-striped">
  <tbody>
	  <tr>
		<th>参数名</th>
		<th>含义</th>
	  </tr>
	  <tr>
		<td>Result</td>
		<td>为Token值。你不需要保存它。因为服务器已经帮你把这个值存在了Cookie里了。这里只是让你看到并确认，并方便传递。</td>
	  </tr>
	  <tr>
		<td>Code</td>
		<td>为代码。0表示正常。</td>
	  </tr>
	  <tr>
		<td>Life</td>
		<td>Life表示Token的生命长度，单位为秒。考虑到Token生存期随时可能更改，请根据Life判断Token是否过期，如果过期应及时更新</td>
	  </tr>
	</tbody>
</table>

#### 可能的返回值：
<table class="table table-bordered table-striped">
  <tbody>
	  <tr>
		<th>错误号</th>
		<th>含义</th>
	  </tr>
	  <tr>
		<td>0</td>
		<td>已经成功为你的Cookie写入Token</td>
	  </tr>
	  <tr>
		<td>-2</td>
		<td>已经达到了今日Token获取上限。不能再进行获取</td>
	  </tr>
	  <tr>
		<td>-4</td>
		<td>没有找到目标应用。应用的AppId或AppSecret错误</td>
	  </tr>
	</tbody>
</table>

### 检查Token是否过期  

开发者可以根据Cookie生存状态本地判断Token是否过期。本接口用于在开发过程中检查是否已经成功接入Token系统。

Productive级和Staging级App不应当调用本API

#### 地址：

>[/api/validatetoken](/api/validatetoken)   

#### 方法：GET  

#### 返回值：  
 
	{
		"Result":"OK!",
		"Code":0
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
		<td>本次请求携带了有效的Token</td>
	  </tr>
	  <tr>
		<td>-7</td>
		<td>Token无效或已超时</td>
	  </tr>
	  <tr>
		<td>-10</td>
		<td>请求没有携带Token</td>
	  </tr>
	</tbody>
</table>