# 常用API

### Object

它是所有类的父类，它所有的方法，在所有的对象都有，包括数组对象，任何对象创建的时候都会调用Object的无参构造方法。它常用方法如下：

1. clone\(\):如果子类支持克隆，子类需要实现cloneable\(\)接口，否则会报CloneNotSupportException。
2. equals\(\):如果子类需要比较的属性的内容，那么必须要重写这个方法，它是判断对象object是否与对象this相等。
3. hashcode\(\):如果重写了equals方法，那么就必须重写hashcode\(\)方法。与equals\(\)的关系，两个对象的equals\(\)返回true,两个对象的hashcode值便一定相等。两个对象的hashcode不相等，那么equals的结果便一定为false,如果两个对象的hashcode相等，但是equals不一定相等。
4. getClass\(\)返回某个对象的运行时类型，而不是编译时类型。
5. finalize\(\)当对象被垃圾回收机制回收之前调用，而且只会调用一次。
6. toString\(\)方法
7. notify\(\)、notifyAll\(\)、wait\(\)多线程中常使用的方法

### String

String不能被继承，因为String是final修饰的类，字符串对象是常量对象，一旦创建就不能修改，一旦修改便是一个新对象。它常用方法如下：

1. length\(\)返回字符串的长度。
2. isEmpty\(\)判断是不是空字符串
3. getBytes\(\)把字符串转成字节数组

### Time

时间格式化的方式：

```java
// one
LocalDate date = LocalDate.now();
date.format(DateTimeFormatter.ISO_DATE
// two
DateTimeFormatter dt = DateTimeFormatter.ofLocalizedDate(FormatStyle.FULL);
// three
DateTimeFormatter op = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
op.format(LocalDateTime.now())
```



