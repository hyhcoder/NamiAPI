# Windows部署使用Nami

----

### 下载
 * 若需要最新的版本,可以自己从github拉取并编译生成;
 * 或者[点击这里](https://pan.baidu.com/s/1bJmUtg#list/path=%2FNAMI)下载;(不定期更新)
 * 选择Win32/64位版本;
 
### 解压安装
 * 下载安装包直接解压到任意位置
 * 解压后有以下目录
	
		appserver：内置的tomcat，未来可能还会放入jdk，开发者不用关注
		conf：配置文件，包括小程序appid，数据库连接等都配置在这里
		database：内置的h2文件数据库，开发者不用关注
		request：自定义request请求的脚本代码
		websocket：自定义websocket的脚本代码
		function：业务函数逻辑代码
		download：提供给客户端下载的资源
		resource：客户端上传的资源（图片，视频，语言等）的默认保存位置
		log：日志
		nami：NAMI内核包的位置，开发者不用关注

 * 直接双击start.bat即可启动内置tomcat。


### 更改配置
 * 更改数据库配置

		打开nami包下的conf文件夹,修改jdbc.properties可更改数据库连接	
		(默认连接H2数据库)


 * 修改Tomcat端口
 
		打开nami包下\appserver\CATALINA_BASE\conf文件夹,修改server.xml文件
		(默认8080端口);

### 测试
 * 打开微信开发工具;
 * 新建一个无appid的quickstart项目;
 * 在app.js进行回调;
 * 回调的地址为: http://服务器地址:8080/request/hello.groovy; (正式上线需要换成https)
 * 进行打印输出测试;
 * 具体还可以看下这个视频,[开始第一个小程序.](http://mp.weixin.qq.com/s/229Ni6VOeLEkEaUH7CfWVg)