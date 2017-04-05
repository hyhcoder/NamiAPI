#date 日期操作处理
date函数库提供各种日期处理的函数

## compare
计算两个时间之间的差值
### 参数API
| 序号   	|  参数类型  	|                 说明                 	|
|--------	|:----------:	|:------------------------------------:	|
|    1   	| Date日期 	| 入参一个想要比较的第一个日期 	|
| 2 	|    Date日期    	|             入参一个想要比较的第二个日期             	|
| 3 	|    字符串(可选)    	|             可选,默认差值为天;可以选择入参选择年月日时分等;如年:"Y"/"y";  月:"M";  天:"D"/"d"(默认); 小时:"H"/"h"; 分:"m"; 秒:"s"; 毫秒:"S";             	|
| 返回值 	|    长整数    	|             返回相应的差值,正或负             	|

#### 示例1 : 对比2015/02/03和2014/05/03之间相差的天数
```java
Calendar now = Calendar.getInstance();
now.set(Calendar.YEAR, 2015);
now.set(Calendar.MONTH, 2);
now.set(Calendar.DAY_OF_MONTH, 3);

Calendar before = Calendar.getInstance();
before.set(Calendar.YEAR, 2014);
before.set(Calendar.MONTH, 5);
before.set(Calendar.DAY_OF_MONTH, 3);
		
return date.compare(before.getTime(),now.getTime());
```
#### 示例2 : 对比2015/02/03和2014/05/03之间相差的月数
```java
Calendar now = Calendar.getInstance();
now.set(Calendar.YEAR, 2015);
now.set(Calendar.MONTH, 2);
now.set(Calendar.DAY_OF_MONTH, 3);

Calendar before = Calendar.getInstance();
before.set(Calendar.YEAR, 2014);
before.set(Calendar.MONTH, 5);
before.set(Calendar.DAY_OF_MONTH, 3);
		
return date.compare(before.getTime(),now.getTime(),"M");
```

## diffYear / diffMonth
计算两个日期相差的年份 / 月份
### 参数API
| 序号   | 参数类型 | 说明                         |
|--------|----------|------------------------------|
| 1      | Date日期 | 入参一个想要比较的第一个日期 |
| 2      | Date日期 | 入参一个想要比较的第二个日期 |
| 返回值 | 长整数   | 返回相差的年份 / 月份               |

#### 示例 1: 对比2015/02/03和2005/05/03之间相差的年份
```java
Calendar now = Calendar.getInstance();
now.set(Calendar.YEAR, 2015);
now.set(Calendar.MONTH, 2);
now.set(Calendar.DAY_OF_MONTH, 3);
	
Calendar before = Calendar.getInstance();
before.set(Calendar.YEAR, 2005);
before.set(Calendar.MONTH, 5);
before.set(Calendar.DAY_OF_MONTH, 3);
		
return date.diffYear(now.getTime(),before.getTime());
```
#### 示例 2: 对比2015/02/03和2005/05/03之间相差的月份
```java
Calendar now = Calendar.getInstance();
now.set(Calendar.YEAR, 2015);
now.set(Calendar.MONTH, 2);
now.set(Calendar.DAY_OF_MONTH, 3);
		
Calendar before = Calendar.getInstance();
before.set(Calendar.YEAR, 2005);
before.set(Calendar.MONTH, 5);
before.set(Calendar.DAY_OF_MONTH, 3);
		
return date.diffMonth(now.getTime(),before.getTime());
```

## cal
计算日期加减
### 参数API
| 序号   | 参数类型     | 说明                                                                                                                           |
|--------|--------------|--------------------------------------------------------------------------------------------------------------------------------|
| 1      | Date日期     | 输入待计算的日期                                                                                                               |
| 2      | 整数         | 对日期的操作数,正数为加,负数为减                                                                                               |
| 3      | 字符串(可选) | 操作数的单位,可选,可以选择入参选择年月日时分等;如年:"Y"/"y"; 月:"M"; 天:"D"/"d"(默认); 小时:"H"/"h"; 分:"m"; 秒:"s"; 毫秒:"S"; |
| 返回值 | Date日期         | 返回计算过后的日期                                                                                                             |
#### 示例 1:对日期2015/02/03 进行加10天计算
```java
Calendar now = Calendar.getInstance();
now.set(Calendar.YEAR, 2015);
now.set(Calendar.MONTH, 2);
now.set(Calendar.DAY_OF_MONTH, 3);
		
return date.cal(now.getTime(),10);
```
#### 示例 2:对日期2015/02/03 进行加两年计算
```java
Calendar now = Calendar.getInstance();
now.set(Calendar.YEAR, 2015);
now.set(Calendar.MONTH, 2);
now.set(Calendar.DAY_OF_MONTH, 3);
		
return date.cal(now.getTime(),2,"Y");
```