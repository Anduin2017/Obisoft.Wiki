# 用户关系管理

### 查看我的所有好友

#### 说明

本API将会列出所有已经同意了好友请求的用户列表

#### 需要权限

已经登录

#### 地址

>[/api/MyFriends](/api/MyFriends)

#### 方法

GET

#### 参数列表

无

#### 返回值

	{
		"Result": "Successfully Get Friends List.",
		"Friends": [
			{
				"FriendRelationId": 2,
				"MeId": "8d655227-d055-4448-9c78-4fbb637e5de8",
				"TargetUserId": "ca0e279c-abc1-4745-b78c-e151cc957a17",
				"UserNickName": "mmfa",
				"UserDes": "Nothing to say",
				"UserIcon": "https://www.gravatar.com/avatar/5e4770506f2399736f5db92ed61eca41.png?s=160&d=https%3A%2F%2Fobisoft.oss-cn-beijing.aliyuncs.com%2FWebSiteIcon%2FIcon.jpg"
			},
			{
				"FriendRelationId": 3,
				"MeId": "8d655227-d055-4448-9c78-4fbb637e5de8",
				"TargetUserId": "1be3d8b5-79e6-441b-95c5-04655028d1b0",
				"UserNickName": "xuefengxuefrom",
				"UserDes": "Nothing to say",
				"UserIcon": "https://www.gravatar.com/avatar/92e6e7e91f33ede0ef06c969480b043d.png?s=160&d=https%3A%2F%2Fobisoft.oss-cn-beijing.aliyuncs.com%2FWebSiteIcon%2FIcon.jpg"
			},
			{
				"FriendRelationId": 5,
				"MeId": "8d655227-d055-4448-9c78-4fbb637e5de8",
				"TargetUserId": "6ff66994-f5b0-40f9-8aa0-1c2e81d43c5d",
				"UserNickName": "hkyla",
				"UserDes": "Nothing to say",
				"UserIcon": "https://www.gravatar.com/avatar/e569e15c997a006a9f422bcf99c4fdee.png?s=160&d=https%3A%2F%2Fobisoft.oss-cn-beijing.aliyuncs.com%2FWebSiteIcon%2FIcon.jpg"
			},
			{
				"FriendRelationId": 8,
				"MeId": "8d655227-d055-4448-9c78-4fbb637e5de8",
				"TargetUserId": "1d097302-42d6-49a9-9241-c1f3b49a86f0",
				"UserNickName": "1256618728",
				"UserDes": "Nothing to say",
				"UserIcon": "https://www.gravatar.com/avatar/13d42d61a3f9ee70e46a318bdad98007.png?s=160&d=https%3A%2F%2Fobisoft.oss-cn-beijing.aliyuncs.com%2FWebSiteIcon%2FIcon.jpg"
			},
			{
				"FriendRelationId": 9,
				"MeId": "8d655227-d055-4448-9c78-4fbb637e5de8",
				"TargetUserId": "7b42520a-fe1d-4a75-87a7-384b91b62140",
				"UserNickName": "mmfza",
				"UserDes": "Nothing to say",
				"UserIcon": "https://www.gravatar.com/avatar/c28e23e25776872851b34f1fa9868762.png?s=160&d=https%3A%2F%2Fobisoft.oss-cn-beijing.aliyuncs.com%2FWebSiteIcon%2FIcon.jpg"
			}
		],
		"Code": 0
	}

### 创建好友申请

#### 说明

本API会新建一个好友申请，并发送给目标用户。好友申请属于一种通知，可以通过通知管理API进行管理。

#### 需要权限

已经登录，且目标用户不是你的好友，且目标用户已经处理了所有和你的关系请求

#### 地址

>[/api/CreateFriendRequest](/api/CreateFriendRequest)

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
		<td>TargetUserId</td>
		<td>true</td>
		<td>string</td>
		<td>目标用户ID</td>
	  </tr>
	</tbody>
</table>

#### 返回值

	{
	  "Result": "Friend request sent",
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
		<td>已经成功创建了好友申请</td>
	  </tr>
	  <tr>
		<td>-4</td>
		<td>没有找到目标用户</td>
	  </tr>
	  <tr>
		<td>-6</td>
		<td>你们已经是好友了。</td>
	  </tr>
	  <tr>
		<td>-7</td>
		<td>你们之间没有未处理的好友请求。</td>
	  </tr>
	  <tr>
		<td>-8</td>
		<td>不允许自己申请加自己为好友。</td>
	  </tr>
	</tbody>
</table>

### 处理一个好友请求

#### 说明

当其它用户向当前用户发送了好友申请后，在这里通过好友申请，或拒绝好友申请。如果好友申请没有被阅读，它会被设置为已读，同时设置为已执行操作。

#### 需要权限

已经登录

#### 地址

>[/api/OperateFriendRequest](/api/OperateFriendRequest)

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
		<td>string</td>
		<td>目标好友申请ID</td>
	  </tr>
	  <tr>
		<td>Accepted</td>
		<td>true</td>
		<td>bool</td>
		<td>是否接受好友请求。若为true，则会添加好友关系。若为false，则拒绝。</td>
	  </tr>
	</tbody>
</table>


#### 可能的返回值

<table class="table table-bordered table-striped">
  <tbody>
	  <tr>
		<th>错误号</th>
		<th>含义</th>
	  </tr>
	  <tr>
		<td>0</td>
		<td>已经成功处理了好友申请</td>
	  </tr>
	  <tr>
		<td>-4</td>
		<td>没有找到目标好友请求</td>
	  </tr>
	  <tr>
		<td>-6</td>
		<td>好友请求已经被处理过了。</td>
	  </tr>
	  <tr>
		<td>-7</td>
		<td>你们已经是好友了。</td>
	  </tr>
	</tbody>
</table>

### 删除好友关系

#### 说明

删除好友关系，不需要任何申请，会直接删除双向的好友关系

#### 需要权限

已经登录，且你们已经是好友

#### 地址 

>[/api/RemoveFriend](/api/RemoveFriend)

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
		<td>TargetUserId</td>
		<td>true</td>
		<td>string</td>
		<td>目标好友ID</td>
	  </tr>
	</tbody>
</table>

#### 返回值

**待更新**

#### 可能的返回值

<table class="table table-bordered table-striped">
  <tbody>
	  <tr>
		<th>错误号</th>
		<th>含义</th>
	  </tr>
	  <tr>
		<td>0</td>
		<td>已经成功处理了好友申请</td>
	  </tr>
	  <tr>
		<td>-7</td>
		<td>你们并没有成为好友</td>
	  </tr>
	</tbody>
</table>