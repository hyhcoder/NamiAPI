# Linux部署

----

### 下载
 * 若需要最新的版本,可以自己从github拉取并编译生成;
 * 或者[点击这里](https://pan.baidu.com/s/1bJmUtg#list/path=%2FNAMI)下载;(不定期更新)
 * 选择linux32/64位版本;
 
### 解压安装
 * 解压压缩包;
 * 然后chmod +x ./grant.sh;
 * 执行./grant.sh;
 * 对压缩包文件进行赋权;
 * 运行./server.sh start 把nami服务启动;

### 连接数据库
 * 更改~/conf中的jdbc.properties文件,连接数据库;
 * 若要更改tomcat端口, 可以更改~/appserver/CATALINA_BASE/conf/server.xml文件;(默认8080端口);

### 测试
 * 打开微信开发工具;
 * 新建一个无appid的quickstart项目;
 * 在app.js进行回调;
 * 回调的地址为: http://服务器地址:8080/request/hello.groovy; (正式上线需要换成https)
 * 进行打印输出测试;
 * 具体还可以看下这个视频,[开始第一个小程序.](http://mp.weixin.qq.com/s/229Ni6VOeLEkEaUH7CfWVg)