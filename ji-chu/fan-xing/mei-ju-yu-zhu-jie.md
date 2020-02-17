# 枚举与注解

### 枚举

类型的对象是有固定几个时，此时便可以将这种声明为枚举类型。在Java 5之前，枚举类中的final修饰；而在Java 1.5 之后，使用enum关键字。  
实例：

```text
public enum Week{
	MONDAY(1,"星期一"),
	TUESDAY(2,"星期二"),
	WEDNESDAY(3,"星期"),
	THURSDAY(4,"星期四"),
	FRIDAY(5,"星期五"),
	SATURDAY(6,"星期六"),
	SUNDAY(7,"星期日");
	
	private int number;
	private String decription;
	
	private Week(int number, String decription) {
		this.number = number;
		this.decription = decription;
	}
	
	public static Week getByNumber(int number){
		switch(number){
		case 1:
			return MONDAY;
		case 2:
			return TUESDAY;
		case 3:
			return WEDNESDAY;
		case 4:
			return THURSDAY;
		case 5:
			return FRIDAY;
		case 6:
			return SATURDAY;
		case 7:
			return SUNDAY;
		default:
			return null;
		}
	}

	public int getNumber() {
		return number;
	}

	public void setNumber(int number) {
		this.number = number;
	}

	public String getDecription() {
		return decription;
	}

	public void setDecription(String decription) {
		this.decription = decription;
	}

	@Override
	public String toString() {
		return super.toString()+"(" + number + ","+ decription + ")";
	}
	
}
```

备注:

1. 常量对象必须在首行，常量对象名用大写
2. 如果枚举类型除了常量对象，还有其他的成员，那么要求在常量对象后面，否则可以缺省
3. 如果要在枚举类型中声明构造器，那么构造器必须是private,默认也是private
4. 默认的toString\(\)防范，返回的常量名称
5. 枚举类型不能够继承别的类型，因为他有一个直接父类java.lang.Enum类型
6. 枚举类只有一个有参构造，调用的是父类的两个属性值，name\(常量对象名\)和ordinal\(序号，从0开始\)
7. 枚举类默认是实现了Comparable接口，默认是按照序号排序
8. 枚举类有两个编译器自动添加的方法：
   1. 枚举类型  valueof\(常量名\)
   2. 枚举类型\[\] values\(\)
9. 枚举类型可以实现接口；对于接口的抽象方法的实现，可以统一实现，也可以单独实现。

