# ArrayList类

## 1. 使用步骤

基本格式： 

```java
ArrayList<String> list = new ArrayList<String>();
```

简化格式： 

```java
ArrayList<String> list = new ArrayList<>();
```

## 2. 常用方法

对于元素的操作， 基本体现在——增、 删、 查。 常用的方法有： 

+ `public boolean add(E,e)` ： 将指定的元素添加到集合的尾部。 

+ `public E remove(int index)` ： 移除此集合中指定位置上的元素。 返回被删除的元素

+ `public E get(int index)` ： 返回此集合中指定位置上的元素。 返回获取的元素

+ `public int size() ` ： 返回此集合中的元素数。 遍历集合时， 可以控制索引范围， 防止越界

## 3. 如何存储基本数据类型

ArrayList 对象不能存储基本类型， 只能存储引用类型的数据。 类似 `<int>`  不能写， 但是存储基本数据类型对应的包装类型是可以的。 所以， 想要存储基本数据类型， <>中的数据类型， 必须转换后才能编写， 转换写法如下： 

| 基本数据类型 | 基本包装类型 |
|--------------|--------------|
| byte         | Byte         |
| short        | Short        |
| int          | Integer      |
| long         | Long         |
| float        | Float        |
| double       | Double       |
| char         | Character    |
| boolean      | Boolean      |
