# Objcect类

## 概述

`java.lang.Object` 类是Java语言中的根类，即所有类的父类。它中描述的所有方法子类都可以使用。在对象实例化的时候，最终找的父类就是Object。
如果一个类没有特别指定父类， 那么默认则继承自Object类。

## toString方法

### 方法摘要

+ `public String toString()`：返回该对象的字符串表现形式。

toString方法返回该对象的字符串表示，其实该字符串内容就是对象的类型+@+内存地址值。

### 覆盖重写

```java
public class Person {
    private String name;
    private int age;
    @Override
    public String toString() {
        return "Person{" + "name='" + name + '\'' + ", age=" + age + '}';
    }

    // 省略构造器与Getter Setter

}
```
> tips:alt+insert ，点击 toString() 选项。选择需要包含的成员变量并确定。

## equals方法

### 方法摘要

+ `public boolean equals(Object obj)`：表示其他某个对象是否与此对象“相等”。

### 默认地址比较

如果没有覆盖重写equals方法，那么Object类中默认进行 == 运算符的对象地址比较，只要不是同一个对象，结果必然为false。

### 对象内容比较

如果希望进行对象的内容比较，即所有或指定的部分成员变量相同就判定两个对象相同，则可以覆盖重写equals方法。例如：

```java
import java.util.Objects;

public class Person {
    private String name;
    private int age;
    @Override
    public boolean equals(Object o) {
        // 如果对象地址一样，则认为相同
        if (this == o)  return true;
        // 如果参数为空，或者类型信息不一样，则认为不同
        if (o == null || getClass() != o.getClass())    return false;
        // 转换为当前类型
        Person person = (Person) o;
        // 要求基本类型相等，并且将引用类型交给java.util.Objects类的equals静态方法取用结果
        return age == person.age && Objects.equals(name, person.name);
    }
}

```
> tips:alt+insert ，并选择equals() and hashCode() 进行自动代码生成。


## Objects类

### equals方法
在比较两个对象的时候，Object的equals方法容易抛出空指针异常，而Objects类中的equals方法就优化了这个问题。

+ `public static boolean equals(Object a, Object b)`

源码：
```java
public static boolean equals(Object a, Object b) {
    return (a == b) || (a != null && a.equals(b));
}
```
