# String类

## 特点

1. 字符串不变： 字符串的值在创建后不能更改。 

```java
String s1 = "abc";
s1 += "d";
System.out.println(s1);// "abcd"
//内存中有"abc"，"abcd"两个对象，s1从指向"abc",改变指向了"abcd"。

```

2. 因为String对象是不可变的， 所以他们可以被共享。 

3. ` "abc" ` 等效于 ` char[] data = {'a' , 'b' , 'c'} ` 。 

## 常用方法

### 判断功能的方法

+ `public boolean equals(Object anObject)` ： 将此字符串与指定对象进行比较。 

+ `public boolean equalsIgnoreCase (String anotherString)` ： 将此字符串与指定对象进行比较， 忽略大小写。 

### 获取功能的方法

+ `public int length ()` ： 返回此字符串的长度。 

+ `public String concat (String str)` ： 将指定的字符串连接到该字符串的末尾。 

+ `public char charAt (int index)` ： 返回指定索引处的char值。 

+ `public int indexOf (String str)` : 返回指定子字符串第一次出现在该字符串内的索引。 

+ `public String substring (int beginIndex)` ： 返回一个子字符串， 从beginIndex开始截取字符串到字符

串结尾。 

+ `public String substring (int beginIndex, int endIndex)` ： 返回一个子字符串， 从beginIndex到endIndex截取字符串。含beginIndex，不含endIndex。 

### 转换功能的方法

+ `public char[] toCharArray ()` ： 将此字符串转换为新的字符数组。 

+ `public byte[] getBytes ()` ： 使用平台的默认字符集将该 String编码转换为新的字节数组。 

+ `public String replace (CharSequence target, CharSequence replacement)` ： 将与target匹配的字符串使

用replacement字符串替换。 

### 分割功能的方法

+ `public String[] split(String regex)` ： 将此字符串按照给定的regex（规则）拆分为字符串数组。 

