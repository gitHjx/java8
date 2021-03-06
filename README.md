# lambda表达式
## 一、lambda概述：
     lambda表示数学符号"λ"，计算机领域中λ代表"λ演算"，表达了计算机中最基本的概念： "调用"和"转换"。
## 二、为什么使用lambda
      1.Java是面向对象的语言，不能像函数式语言那样嵌套定义方法。
      2.Java的匿名内部类只能存在于创建它的线程中，不能运行在多线程中，无法充分利用多核的硬件优势。
      3.匿名内部类的缺点还有：
          3.1 语法相对复杂。
          3.2 在调用内部类的上下文中，指引和this的指代空易混淆。
          3.3 类加载和实例创建语法不可避免。
          3.4 不能引用外部的非final对象。
          3.5 不能抽象化控制流程。
## 三、lambda的语法包括三部分：
       1. 参数列表
       2. 箭头符号"->"
       3. 代码块。
       
# Stream接口
## 一、什么是Stream
  	1. Stream在Java8中被定义为泛型接口
 	2. Stream接口代表数据流：此数据流并非我们所熟知的I/O流
  	3. Stream不是一个数据结构，不直接存储数据。
  	4. Stream通过管道操作数据。
 	5. 创建Stream接口实现类对象：
  		stream():创建一个Stream接口实现类的对象。
  	例如：
  		Stream<Person> stream = people.stream();
  		其中people是一个ArrayList集合，调用其中的stream()方法，返回一个Stream对象
 
## 二、 什么是管道
 	1. 管道：代表一个操作序列。
 	2. 管道包含以下组件：
 		a. 数据集：可能是集合、数组等。
 		b. 零个或多个中间业务。如过滤器
 		c. 一个终端操作，如forEach
## 三、什么是过滤器
 	1. 过滤器：用给定的条件在源数据基础上过滤出新的数据，并返回一个Stream对象。
 	2. 过滤器包含匹配的谓词。
 		例如：判断p对象是否为男性的lambda表达式：
 			Stream<Person> stream = people.stream();
 			stream = stream.filter(p->p.getGender() == '男');
 			
 			
 			
 			
 			
# 【过滤器案例】
	过滤出集合中名字含有“菲”字的Person对象
	
	
# DoubleStream接口
## 一、DoubleStream接口表示元素类型是double的数据源。
## 二、DoubleStream接口的常用方法：
	1. stream.max().getAsDouble():获取流中数据集的最大值。
	2. stream.min.getAsDouble():获取流中数据集的最小值。
	3. stream.average():获取流中数据集的平均值。
	
## 【案例】统计people集合中姓名中包含“菲”字的平均身高。


# LocalDate类
# 一、概述
   1. LocalDate类使用ISO日历表示年、月、日。
   2. ISO日历是国际标准化组织用来表示日期的标准格式法
# 二、常用方法
1. LocalDate.now()：获取系统当前日期。
2. LocalDate.of(int year, int month, int dayOfMonth)
 按指定日期创建LocalDate对象。
3. getYear():返回日期中的年份，返回值为int类型。
4. getMonth():返回日期中的月份，返回值为int类型。
5. getDayOfMonth():返回月份中的日，返回值为int类型。

# 【案例】：获取当前系统时间

测试代码如下：
```
public class Test06_localDate {

	public static void main(String[] args) {
		
		/**
		 * java8前
		 */
		Calendar calendar = Calendar.getInstance();
		calendar.setTime(new Date());
		int year = calendar.get(Calendar.YEAR);
		int month = calendar.get(Calendar.MONTH);
		int day = calendar.get(Calendar.DAY_OF_MONTH);
		System.out.println("java8前的Calendar类:"+year+"-"+month+"-"+day);
		
		/**
		 * java8后
		 */
		LocalDate date = LocalDate.now();
		year = date.getYear();
		month = date.getMonthValue();
		day = date.getDayOfMonth();
		System.out.println("java8的LocalDate类:"+year+"-"+month+"-"+day);
		System.out.println("java8的LocalDate类的toString方法："+date);
		
		/**
		 *  java8前获取的月份从0开始，java8的LocalDate获取的月份从1开始
		 */
	}

}

```

运行以上代码，控制台打印输出结果如下：
```
java8前的Calendar类:2018-7-16
java8的LocalDate类:2018-8-16
java8的LocalDate类的toString方法：2018-08-16
```
 从以上运行结果可知：java8前的Calendar类输出的月份是从0开始，总是比实际月份小1个月，而java8的LocalDate类月份是从1开始的
 
 
# LocalTime类

# 一、概述
   1. LocalTime类表示一天中的时间
# 二、常用方法
1. LocalTime.now(): 静态方法，获取系统当前时间。
2. LocalTime.of(int hour, int minute, int second)
	按指定时间创建LocalTime对象。
3. getHour():返回小时.
4. getMinute():返回分钟。
5. getSecond():返回秒。

# 【案例】用LocalTime获取当前时间

测试代码如下：
```
public class Test07_localTime {

	/**
	 * 【案例】用LocalTime获取当前时间
	 * @param args
	 */
	public static void main(String[] args) {
		
		
		/**
		 * java8前的Calendar
		 */
		Calendar calendar = Calendar.getInstance();
		calendar.setTime(new Date());
		int hour = calendar.get(Calendar.HOUR);
		int minute = calendar.get(Calendar.MINUTE);
		int second = calendar.get(Calendar.SECOND);
		System.out.println("java8前的Calendar类:"+hour+":"+minute+":"+second);
		
		
		
		
		/**
		 * java8的 LocalTime类
		 */
		LocalTime localTime = LocalTime.now();
		hour = localTime.getHour();
		minute = localTime.getMinute();
		second = localTime.getSecond();
		System.out.println("java8的LocalTime类:"+hour+":"+minute+":"+second);
		System.out.println("LocalTime的toString方法："+localTime.toString());
		
		LocalTime localTime2 = localTime.of(12, 12,12);//指定时间
		hour = localTime2.getHour();
		minute = localTime2.getMinute();
		second = localTime2.getSecond();
		System.out.println("指定时间的LocalTime:"+hour+":"+minute+":"+second);
		System.out.println(localTime2.toString());
		
	}
	
}


```

