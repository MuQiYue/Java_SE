## jdk8新特性

### 1 Lambda表达式

#### 1.1 函数式编程思想

在数学中，函数接收有输入量、输出量的一套计算方案，也就是“拿数据，做操作”
面对对象思想强调“必须通过对象的方式做事情"
函数式思想就是尽量忽视面对对象的复杂语法："强调做什么，而不是用什么形式去做"
而lambda表达式就是函数式思想的体现

#### 1.2 lambda表达式的标准格式

组成lambda表达式的三要素：形式参数、箭头、代码块

Lambda表达式的格式

* 格式：(形式参数) -> {代码块}
* 形式参数：如果有多个参数，参数之间用逗号隔开，没有参数，留空即可。
* ->：由英文中画线和大于符号组成，固定写法。代表指向动作
* 代码块：我们要做的事情

Lamdba使用前提：

* 有一个接口
* 接口中有且只有一个抽象方法 

####  1.3 lambda省略模式

* 参数的类型可以省略，但是有多个参数的情况下不能只省略一个
* 参数有且仅有一个时，小括号可以省略
* 代码块的语句只有一条时，可以省略大括号和分号甚至可以省略return

#### 1.4 Lambda注意事项

注意事项

* 使用Lambda必须要有接口，并且要求接口有且仅有一个方法

* 必须有上下文环境，才能推导出Lambda对应的接口

    ​	根据局部变量的赋值得知Lambda对应的接口
    ​	Runnabler = () -> System.out.println("Lambda表达式")；

    ​	根据调用方法的参数得知Lambda对应的接口：
    ​	new Thread(() - > System.out.print("Lambda表达式"))；

#### 1.5 Lambda表达式和匿名内部类的区别

所需类型不同

* 匿名内部类：可以是接口，也可以是抽象类，还可以是具体类
* Lambda表达式：只能是接口

使用限制不同

* 匿名内部类 :如果接口中有且一个抽象方法，可以使用Lambda表达式，也可以使用匿名内部类
* Lambda表达式：如果有多个方法只能使用匿名内部类

实现原理不同

* 匿名内部类：编译之后惠产生一个class字节码文件
* Lambda表达式：编译之后，不会产生字节码文件。对应的主机名会在运行的时候动态生成

### 2 接口组成更新

#### 2.1接口组成更新概况

接口的组成部分：

* 常量(final)
* 抽象方法(abstract)
* 默认方法(dafault)
* 静态方法(static)
* 私有方法(private)

#### 2.2 接口中默认方法

接口中默认方法的定义格式

* 格式：`public default 返回值类型 方法名(参数列表) { }`
* 范例：`public dafault void show() { }`

默认方法的注意事项

* 默认方法不是抽象方法，不强制被重写，但可以重写它，重写是去掉default关键字
* public可以省略，default不能省略

#### 2.3 接口中静态方法

接口中静态方法的定义格式

* 格式：`public static 返回值类型 方法名(参数列表) { }`
* 范例：`public static void show() { }`

静态方法的注意事项

* 静态方法只能通过接口名调用，不能通过实现类名或者对象调用
* public可以省略，static不能省略

#### 2.4 接口中私有方法

接口中私有方法的定义格式

* 格式1：`private static 返回值类型 方法名(参数列表) { }`
* 范例2：`private static void show() { }`
* 格式1：`private  返回值类型 方法名(参数列表) { }`
* 范例2：`private  void show() { }`

静态方法的注意事项

* 默认方法可以调用私有静态方法也可以调用私有方法
* 静态方法只能调用私有静态方法

### 3 方法引用

#### 3.1  方法引用符

方法引用符

* ::  该符号为引用运算符，而它所在的表达式被称为方法引用

    lambda表达式：`useShow(s - > System.out.println(s));`
    		分析：拿到参数s之后通过Lambda表达式，传递给System.out.println方法处理

    方法引用：`useShow(System.out::println)；`
    		分析：直接使用System.out中的输出方法取代Lambda，代码更整洁

推导和省略

* 如果使用lambda表达式，那么根据“可推导就是可省略”的原则，无需指定参数类型，也无需指定方式重载，他们都会吧推导
* 如果使用方法引用，也可以根据上下文进行推导
* 方法引用和Lambda表达式是孪生兄弟

#### 3.2 引用类方法

引用类方法，其实就是引用类的静态方法

* 格式：类名::静态方法

* 范例：Integer::parselnt

    ​	lnteger类的方法：publicstatic int parselnt(String s)	将此String转换为int类型

Lambda表达式被类方法替代的时候，他的形参全传递给静态方法作为参数

#### 3.3 引用对象的实例方法

引用对象的实例方法，其实就是引用对象中的成员方法

* 格式：对象::成员方法

* 范例：“HelloWorld”::toUpperCase

    ​	String类中的方法：public String toUpperCase() 将此String所有字符转换为大写

Lambda表达式被引用对象的实例方法替代的时候，他的形参全传递给引用对象的实例方法作为参数

#### 3.4 引用类的实例方法

引用类的实例方法，其实就是引用类中的成员方法

* 格式：类名::成员方法

