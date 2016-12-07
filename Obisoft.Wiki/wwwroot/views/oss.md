# 对象存储

Obisoft对象存储用于保存不存在数据库中的数据，包括文件，例如：照片、视频、音乐等。

Obisoft对象存储服务目前对所有用户公开免费开放使用。目前只允许上传8MB以内文件。

### 上传一个文件

#### 说明

这将会向目标服务器上传一个文件并得到它在web上的路径

#### 地址  
>[https://oss.obisoft.com.cn/](https://oss.obisoft.com.cn/)

#### 调试地址
>[https://oss.obisoft.com.cn/](https://oss.obisoft.com.cn/)

直接在浏览器中打开即可预览对象存储的使用

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
		<td>token</td>
		<td>true</td>
		<td>string</td>
		<td>Obisoft Access Token</td>
	  </tr>
	</tbody>
</table>

#### 返回值:
 
    {
        "path":"https://oss.obisoft.com.cn/38c0237b58cd5f995a63e7eafe61106cac4c3529718ff0b7077aa33551d2d24e.jpg",
        "code":0
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
		<td>上传成功</td>
	  </tr>
	  <tr>
		<td>-1</td>
		<td>文件过大而无法上传</td>
	  </tr>
	  <tr>
		<td>-10</td>
		<td>没有携带有效的AppId和AppSecret</td>
	  </tr>
	  <tr>
		<td>-5</td>
		<td>对象存储服务异常</td>
	  </tr>
	</tbody>
</table>

#### 例如:

    { 
        "Result" : "Error with your appid or appsecret", 
        "Code" = -10 
    }

**对象存储目前还在更新，即将增加‘删除文件’、‘创建文件夹等功能’**