运行以上代码，控制台打印输出结果如下：
```
java8前的Calendar类:11:34:6
java8的LocalTime类:23:34:6
LocalTime的toString方法：23:34:06.609
指定时间的LocalTime:12:12:12
12:12:12

```

# LocalDateTime类
 ----
# 一、概述
   LocalDateTime类用于表示日期和时间。
# 二、常用方法
  1. LocalDateTime.now()：获取系统当前时间。
  2. LocalDateTime.of(int year,int month,int dayOfMonth,int hour,int minute,int second):按指定日期和时间创建LocalDateTime对象。
  3. getYear():返回日期中的年份。
  4. getMonth():返回日期中的月份。
  5. getDayOfMonth():返回月份中的日。
  6. getHour():返回小时。
  7. getMinute():返回分钟.
  8. getSecond():返回秒。

# 【案例】 用LocalDateTime获取当前日期和时间。

测试代码如下：
```
public class Test08_localDateTime {
	
	public static void main(String[] args) {
		/**
		 * 【案例】 用LocalDateTime获取当前日期和时间。
		 */
		
		LocalDateTime dateTime = LocalDateTime.now();
		int year = dateTime.getYear();
		int month = dateTime.getMonthValue();
		int day = dateTime.getDayOfMonth();
		int hour = dateTime.getHour();
		int minute = dateTime.getMinute();
		int second = dateTime.getSecond();
		System.out.println("java8LocalDateTime类:"+year+"年"+month+"月"+day+"日 "+hour+":"+minute+":"+second);
		System.out.println("java8LocalDateTime类的toString:"+dateTime);
		
	}

}


```

运行以上代码，控制台打印输出结果如下：
```
java8LocalDateTime类:2018年8月18日 22:27:13
java8LocalDateTime类的toString:2018-08-18T22:27:13.906
```
# DateTimeFormatter类
 ---
# 一、概述
  DateTimeFormatter类用于将字符串解析为日期对象
# 二、常用方法
  1. static ofPattern(String pattern):静态方法，根据指定的字符串设定的格式，将返回一个DateTimeFormatter对象。
  2. LocalDateTime.parse(strDate,formatter);静态方法，此方法将指定的字符串strDate,按DateTimeFormatter对象的字符串格式解析为一个LocalDateTime对象。
  3. format(formatter):此方法属于LocalDateTime类的方法。用于将LocalDateTime对象按照DateTimeFormatter指定的格式，转换为一个字符串对象。

# 【案例】将字符串"2018-08-18 22:30:22"解析为一个LocalDateTime对象
测试代码如下：
```
public class Test09_dateTimeFormatter {
	/**
	 * 【案例】将字符串"2018-08-18 22:30:22"解析为一个LocalDateTime对象
	 * @param args
	 */
	public static void main(String[] args) {
		
		DateTimeFormatter formatter =
						DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
		//将字符串按照DateTimeFormatter对象指定的格式解析为LocalDateTime对象
		LocalDateTime date = LocalDateTime.parse("2018-08-18 22:30:22", formatter);
		System.out.println(date.toString());
		
		//将LocalDateTime对象按照DateTimeFormatter指定的格式转换为字符串输出
		formatter = DateTimeFormatter.ofPattern("yyyy/MM/dd_HH/mm/ss");
		String str = date.format(formatter);
		System.out.println(str);
		
	}

}


```
运行以上代码，控制台打印输出结果如下：
```
2018-08-18T22:30:22
2018/08/18_22/30/22
```


- Java8新增的DateTimeFormatter与SimpleDateFormat最大区别是:Java8的DateTimeFormatter是线程安全的，而SimpleDateFormat不是线程安全。


# ZonedDateTime类
 ---
# 一、概述
  ZonedDateTime处理日期和时间与相应的时区
# 二、常用方法
  1. ZonedDateTime.now()：获取系统当前日期和时间。
  2. String format(DateTimeFormatter formatter):
    根据DateTimeFormatter对象设置的格式将日期转换为一个字符串
  3. plusDays(int days); 加上指定的天数，
# 【案例】将当前日期格式化为字符串并显示年、月、日、时、分和秒。

测试代码如下：
~~~
public class Test10_zonedDateTime {
	/**
	 * 【案例】将当前日期格式化为字符串并显示年、月、日、时、分和秒。
	 * 
	 */
	public static void main(String[] args) {
		ZonedDateTime now = ZonedDateTime.now();
		DateTimeFormatter formatter = DateTimeFormatter.ofPattern("MM/dd/yy HH:mm:ss");
		String strDate = now.format(formatter);
		System.out.println("format方法返回的字符串："+strDate);
		now = now.plusDays(1);//当前日期 加上1天
		String strDate2 = now.format(formatter);
		System.out.println("加上一天后的日期："+strDate2);
	}
}

~~~

运行上述代码控制台打印结果如下：
~~~
format方法返回的字符串：08/19/18 23:05:40
加上一天后的日期：08/20/18 23:05:40
~~~



	 