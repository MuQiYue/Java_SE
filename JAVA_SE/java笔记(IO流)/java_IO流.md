## I/O流

### 1 File

#### 1.1 File描述

它是文件和目录路径名的抽象表示。
<!--more-->
特点：
1、文件和目录都封装在file对象中
2、对于File来说，封装的可以是具体的文件和目录，也可以是不存在的抽象路径，可以通过具体的方法来实现转换

#### 1.2 File创建方法

`boolean create newfile()`
文件不存在是，创建一个抽象路径
`Boolean mkdir()`
创建由此路径的目录
`Boolean mkdirs()`
创建由此路径的目录，包括他没有的父目录

#### 1.3 File类的判断和获取功能

`Boolean isDirectory()`
判断这个路径名是否是目录
`Boolean isFile()`
判断路径名是否为文件
`Boolean exists()`
判断是否该路径名的文件是否存在
`String getAbsolutePath()`
返回路径名的绝对路径
`String getPath()`
把路径名转换为字符串
`String getName()`
返回这个路径名的文件和目录的名称
`String[] list()`
返回路径名表示的目录中的文件和目录的字符串数组
`File[] listFiles()`
返回路径名表示的目录中的文件和目录的file对象数组

#### 1.4 File删除功能

`Boolean delete()`
删除由此路径名表示的文件和目录
删除目录时要把目录中的内容删除，否则无非删除目录

#### 1.5

### 2 字节流

字节输入流读数据的步骤
1、创建字节输入流对象
2、调用字节输入流对象的写或读数据方法
3、释放资源(`close方法`释放)

##### 2.1字节流

i/o流分类
按照数据的流向
	输入流：读数据
	输出流：写数据
按照数据类型来分
字节流
	字节输入流；字节输出流
字符流
	字符输入流；字符输出流
我们一般说io流的分类是按照数据类型来区分的
如果数据能用Windows自带的记事本打开，里面的内容还可以读懂里面的内容就使用字符流
否则使用字节流，不知道该使用哪种就使用字节流

##### 2.2字节流写数据

字节流写数据
字节流的基类
`inputstream`：这个抽象类是表示字节输入流的所有类的超类
`outputstream`：这个抽象类是表示字节输出流的所有类的超类
子类的特点都是以其父类名作为结尾

`FileOutoutstream`：文件输出流用于将数据写入file
`fileoutputstream（string name）`：创建文件输出流以指定的名称写入文件
name为文件绝对路径

##### 2.3字节流的输入的三种方式

void wrte(int)
写单个字节
`void write(byte[] bys)`
写多个字节
`void write(byte[] bys, int off, int len)`
写部分字节,off表示哪里开始，len表示写多少个

##### 2.4字节流写数据的两个问题

换行和追加

换行符: 
`windows: \r\n`
`linux: \n`
`mac: \r`

追加:
`FileOutputStream(String name,boolean append)`
以指定的名称写入文件，如果第二个参数为true，写入文件将以文件的末尾开始写

##### 2.5字节流写数据加异常处理

finally关键字

`try{`
		`可能出现的异常代码`
`} catch (异常类名 变量名) {`
		`异常的处理代码`
`} finally {`
		`执行所有清除操作`
`}`

##### 2.6字节流读数据

`FileInputStream(String name)`

通过打开与实际的连接来建立一个读文件，该文件有文件系统中的路径名name命名
把相关的数据输出到控制台

##### 2.71一个一个字节读

核心代码
int len;
while ((f1 = fis.read()) != -1) {
           fos.write(f1);
        }

##### 2.72一个一个字节数组读

字节数组使用1024或者其倍数

核心代码

byte[] by = new byte[1024];
        int len;
        while ((len=fis.read(by)) != -1){
            fos.write(by,0,len);
       }

##### 2.8字节缓冲流

`BufferedInputStream bis = new BufferedInputStream(`

`new FileInputStream("文件路径"));`输出流也同理

最高可以缓冲8192个字节，极大提高速率。

---

### 3 字符流

##### 3.1 字符流

字符流就是字节流加上编码集

##### 3.2 编码集

常见的编码集：ASCII码、GBK、UTF-8
使用什么编码就要使用什么解码，不然就会出现乱码

##### 3.4 字符串编码和解码

编码
byte[] getByte();
使用平台的默认的字符集

byte[] getByte(String charsetName);
使用指定的字符集来存储

解码
String (byte[] bytes)
通过平台的默认的字符集来解码

String (byte[] bytes, String charsetName);
使用指定的字符集解码

##### 3.5 字符流的编码和解码

字符流抽象基类
Reader		读取字符
Write			写入字符

Reader具体类
InputStreamReader()		字节流到字符流的桥梁

>InputStreamReader(inputStream int);
>使用默认的字符集
>InputStreamReader(inputStream int, String charsetName)
>使用指定的字符集
>FileReader(String name)
>改进版缩写了前面的复杂的格式

Write具体类
OutputStreamWriter()		字符流到字符流的桥梁

> OutputStreamReader(OutputStream out);
> 使用默认的字符集
> OutputStreamReader(OutputStream out, String charsetName)
> 使用指定的字符集
> FileWrite(String name)
> 改进版缩写了前面的复杂的格式

##### 3.6 字符流写数据的5种方式(把数据写文件)

1、void write(int c)
写一个字符

2、void write(char[] cbuf)
写一个字符数组

3、void write(char[] cbut, int off, int len)
写一字符数组的部分

4、void write(String str)
写一个字符串

5、void write(String str, int off, int len)
写一个字符串的部分

释放流(写入文件)
void flush()

关闭流(关闭)
void close()

##### 3.7 字符流读数据(输出在控制台)

