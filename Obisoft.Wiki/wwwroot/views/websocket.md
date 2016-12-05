# WebScoket

#### 说明

服务器采用WebSocket进行主动事件推送。WebSocket工作在两种模式下
* 长连接客户端事件
* 长连接服务器事件

两种工作模式地址分别为：

#### 客户端事件

>wss://obisoft.com.cn/ws/ClientEvent

#### 服务器事件

>wss://obisoft.com.cn/ws/ServerEvent?Rel=Name

### 客户端事件

#### 说明

客户端事件工作模式和HTTP POST类似。客户端首先和WebSocket服务器建立连接。在客户端需要即时反馈的时候，直接向服务器发送数据，服务器会给出相应返回值。客户端事件中，不会有任何服务器主动发送的消息

#### 调试地址

>[/ws/ClientEvent](/ws/ClientEvent)

调试时，直接用浏览器打开调试地址即可。

#### 通用返回值

    WS echo from server:{输入值}

#### 代码示例 HTML部分

	<div id="spanStatus"></div>
	<textarea id="textInput">Message</textarea>
	<button type="button" id="btnSend">Send</button>

#### 代码示例 JavaScript部分

	var webSocket;
	webSocket = new WebSocket("wss://www.obisoft.com.cn/WS/ClientEvent");
	webSocket.onopen = function () {
		$("#spanStatus").text("connected");
	};
	webSocket.onmessage = function (evt) {
		$("#spanStatus").text(evt.data);
	};
	webSocket.onerror = function (evt) {
		alert(evt.message);
	};
	webSocket.onclose = function () {
		$("#spanStatus").text("disconnected");
	};
	$("#btnSend").click(function () {
		if (webSocket.readyState == WebSocket.OPEN) {
			webSocket.send($("#textInput").val());
		}
		else {
			$("#spanStatus").text("Connection is closed");
		}
	});

### 服务器事件

#### 说明

服务器事件需要客户端进行连接，之后客户端需要随时准备接收事件。服务器可能会在任意时刻返回任意内容。返回后连接不中断。

#### 服务器频率限制

服务器内部轮询侦听事件。对于单一客户端单一频道，最大延迟可达0.1秒。

为了降低服务器压力，两次推送最短间隔为250毫秒。因此在刚刚完成推送的250毫秒内服务器不会推送任何事件。这些事件会被直接丢失掉。

一般服务器事件不传递任何具体内容，仅仅表示一个通知。在收到服务器事件后，后续处理均使用HTTP通信完成。

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
		<td>Ref</td>
		<td>true</td>
		<td>string</td>
		<td>频道名</td>
	  </tr>
	</tbody>
</table>

服务器事件区分事件频道。例如消息频道仅推送消息事件，评论频道仅推送评论事件。这是为了避免一个频道中产生过多无用的信息

#### 调试地址

>[/ws/ServerEvent?ref=ref](/ws/ServerEvent?ref=ApiIndex)

#### 代码示例 Javascript

    var webSocket;
    $().ready(function () {
        webSocket = new WebSocket("wss://www.obisoft.com.cn/WS/ServerEvent?Ref=ApiIndex");
        webSocket.onopen = function () {
            $("#spanStatus").text("connected");
        };
        webSocket.onmessage = function (evt) {
            $("#spanStatus").text(evt.data);
        };
        webSocket.onerror = function (evt) {
            alert(evt.message);
        };
        webSocket.onclose = function () {
            $("#spanStatus").text("disconnected");
        };
    });

### Hello World API

#### 说明

本API仅用于开发者测试是否已经成功接入了服务器事件系统。

#### 类型

服务器事件

#### 频道

ApiIndex

#### 触发器

>[/api](/api)

每次收到访问，本API就会返回上次返回的时间。不会涉及历史访问。

#### 返回值

	WS Server Event:Index Viewd 9/9/2016 15:22:53

### 社区评论更新

#### 说明

在社区特定文章产生新评论时进行推送。

#### 类型

服务器事件

#### 频道

ArticleMessage+频道号码，例如：

>ArticleMessage256

#### 触发器

目标ID的社区文章每次收到评论，本API就会发出推送。

#### 返回值

	WS Server Event:GotNew

### 系统通知更新

#### 说明

系统通知更新，实时显示好友申请等。

#### 类型

服务器事件

#### 需要权限

已经登录

#### 频道

SystemMessage+URL编码后的用户邮箱，例如：

>SystemMessagemma%40obisoft.com.cn

#### 触发器

产生新的通知的时候会触发。

#### 返回值

	WS Server Event:GotNew
	
**警告：返回值不确定！尽GotNew代表新系统消息。未来随时可能会添加不同的返回值来标记不同的系统事件**
