# 通知管理

### 查看我的所有通知

#### 说明

这将查看到发给我的所有系统通知。这包含已读的通知和未读的通知。但不包含用户已经阅读并执行过操作的通知。

**警告：有些通知，只要设为了已读，就会标记为用户已经执行操作。有些通知，必须用户进行了响应才会标记为已经操作。**

本API应当和WebSocket的`系统通知更新API`结合使用。也就是说，每当`系统通知更新API`推送了GotNew消息时，就应当调用本API刷新消息列表。

**警告：WebSocket API 中的服务器事件当且仅当返回GotNew时代表服务器事件。本API可能会返回其他值，请不要在这种情况下当作系统消息处理。**

#### 方法

GET

#### 地址

>[/api/AllMyMessages](https://www.obisoft.com.cn/api/AllMyMessages)

#### 需要权限

已经登录

#### 参数列表

无

#### 返回值

	{
		"Result": "Successfully get all your messages",
		"Code": 0,
		"Messages": [
			{
				"Accepted": false,
				"FromUserId": "ca0e279c-abc1-4745-b78c-e151cc957a17",
				"SystemMessageId": 32,
				"Read": false,
				"Operated": false,
				"MessageContent": "mmfa requires to be your friend.",
				"TargetUserId": "8d655227-d055-4448-9c78-4fbb637e5de8",
				"Discriminator": "FriendRequest",
				"CreateDate": "2016-09-16"
			},
			{
				"DoitFromUserId": "1be3d8b5-79e6-441b-95c5-04655028d1b0",
				"SystemMessageId": 33,
				"Read": false,
				"Operated": false,
				"MessageContent": "Your frinedxuefengxuefrom has remvoed your friend relation",
				"TargetUserId": "8d655227-d055-4448-9c78-4fbb637e5de8",
				"Discriminator": "RemoveFriendRequest",
				"CreateDate": "2016-09-16"
			},
			{
				"CoFromUserId": "1be3d8b5-79e6-441b-95c5-04655028d1b0",
				"SystemMessageId": 34,
				"Read": false,
				"Operated": false,
				"MessageContent": "你有一条新留言",
				"TargetUserId": "8d655227-d055-4448-9c78-4fbb637e5de8",
				"Discriminator": "CommunityPushMessage",
				"CreateDate": "2016-09-16"
			}
		]
	}

# 目前支持的消息类型 

### 好友请求

#### 触发器

当有其它用户申请添加当前用户为好友时，触发本请求

#### 示例

	{
		"Accepted": false,
		"FromUserId": "ca0e279c-abc1-4745-b78c-e151cc957a17",
		"SystemMessageId": 32,
		"Read": false,
		"Operated": false,
		"MessageContent": "mmfa requires to be your friend.",
		"TargetUserId": "8d655227-d055-4448-9c78-4fbb637e5de8",
		"Discriminator": "FriendRequest",
		"CreateDate": "2016-09-16"
	}


### 社区留言

#### 触发器

当有其它用户在当然用户的博客主页留言时，触发本请求

#### 示例

	{
		"CoFromUserId": "1be3d8b5-79e6-441b-95c5-04655028d1b0",
		"SystemMessageId": 34,
		"Read": false,
		"Operated": false,
		"MessageContent": "你有一条新留言",
		"TargetUserId": "8d655227-d055-4448-9c78-4fbb637e5de8",
		"Discriminator": "CommunityPushMessage",
		"CreateDate": "2016-09-16"
	}

### 删除好友通知

#### 触发器

当有其它用户在好友列表中删除了当前用户时触发

#### 示例

	{
		"DoitFromUserId": "1be3d8b5-79e6-441b-95c5-04655028d1b0",
		"SystemMessageId": 33,
		"Read": false,
		"Operated": false,
		"MessageContent": "Your frinedxuefengxuefrom has remvoed your friend relation",
		"TargetUserId": "8d655227-d055-4448-9c78-4fbb637e5de8",
		"Discriminator": "RemoveFriendRequest",
		"CreateDate": "2016-09-16"
	}

### 区分

所有消息中都包含一些基本属性，如SystemMessageId、Read、Operated、MessageContent、TargetUserId、CreateDate。

还有一些特有属性：Accepted、FromUserId、DoitFromUserId、CoFromUserId。

具体可以直接观察返回值示例。

其中有一个最特殊的属性：Discriminator。它用于区分当前消息是哪种类型。


### 将特定通知设置为已读

#### 说明

所有通知都有是否已读选项。如果通知已读，就不应该继续使用一些小红点来提醒用户

#### 需要权限

已经登录

#### 地址

>[/api/SetSystemMessageRead](https://www.obisoft.com.cn/api/SetSystemMessageRead)

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
		<td>MessageId</td>
		<td>true</td>
		<td>int</td>
		<td>目标消息的ID</td>
	  </tr>
	</tbody>
</table>

#### 返回值

	{
	  "Result": "Message Read!",
	  "Code": 0
	}

#### 可能的返回值

<table class="table table-bordered table-striped">
  <tbody>
	  <tr>
		<th>错误号</th>
		<th>含义</th>
	  </tr>
	  <tr>
		<td>0</td>
		<td>设置成功</td>
	  </tr>
	  <tr>
		<td>-4</td>
		<td>等待进行第二步认证</td>
	  </tr>
	  <tr>
		<td>-6</td>
		<td>消息已经设置成了已读</td>
	  </tr>
	</tbody>
</table>