两种方式
int read()
一次读一个字符数据

int read(char cbuf)
一次读一个字符数组数据

##### 3.8 字符缓冲流

bufferedWriter(Writer out)
字符输出缓冲流，提高字节、数组和字符串的高效写入
写的特有功能：
void newLine()
写一行行分隔符，行分隔符有系统属性定义

bufferedReader(Reader in)
字符输入缓冲流，提高字节、数组和字符串的高效读取
String readLine()
读一行文字，包括行的内容的字符串，不包括行终止符 

##### 3.91 复制文件夹

1、创建数据源file对象
2、创建目的地file对象
3、使用copyFolder方法复制文件夹
3.1、调用数据源和目的地的file对象
3.2、判断是否数据源file是否为文件夹
3.21、把数据源file下文件夹的名字复制下来
3.22、目的地file添加和数据源file名称一样的file对象
3.23、判断是否目的地文件夹是否存在文件
3.24、获取数据源下文件名的file数组
3.25、遍历数据源的每一个文件名，递归copyFolder方法
3.3、说明获取到的是文件，直接复制，使用字节缓冲流
3.31、创建目的地对象使用目的地file和数据源getName方法得到的字符串
3.32、调用copyFile复制文件的方法

##### 3.92 处理复制文件异常

建议使用jdk7的改进方案(可以自动释放资源，而不用手动去书写)

try（file输入和输出流对象）{
		......
} catch(IOException e) {
		e.printStackTrace
}

### 4 特殊操作流

##### 4.1 标准输入输出流 

public static fina InputStream in;
标准输入流，通常使用该流键盘输入或由主机环境或用户指定的另一个输入源

BufferedReader br = new BufferedReader(new IntputStreamReader(system in));
自己实现键盘录入

Scannner sc = new Scanner(System.in);
自己来实现太麻烦，java提供相对应的Scanner来实现键盘录入



public static fina outputStream out;
标准输出流，通常使用该流键盘输出或由主机环境或用户指定的另一个输出源
System.out :本质上是一个字节输出流
PrintSteam Ps = System.out;
printStream类有的方法，system.out都可以使用

##### 4.2 打印流

分类：
字节打印流：PrintSteam
字符打印流：PrintWriter

打印流的特点：
只负责输出数据，不负责读取数据
有自己的特殊方法

字节打印流
构造方法：
PrintSteam(String FileName)

使用指定的文件名创建新的打印流
特点：使用继承父类的写方法写数据( writer方法)，查看时会转码；而使用自己的特有方法时(print/println)，查看的数据还是原来的。

字符打印流
构造方法：
PrintWriter(String fileName)
使用指定的文件名创建一个新的PrintWriter，而不需要自动执行刷新
PrintWriter(Writer out, boolean autoFlush)
创建一个新的PrintWriter
out	字符输出流
autoFlush	布尔值，为真print、printf和format方法将刷新缓冲区

##### 4.3 对象序列化流

对象序列化：将对象保存到磁盘中或者在网络中传输对象
这种机制就是使用一个字节序列表示一个对象，该字节序列包含：对象的类型、对象的数据和对象中存储的属性等信息，字节序列写到文件中持久保存了一个对象的信息；反之，该字节序列还可以从文件中读取回来，重构对象对它进行反序列化

对象序列化流：
ObjectOutputSteam
ObjectOutputStream将Java对象的原始数据类型和图形写入OutputStream。 可以使用ObjectInputStream读取（重构）对象。 可以通过使用流的文件来完成对象的持久存储。 如果流是网络套接字流，则可以在另一个主机或另一个进程中重新构建对象。 

构造方法：
ObjectOutputSteam(OutputSteam out)
创建一个写入指定OutpuSteam的ObjectOutputSteam

序列化对象的方法
void writeObjuct(Objuct obj)
将指定的对象写入ObjectOutputSteam

一个对象要想被序列化，该对象所属的类必须实现Serializable接口
Serializable是一个标记接口，不需要重写任何方法



对象反序列化流：
ObjectInputStream
ObjectInputStream反序列化先前ObjectOutputStream编写的原始数据和对象

构造方法：
ObjectInputStream(InputStream in)
创建从指定的InputStream读取的ObjectInputStream

反序列化的方方法
Object readObject()
从ObjectInputSteam读取一个对象

1、用对象序列化流序列化了一个对象，假如我们修改了对象所属的类文件，读取数据会出问题，并抛出InvalidClassException异常

2、出现了InvalidClassException异常，可以给对象所属的类加上SerialVersionUID
		private static final 容serialVersionUID = 42L;

3、如果对象中一个成员变量的值不想被序列化，请给该成员变量加上transient关键字修饰，该关键字标记的成员变量不参与序列化过程

##### 4.4 Properties

概述：

Properties是一个Map体系的集合类，可以保存到流中或从流中加载(不能使用泛型声明)

作为集合的特有方法
Object setProperty(String key, String value);
设置集合的键和值，都是String类型的，底层调用Haphtable方法put
String getProperty(String key);
使用此属性列表中指定的键搜索属性
Set<String> stringPropertyNames();
从该属性列表中返回一个不可修改的键集，其中键和他对应的值是字符串

Properties和IO流结合的方法
void load(lnputStream inStream)
输出字节流读取属性列表(键和元素对)
void load(Reader reader)
输出字符流读取属性列表(键和元素对)
void store(OutputStream out, String comments)
将此属性列表(键和元素对)写入Properties表中，以适合使用load(InputStream)方法的格式写入输出字节流
void store(Writer writer, String comments)
将此属性列表(键和元素对)写入Properties表中，以适合使用load(Reader)方法的格式写入输出字符流















