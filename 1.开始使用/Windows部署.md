# Windows部署使用Nami

----

### 下载
 * 若需要最新的版本,可以自己从github拉取并编译生成;
 * 或者[点击这里](https://pan.baidu.com/s/1bJmUtg#list/path=%2FNAMI)下载;(不定期更新)
 * 选择Win32/64位版本;
 
### 解压安装
 * 下载安装包直接解压到任意位置
 * 直接双击start.bat即可启动内置tomcat。

### 更改配置
 * 更改数据库配置
```
打开nami包下的conf文件夹,修改jdbc.properties可更改数据库连接	
(默认连接H2数据库)
```

 * 修改Tomcat端口
``` 
打开nami包下\appserver\CATALINA_BASE\conf文件夹,修改server.xml文件
(默认8080端口);
```

### 测试
 * 打开微信开发工具;
 * 新建一个无appid的quickstart项目;
 * 在app.js进行回调;
 * 回调的地址为: http://服务器地址:8080/request/hello.groovy; (正式上线需要换成https)
 * 进行打印输出测试;
 * 具体还可以看下这个视频,[开始第一个小程序.](http://mp.weixin.qq.com/s/229Ni6VOeLEkEaUH7CfWVg)