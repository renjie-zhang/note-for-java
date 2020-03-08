# 集合

在平常的开发中，使用集合来作为对象的容器；在计算机中主要的数据结构有数组与链表，而根据逻辑结构产生了更加多样的容器。常用的容器如下图所示：

![Java&#x96C6;&#x5408;](../.gitbook/assets/java-ji-he.png)

在开发中使用较多的是ArrayList、LinkedList、HashMap等集合，涉及这部分集合的操作也是最为基础的部分。在并发包中concurrentHashMap,ConcurrentLinkedQueue等是并发场景下尝试用的集合。

### Iterable

Iterable是一个接口,Collection是继承与它的接口。其中Iterable的主要方法有：

```text
public interface Iterable<T> {
     /**
      *返回一个iterator的元素，类型为T
      */
    Iterator<T> iterator();

    /**
     * 从1.8开始，接口中存在默认实现
     */
    default void forEach(Consumer<? super T> action) {
        Objects.requireNonNull(action);
        for (T t : this) {
            action.accept(t);
        }
    }

    /**
     * 从1.8开始，接口的默认实现。创建一个spliterator，
     */
    default Spliterator<T> spliterator() {
        return Spliterators.spliteratorUnknownSize(iterator(), 0);
    }
}
```

### Collection

```text
public interface Collection<E> extends Iterable<E> {
    // 查询操作
    /**
     * 返回元素个数
     */
    int size();

    /**
     * 如果这个集合中没有元素则返回True
     */
    boolean isEmpty();

    /**
     * 如果此集合中有该元素，那么返回True
     */
    boolean contains(Object o);

    /**
     * 返回一个iterator
     */
    Iterator<E> iterator();

    /**
     * 
     */
    Object[] toArray();

    /**
     * 
     */
    <T> T[] toArray(T[] a);

    // 更新操作

    /**
     * 添加元素
     */
    boolean add(E e);

    /**
     * 移除元素
     */
    boolean remove(Object o);


    // Bulk Operations

    /**
     * 
     */
    boolean containsAll(Collection<?> c);

    /**
     * 
     */
    boolean addAll(Collection<? extends E> c);

    /**
     * 
     */
    boolean removeAll(Collection<?> c);

    /**
     * 
     */
    default boolean removeIf(Predicate<? super E> filter) {
        Objects.requireNonNull(filter);
        boolean removed = false;
        final Iterator<E> each = iterator();
        while (each.hasNext()) {
            if (filter.test(each.next())) {
                each.remove();
                removed = true;
            }
        }
        return removed;
    }

    /**
     * 
     */
    boolean retainAll(Collection<?> c);

    /**
     * 
     */
    void clear();


    // Comparison and hashing

    /**
     * 
     */
    boolean equals(Object o);

    /**
     * 
     */
    int hashCode();

    /**
     *
     */
    @Override
    default Spliterator<E> spliterator() {
        return Spliterators.spliterator(this, 0);
    }

    /**
     * 
     */
    default Stream<E> stream() {
        return StreamSupport.stream(spliterator(), false);
    }

    /**
     * 
     */
    default Stream<E> parallelStream() {
        return StreamSupport.stream(spliterator(), true);
    }
```

