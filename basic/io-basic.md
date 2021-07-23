# IO Basic

IO流又称为输入输出流，其中四个抽象基类：InputStream、OutputStream、Reader、Writer。其中InputStream与OutputStream为字节流，Reader与Writer为字符流。

### 与文件相关的流

| 类型 | 描述 | 特点 |
| :--- | :--- | :--- |
| FileInputStream | 文件字节输入流 | 读取任意文件 |
| FileOutputStream | 文件字节输出流 | 写数据到任意类型的文件 |
| FileReader | 文件字符输入流 | 只能够读取纯文本文件 |
| FilerWriter | 文件字符输出流 | 只能把流保存到纯文本中 |

### 与处理相关的流

#### 缓冲流

主要作用是增加缓冲区，提供效率。

1. BufferedInputStream
2. BufferedOutputStream
3. BufferedReader
4. BufferedWriter

缓冲区大小：8192字节或者8192字符

#### 数据流

主要作用处理Java的基本数据类型+字符型

1. DataOutputStream
2. DataInputStream

#### 对象流

主要作用处理Java对象

1. ObjectOutputStream
2. ObjectInputStream

在序列化中是使用这两个对象，其中对象的序列化使用ObjectOutputStream，而反序列化使用ObjectInputStream,在此过程中需要注意的是：

1. 凡是要序列化的对象，它的类型必须要实现Serializable接口；
2. 如果在类的属性中也涉及到了应用类型，那么也需要将这个类型进行序列化；
3. 如果不想序列化，那么可以使用transient关键字，那么在序列化时会忽略；如果是反序列化，那么将会赋予一个默认的值；
4. 在实现Serializable接口时，最好加上一个常量，序列化版本ID，private static final long serialVersionUID = 1L;
5. 静态属性不能序列化。

#### 打印流

作用是可以打印各种类型的数据，最终都是以字符的形式打印，如果是应用类型那么就调用该类型的toString\(\)方法。

1. PrintStream
2. PrintWriter

