## 集合

### 集合的体系结构



![导图3](G:\Typora\java\java笔记(集合)\导图3.jpg)

### 1 Collection

#### 1.1 Collection概述

* collection是单例集合的顶层接口，他表示一组对象

* JDK不提供接口的任何直接实现，他提供更具体的子接口

创建Collection集合对象

* 多态的方式
* 具体的类(ArrayList)

#### 1.2 Collection常用方法

`Boolean add(E e)`
添加方法

`boolean remove(Object 0)`
删除集合中的元素

`boolean contains(Object o)` 
判断集合中否存在指定元素

`void clear()`
清除集合中的元素

`Boolean isEmpty()`
判断集合是否为空

`int size()`
计算集合中的个数

#### 1.3 集合中的迭代器(Iterator)

Iterator概述：

* 提供一种方法对容器对象中的各个元素进行访问，而不是暴露该对象容器的内部结构

常用方法：

`boolea hasNext()`
遍历集合(如果迭代器返回一个集合而不是异常，则为true)

`E next()` 
返回迭代中的下一个元素。  

#### 1.4 列表迭代器(ListIterator)

ListIterator概述：

* 提供List集合的Iterator()方法得到，是List特有迭代器

常用方法：

`boolean hasPrevious()` 
逆向遍历集合

`E previous()` 
返回上一个元素

`void add(E e)`
将指定的元素插入列表

### 2 List集合

#### 2.1 List概述

list的概述：

* 有序集合（也称为*序列* ）。该接口的用户可以精确控制列表中每个元素的插入位置。用户可以通过整数索引（列表中的位置）访问元素，并搜索列表中的元素。
* 与set集合不同，list集合通常允许重复元素。 

特点：

* 有序：存储和取出的顺序一样
* 可重复：存储的数据可以重复

#### 2.2 List方法

特有方法：

`void add (int index, E ele)`
在集合中的指定位置插入数据

`E remove(int index)`
删除指定索引的元素

`E set(int index, E element)`
更改指定索引的元素

`E get(int index)`
返回指定索引的元素

#### 2.3 增强for循环

概述：

* 简化了数组和collection集合 的遍历
* 实现Iterable接口的类允许其对象成为增强for循环语句
* 它是jdk5之后出现的，其内部的原理是一个迭代器

格式：

​	for(类、数组、数据类型、集合  name ：对应的) {

​		。。。。。。。。。。。

}

范例：

`int[] arr ={1,2,3,4,5};`
`for (ine i : arr) {`
		`System.out.print(i)；`
`}`

}

#### 2.4 List集合子类特点

常用的子类有：`ArrayList、LinkedList`

ArrayList:底层的数据结构是数组、查询快、增删慢
LinkedList:底层的数据结构时链表，查询慢，增删快



#### 2.5 LinkedList集合

概述：双链表实现了List和Deque接口。实现所有可选列表操作，并允许所有元素(包括null)。 

常用方法：

`void addFirst(E e)`
在此列表的开头插入指定的元素。 

`void addLast(E e)`
将指定的元素追加到此列表的末尾。

`E getFirst()`
返回此列表中的第一个元素。  

`E getLast()`
返回此列表中的最后一个元素。    

`E removeFirst() `
从此列表中删除并返回第一个元素。  

`E removeLast() `
从此列表中删除并返回最后一个元素。

### 3 Set集合

### 3.1 set集合特点

特点：

* 不包含重复元素的集合
* 没有索引的方法，不能使用普通的for循环

#### 3.2 哈希值

概述：

是jdk根据对象的地址或字符串或数字计算出来的int类型的数值

object类中有一个方法可以获取对象的哈希值

`int hashCode()`
返回对象的哈希值

特点：

* 同一对象多次调用hashCode()方法返回的哈希值是相同的
* 默认情况不同哈希值是不同的，但重写hashCode()方法，可以实现不同对象哈希值相同。

#### 3.3 LinkedHashset集合

概述：

Hash表和Set接口的链表实现，具有可预测的迭代顺序。 

* 由链表保证数据有序，也可以说元素存储和取出是一致的
* 有哈希表保证数据唯一

#### 3.4 Treeset 集合

特点：

Treeset是顺序的集合。有顺序不是指存储和取出，而是排序方法取决于构造方法

