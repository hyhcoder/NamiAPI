# db
db函数库提供的数据库操作类的函数

## find
根据sql查询唯一值

#### 参数API
| 序号   | 参数类型 | 说明                                                                                                                     |
|--------|----------|--------------------------------------------------------------------------------------------------------------------------|
| 1      | 字符串   | SQL串（可用问号代替入参）。                                                                                              |
| 2...N  | 无限制   | 问号替换参数（比如db.find("select * from BS_CUSTOMER where CUSTOMER_ID = ? and ADDRESS like ?", "CUS001", "%11号%");）。 |
| 返回值 | 对象     | 对象Map                                                                                                                  |
#### 示例1：
		//返回对象超过一个会报错
		db.find("select * from BS_CUSTOMER");
#### 示例2：

		db.find("select * from BS_CUSTOMER where CUSTOMER_ID = ?", "CUS001");
## query
根据sql查询列表

#### 参数API
| 序号   | 参数类型 | 说明                                                                                                                     |
|--------|----------|--------------------------------------------------------------------------------------------------------------------------|
| 1      | 字符串   | SQL串（可用问号代替入参）。                                                                                              |
| 2...N  | 无限制   | 问号替换参数（比如db.query("select * from BS_CUSTOMER where ADDRESS like ?", "%广州%");）。 |
| 返回值 | 对象     | 对象Map                                                                                                                  |
#### 示例1：

		db.query("select * from BS_CUSTOMER");

#### 示例2：
		
		db.query("select * from BS_CUSTOMER where BUSI_NAME like ?", "%广州%");


## exec
执行sql语句
#### 参考API
| 序号   | 参数类型 | 说明                        |
|--------|----------|-----------------------------|
| 1      | 字符串   | SQL串（可用问号代替入参）。 |
| 2...N  | 无限制   | 参考db.find和db.query       |
| 返回值 | 无       | 无                          |

#### 示例1：

		db.exec("insert into BS_CUSTOMER (CUSTOMER_ID, BUSI_NAME, ADDRESS, CREATE_OPR, CREATE_DATE)values(?, ?, ?, ?, ?)",
		    "CUS005",
		    "广州新欣科技有限公司",
		    "广州市天河软件园建设路5号",
		    user.user.uid,
		    now
		);