* 范例：String::substring

    ​	String类中的方法：public String substring (int beginlndex, int endlndex
    ​	从beginlndex开始到endlndex结束，截取字符串。返回一个子串，子串长度为beginlndex-e
    endlndex.

Lambda表达式被类的实例方法替代时，第一个参数作为调用者，其余的参数全部传递给调用者当参数。

#### 3.5 引用构造器

引用构造器，其实就是引用类的构造方法

* 格式：类名::new
* 范例：Student::new

Lmabda表达式被构造器替代的时候，他的形参全部传递给构造器作为参数

### 4 函数式接口

#### 4.1 函数式接口概述

函数式接口：有且仅有一个抽象方法的接口（是lambda表达式的前提）

java中的函数式编程体现就是Lambda表达式，所以函数式接口就是可以适用于Lambda使用的接口
只有确保接口中有且仅有一个抽象方法，java的lambda表达式才能顺利执行。

如何检验一个接口是不是函数式接口？

* @Functionallnterface
* 放在接口定义的上方：如果接口是函数式接，编译通过；如果不是，编译失败。

注意事项：

* 我们定义函数式接口时，@Functionallnterface是可选的，就算不写，只要满足函数式接口定义条件，也照样是函数式接口。但强烈建议加上注解。

#### 4.2 函数式接口作为方法的参数或方法的返回值

如果方法的参数是一个函数式接口，我们可以使用Lambda表达式作为参数传递

如果方法的返回值是一个函数式接口，我们可以使用Lambda表达式作为结果

#### 4.3 常用的函数式接口

jdk8 在java.util.funcion包下预定义了大量的函数式接口供我们使用

重点学习4种

* Supplier接口
* Consumer接口
* Predicate接口
* Function接口

#### 4.4 Supplier接口

Supplier<T>: 包含一个无参的方法

* T get(): 获得结果
* 该方法不需要参数，它会按照某种实现逻辑(由Lambda表达式实现)返回一个数据
* Supplier<T>接口也被称为生产型接口，如果我们指定接口的泛型是什么类型，那么接口中的个体方法就会生产什么类型的数据供我们使用

#### 4.5 Consumer接口

Consumer<T>: 包含两个方法

* void accept(T t): 给定的参数执行此操作
* default Consumer<T> andThen(Consumer after): 返回一个组合额Consumer，执行此操作，然后执行after操作
* Consumer<T>接口也称为消费型接口，它消费的数据的数据类型由泛型指定

#### 4.6 Predicate接口

Predicate<T>: 常用的四个方法

* Boolean test<T t>: 给定的参数进行判断(判断逻辑由Lambda表达式表现)，返回一个布尔值
* default Predicate<T> negate() ：返回一个逻辑的否定，对应逻辑非
* default Predicate<T> and(Predicate<? super T> other) ：返回一个组合判断，对应短路与
* default Predicate<T> or(Predicate<? super T> other) : 返回一个组合判断，对应短路或

这个接口通常用于判断参数是否满足于某个条件

### 5 Stream流

Stream流的

#### 5.1 stream流

Stream使用场景：Stream流主要对集合进行快捷操作，能数据库场景进行筛选、循环、过滤等一系列操作，在不使用Stream流的情况下， 这样会大大增加代码量，间接增加编写难度

Stream流是真正把函数式编程带进java的。

Stream流的使用

* 生成流：对象.stream()

    通过数据源（集合、数组）生成流

* 中间操作:  filter()

    一个流后面可以跟随多个中间操作，其目的主要是打开流，做完数据的过滤或映射，然后返回新的流

* 终结操作:  forEach()

    一个流只能有一个终极操作，当执行这个操作是，这个流就不能被使用了

####  5.2 Stream流的生成方式

常见的生成方式：

* Collection体系的集合可以使用默认方法stream()生成流

    default Stream <E> stream()

* Map体系的集合间接的生成流

  map体系不能直接生成流，但他的键、值、键值对象可以使用stream生成流
  
* 数组可以通过Stream接口的静态方法of(T ...values)生成流

Stream流的静态方法of() 的参数可以是数组对象、数组本身和可变参数。

#### 5.3 Stream流的中间操作方法

* Stream<T> filter(Predicate<? super T> predicate) 

    用于对流中数据进行过滤

* Stream<T> limit(long maxSize) 

    返回此流中的元素组成的流，截取前参数的数据

* Stream<T> skip(long n) 

    跳过指定参数个数的流，返回其余数据

* static <T> Stream<T> concat(Stream<? extends T> a, Stream<? extends T> b) 

    合并a、b两个流成一个流

* Stream<T> distinct() 

    返回该流中的不同元素（Object.equals(Object)）组成的流

* Stream<T> sorted() 

    将流自然排序

* Stream<T> sorted(Comparator<? super T> comparator) 

    返回该流组成的流，根据题干的Comparator进行排序

#### 5.4 Stream流的终结操作

* void forEach(Consumer<? super T> action) 

    对此流的每个元素执行操作

* long count() 

    返回此流中元素的数量。 

#### 5.5  Stream流的收集

概述：

Stream提供的方法只能接受collector的接口，所以就有了collectors类提供的方法

Stream流的收集方法

* `R collect(Collector collector)`
    * 这个收集方法的参数是collector接口

工具类collectors提供了具体的收集方法

* public static <T,?,List<T>> toList() 
    * 返回 Collector ，将输入元素累积到新的 List
* static <T> Collector<T,?,Set<T>> toSet() 
    * 返回 Collector ，将输入元素累积到新的 Set 
* static <T,K,U>  Collector<T,?,Map<K,U>> toMap(Function keyMapper, Function valueMapper)
    * 返回collector，将键和值累计到新的Map 