* `TreeSet()`  构造一个新的空树集，根据其元素的自然顺序进行排序。 
* `TreeSet(Comparator<? super E> comparator)`  构造一个新的空树集，根据指定的比较器进行排序。  

由于没有索引方法不能使用普通for遍历，他实现了set接口所以数据不能重复

#### 3.5 comparable的使用(自然排序)

用Treeset集合存储自定义对象，无参构造方法使用的是自然排序

* 自然排序就是让元素所属类实现comparable接口，重写int compareTo(T o)方法
* 重点：重写方法时一定要明白主要条件和次要条件
* 元素所属类实现comparable接口

#### 3.6 comparator的使用（比较器排序）

同样使用Treeset集合存储自定义对象，使用比较器排序对行元素排序

* 使用内部类创建新的comparator,重写int compare(T o1, T o2) 
* 重点：重写方法时一定要明白主要条件和次要条件
* 谁用谁就重写内部类

### 4 泛型

#### 4.1 泛型的概述

本质是参数化类型，可以说说操控的数据类型为一个参数。参数化类型可以理解为将类型有原来的具体的类型参数化(抽象化)，然后在使用/调用时传入具体的类型

格式：

* <类型>：指定一种类型的格式：可以看做形参
* <类型，类型>：指定多种类型的格式，可以看做形参
* 将来具体调用时给定的类型可以看做实参，并且实参的类型只能隐约数据类型

好处：

* 把运行时异常改为编译时异常，让我们提前处理
* 有了泛型，程序就不需要强转类型了

#### 4.2 类型通配符

* `<?>`

    格式：List<?>:表示元素类型未知的list类型，可以匹配任何的类型

    这种方法表示各种List的父类，并不能把元素带入其中

* `<? extends 类型>`

    格式：List<? extends Number>它表示的类为Number或者其子类型

    表示其上限

* `<? super 类型>`

    格式：List<? super Number>它表示的类为Number或者其子类型

    表示其下限

#### 4.3 可变参数

概述：

​	可变参数又称为参数个数可变，用作方法的形参出现，那么他的形参就是可变的

格式：

修饰符 返回值类型 方法名（数据类型 ...变量名）{}

范例:

`public int arr (int ...a) {}`

注意事项：

* 变量名存储的是一个数组
* 如果一个方法有多个参数，其中包括可变参数，那么一定要把可变参数放在最后。

### 5 Map 集合

#### 5.1 Map

概述：

* 将键映射到值的对象。
* 集合不能包含重复的键; 每个键最多可以映射一个值

格式：
`Interface Map<K,V>`
K:键的类型		V：值的类型

#### 5.2 Map基本方法

基础方法：

`V put(K key, V value) `
添加元素

`V remove(Object key)`
根据键删除键对元素

`void clear() `
从此映射中删除所有映射 

`boolean containsKey(Object key) `
如果集合中有指定的键，则返回 true 。  

`boolean containsValue(Object value) `
如果集合中有指定的值，则返回true

`boolean isEmpty() `
如果集合为空，返回true

`int size()`
返回映射的个数

#### 5.3 Map的获取方法

`V get(Object key) `
根据键获取值，没有则返回null

`Set<K> keySet() `
获取所有键的集合

`Collection<V> values()`
获取所有值的集合

`set <Map.Entry<K,V>> entry set()`
获取所有键值对象的集合

#### 5.4 Map遍历方法一

思如：

* 首先使用`set<k> keyset()`获取所有键的内容
* 使用增强for来遍历每一个键
* 使用`V get(Object key)` 方法来根据键获取值

#### 5.5 Map遍历方法二

思路：

* 使用`set <Map.Entry<K,V>> entry set()` 获取所有键值对象的集合
* 使用增强for遍历键值对对象的集合，得到每一个键值对对象
* 使用`K getKey()` 得到键，使用`K getValue()` 得到值



#### 6 collections

概述：

​	是一个针对集合操作的工具类

常用方法：

`static <T extends Comparable<? super T>> void sort(List<T> list)` 
将指定列表按升序排序

`static void reverse(List<?> list) `
反转指定列表中的元素

`static void shuffle(List<?> list) `
使用默认的随机源随机排序指定列表

