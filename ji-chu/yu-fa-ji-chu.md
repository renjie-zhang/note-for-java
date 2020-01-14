# 语法基础

### Java中的关键字

基本数据类型相关（8个）：byte、short、int、long、float、double、char、boolean 

流程控制语句相关（10个）：if、else、switch、case、default、break、for、while、do、continue 

判断某个对象是否是某种类型的实例对象运算符：instanceof 

定义类：class 

创建类的对象：new 

包相关：package、import 

权限修饰符：public、protected、（缺省）、private 

继承类：extends 

定义接口：interface 

实现接口：implements 

当前对象：this 

父类引用：super 

表示无返回值：void 

结束方法：return 

定义枚举：enum 

其他修饰符：abstract、static、final、native 

异常处理：try、catch、finally、throws、throw 

多线程同步和安全：synchronized、volatile

### 基本数据类型

#### 整型

1. 字节类型\(byte\):占用内存大小是1个字节,值的范围是-128~127
2. 短整型\(short\):占用内存大小是为2个字节，值的范围是-32767~32767（2的15次方）
3. 整型\(int\):占用内存大小是4个字节，值的范围是-2147483648~2147483647 \(2的31次方\)
4. 长整型\(long\):占用内存大小是8个字节，值的范围是-9223372036854775808~9223372036854775808（2的63次方）

**浮点型**

1. 单精度浮点型\(float\):占用内存大小是4个字节，使用时数字后面需要带上f或者F，值的范围是1.4E-45 ~3.4028235E38 （2的128次方-1）
2. 双精度类型\(double\):占用内存大小是8个字节，值得范围是4.9E-324~1.7976931348623157E308 （2的1024次方-1）

**字符型**

1. 字符型\(char\):占用内存大小是2个字节，统一使用Unicode编码。

**布尔类型**

1. 布尔类型\(boolean\):只有True与False。

计算机的存储单位

计算机最小的单位：bit,比特  位，0/1

计算机最基本的单位：byte,字节  1KB=1024B

