# Stream

为了践行1.8的函数式编程，使用StreamAPI对集合进行了一个补充，可以极大的方便程序员进行进行开发，它并不负责数据存储，每次操作都是一个新的stream，并不会影响源数据，stream中间是懒惰求值，一般在终结操作才会一口气完成。

#### 中间操作-筛选与切片

| 操作 |  |
| :--- | :--- |
| filter | 过滤 |
| distinct | 去重 |
| limit | 取前面几个 |
| skip | 跳过前面几个 |

#### 中间操作-映射

| 操作 |  |
| :--- | :--- |
| map\(Function\) | 对Stream中的元素进行某一个操作，返回值是特殊类型 |
| flatMap\(Function\) | 返回值一个stream,这些stream再合成一个大的stream |

#### 中间操作-排序

| 操作 |  |
| :--- | :--- |
| Sorted\(\) | 自然排序 |
| sorted\(Comparator\) | 定制排序 |

#### 终结操作-遍历

| 操作 |  |
| :--- | :--- |
| forEach\(\) | 遍历 |

#### 结束操作-匹配与查找

| 操作 |  |
| :--- | :--- |
| count\(\) | 统计 |
| max\(\) | 最大值 |
| min\(\) | 最小值 |

#### 结束操作-规约

| 操作 |  |
| :--- | :--- |
| Optional&lt;&gt; | Optional reduce\(BinaryOperator accumulator\) |
| BinaryOperator&lt;&gt; | BinaryOperator是一个BiFunction接口： T apply\(T t1, T t2\) |
| reduce | T reduce\(T identity,BinaryOperator accumulator\) |

#### 结束操作-收集

| 操作 |  |
| :--- | :--- |
|  R collect\(Collector&lt;? super T,A,R&gt; collector\) |  R collect\(Collector&lt;? super T,A,R&gt; collector\) |

