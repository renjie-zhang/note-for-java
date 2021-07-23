# Optional

在开发中，都很大部分都是在验证传入的类型是否是需求的类型，也总是在判断是否为空，但是也会总出现空指针异常，使用Optional是为了可以尽量避免空指针。

```text
// 创建
// 创建一个空的Optional对象
Optional.empty()
// 包装了一个对象的Optional
Optional.of(object)
// 创建一个可能为空的对象
Optional。ofNullable(object)

// 获取包装类对象
// 如果Optional包装的对象不为空，正常返回，如果为空，报异常
Optional.get()
// 如果Optional包装的对象不为空，那么则正常返回，如果为空，那么便返回一个other对象
Optional.orElse(T other)
// 如果Optional包装的对象不为空，正常返回，如果为空，返回由供给型接口提供的对象
Optional.orElseGet(Supplier)
// 如果Optional包装的对象不为空，正常返回，如果为空，报异常，报的异常是由Supplier提供的异常对象
Optional.orElseThrow(Supplier<? extends X> exceptionSupplier)

// 是否存在
// 表示判断Optional中的包装的对象是否存在，如果存在就返回true，否则就是false
Optional.isPresent()
// 如果存在，就执行Consoumer指定的操作，如果不存在就不做
Optional.fPresent(Consumer<? super T> consumer) 

// 过滤
// 对Optional中包装的对象进行过滤，按照Predicate的条件进行判断，如果满足，返回它，
// 如果不满足，返回empty的Optional
Optional.filter(Predicate<? super T> predicate)  

// 映射
// 对Optional包装对象，执行Function中的apply方法，apply方法返回的结果是一个Optional，
// map方法的结果，把apply方法的结果直接返回
Optional.flatMap(Function<? super T,Optional<U>> mapper)  
// 对Optional包装对象，执行Function中的apply方法，apply方法返回的结果可以是任意结果，
// map方法的结果，把apply方法的结果包装成一个Optional对象
Optional.map(Function<? super T,? extends U> mapper) 
```

#### 

