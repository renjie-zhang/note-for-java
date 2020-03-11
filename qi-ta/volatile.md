# Volatile

Java Volatile关键字用于标记一个变量“应当存储在主存中”。更完成的概述应该是每次读取Volatile所修饰的变量，都应该去主存中去读取，而不是从CPU缓存中读取。每次写入Volatile所修饰的变量，都应该写入到主存中，而不仅仅是写到CPU缓存中。

## 变量的可见性

Java Volatile是保证变量在多线程的修改下，所有线程都有可见性。在多线程的应用中，线程在操作变量时，处于对性能的考虑，每个线程可能会将变量从主存中拷贝到CPU缓存中。对于多个CPU，那么运行在各个CPU上的线程都会进行这样一个拷贝。如下图所示：

![](../.gitbook/assets/java-volatile-1.png)

## 完整的Volatile可见性保证

实际上，volatile的可见性保证并不是只对于volatile变量本身那么简单。可见性保证遵循以下规则：

* 如果线程A写入一个volatile变量，线程B随后读取了同样的volatile变量，则线程A在写入volatile变量之前的所有可见的变量值，在线程B读取volatile变量后也同样是可见的。
* 如果线程A读取一个volatile变量，那么线程A中所有可见的变量也会同样从主存重新读取。

使用一段代码来说明：

```java
public class MyClass {
    private int years;
    private int months
    private volatile int days;


    public void update(int years, int months, int days){
        this.years  = years;
        this.months = months;
        this.days   = days;
    }
}
```

在update方法中写入了三个变量，只有days是Volatile修饰的，在写入days变量时，线程中所有可见变量也会写入到主存中。也就是说写入days变量时，years和month也会写入到主存中。于此相同的思想，读取days变量时，也会从主存中去读取。

**译者注：可以将对volatile变量的读写理解为一个触发刷新的操作，写入volatile变量时，线程中的所有变量也都会触发写入主存。而读取volatile变量时，也同样会触发线程中所有变量从主存中重新读取。因此，应当尽量将volatile的写入操作放在最后，而将volatile的读取放在最前，这样就能连带将其他变量也进行刷新。上面的例子中，update\(\)方法对days的赋值就是放在years、months之后，就是保证years、months也能将最新的值写入到主存，如果是放在两个变量之前，则days会写入主存，而years、months则不会。反过来，totalDays\(\)方法则将days的读取放在最前面，就是为了能同时触发刷新years、months变量值，如果是放后面，则years、months就可能还是从CPU缓存中读取值，而不是从主存中获取最新值。**

其中注释比较绕，细细体会。

## 指令重排

出于对性能的考虑，JVM和CPU是允许对程序中的指令进行重排的，只要保证重拍之后的语义不会产生变化。以下面代码为例：

```java
int a = 1;
int b = 2;

a++;
b++;
```

可以按照一下顺序进行指令重排，而不改变语义：

```java
int a = 1;
a++;

int b = 2;
b++;
```

然而这个重排对于Volatile来说就有些不一样了。

```java
public class MyClass {
    private int years;
    private int months
    private volatile int days;


    public void update(int years, int months, int days){
        this.years  = years;
        this.months = months;
        this.days   = days;
    }
}
```

此段代码，一旦update了days的值，则years、months也会更新到主存中；但是如果指令重排之后，比如换成一下方式进行重排：

```java
publiv void update(int years,int months,int days){
    this.days   = days;
    this.years  = years;
    this.months = months;
}
```

在months、years被赋新值之前，就触发了这两个变量值写入主存的操作，自然这两个变量在主存中的值就不是新值。它们的新值并未更新到主存中，而对其他线程而言又是不可见的，所以导致了程序语义的改变。

## Java Volatile Happens-Before保证

为了解决指令重排的问题，Java的volatile关键字在可见性之外，又提供了happends-before保证。happens-before原则如下：**（此段很绕）**

* 如果有读写操作发生在写入volatile变量之前，读写其他变量的指令不能重排到写入volatile变量之后。写入一个volatile变量之前的读写操作，对volatile变量是有happens-before保证的。注意，如果是写入volatile之后，有读写其他变量的操作，那么这些操作指令是有可能被重排到写入volatile操作指令之前的。但反之则不成立。即可以把位于写入volatile操作指令之后的其他指令移到写入volatile操作指令之前，而不能把位于写入volatile操作指令之前的其他指令移到写入volatile操作指令之后。
* 如果有读写操作发生在读取volatile变量之后，读写其他变量的指令不能重排到读取volatile变量之前。注意，如果是读取volatile之前，有读取其他变量的操作，那么这些操作指令是有可能被重排到读取volatile操作指令之后的。但反之则不成立。即可以把位于读取volatile操作指令之前的指令移到读取volatile操作指令之后，而不能把位于读取volatile操作指令之后的指令移到读取volatile操作指令之前。

## 还需synchronized等保持原子性

使用Volatile来保证变量的可见性，但是并不能保证它的原子性，还需要synchronized来保证访问是同步的，保证了读写到的值是一个正确的值，而不是一个错误的值。

## Volatile的性能考虑

读写volatile变量会导致变量从主存读写。从主存读写比从CPU缓存读写更加“昂贵”。访问一个volatile变量同样会禁止指令重排，而指令重排是一种提升性能的技术。因此，你应当只在需要保证变量可见性的情况下，才使用volatile变量。

参考资料：

[http://ifeve.com/java-volatile%e5%85%b3%e9%94%ae%e5%ad%97/](http://ifeve.com/java-volatile关键字/)

