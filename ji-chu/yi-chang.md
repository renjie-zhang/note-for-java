# 异常

异常分为两大类：java.lang.Error和java.lang.Exception。Error相对来说更加的严重，比如常常遇见的StackOverflowError和OutOfMemoryError；这些都是导致程序奔溃的原因。Exception中一种是运行时异常，还有编译时异常，受检异常，需要自己编写代码去处理，否则编译不会通过，比他SQLException。

在平常的开发中，有时需要自定义异常，来满足对程序的控制，要想实现，需要以下几个要求：

1. 自定义异常一定要继承Throwable或者它的子类，原因是：只有这个类型或者它的子类的对象才有可能被“抛出”，只有这个类型或者它的子类才有可能会被“捕获”
2. 一般来说有两个构造器，一个是无参构造器，一个是类型异常\(String ErrorMessage\)
3. 需要进行序列化
4. 自定义异常的对象只能自己进行实例化，并手动抛出，使用throw关键字



