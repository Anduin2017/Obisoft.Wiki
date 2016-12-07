# 基本功能接口

### 修改API返回的语言

#### 说明

部分API支持国际化接口。我们将在正式上线后实现全部API的国际化接口。实现了国际化接口的API能够实现由服务器控制用户交互的提示语，客户端只需要将信息展示即可。

本API不需要Token即可调用。

#### 原理

本API会修改Cookie，设置倾向的语言选项。开发者务必保留这个Cookie

#### 地址

>[/api/ChangeLanguage](https://www.obisoft.com.cn/api/ChangeLanguage)

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
		<td>culture</td>
		<td>false</td>
		<td>Culture</td>
		<td>i18N标准文化代码，例如简体中文：zh-CN，英文美国：en-US，日语日本ja-JP。若不传则为en-US</td>
	  </tr>
	</tbody>
</table>

#### 返回值

	{
	  "Result": "Changed",
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
		<td>-1</td>
		<td>输入的语言不是合法的语言格式。</td>
	  </tr>
	  <tr>
		<td>0</td>
		<td>语言已经应用</td>
	  </tr>
	</tbody>
</table>