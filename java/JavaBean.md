# 标准代码——JavaBean

 `javaBean` 是Java语言编写类的一种标准规范。 符合 `JavaBean` 的类， 要求类必须是具体的和公共的， 并且具有无参数的构造方法， 提供用来操作成员变量的 `set` 和 `get` 方法

```java
public class Student() {
    private String name;
    private int age;

    public Student() {}

    public Student(String name,int age) {
        this.name = name;
        this.age = age;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public int getAge() {
        return age;
    }
}
```

