# 反射

java是一门静态类型语言，但是在后来的发展中，为了让java实现“动态性”，加入了反射的机制。像JS这类动态语言，在编译阶段并不会确定变量的类型，只有真正运行到该变量处才会确定此变量的类型。

如何在获取类上的泛型：

```java
		Class clazz = GenericSub.class;

//  Class sup = clazz.getSuperclass();//得不到泛型的信息

//  System.out.println(sup);

		//Type是包含Class等的所有类型

		Type gs = clazz.getGenericSuperclass();

		//GenericSuper<String>：参数化的类型

		ParameterizedType p  = (ParameterizedType) gs;

		//获取类型实参

		Type[] arr = p.getActualTypeArguments();

		System.out.println(arr[0]);

		System.out.println(arr[1]);
```

### 类加载器

#### 双亲委派机制

某个类加载器接到加载任务，先把加载任务交给“父”加载器（多个类加载器的关系是组合的关系，并不是继承关系），层层往上，一直到引导类加载器，如果“父”加载器可以加载，那么就由“父”加载器加载，如果不可以，传回它的“子”加载器，“子”加载器尝试加载，如果可以，那么就加载，如果不可以，再往回传，一到回到最初接到任务的那个加载器，如果它可以，也正常加载，如果它也不能加载，报异常：ClassNotFoundException

#### 类加载器

1. 引导类加载器（Bootstrap ClassLoader）,非java语言实现
2. 扩展类加载器（Extension ClassLoader）,加载jre/ext目录下的class
3. 应用程序类加载器（Application ClassLoader）,加载用户自定义类型加载器
4. 自定义类加载器



