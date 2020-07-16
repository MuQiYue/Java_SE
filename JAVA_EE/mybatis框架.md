## mybatis框架学习

### 1、持久层技术：

JDBC:

* cobbection
* prepared
* statement

spring的JDBCTemplate和Apache的DBUtils都只是对JDBC的封装

jdbc是一种规范，而其他的只是他的工具类而已。

### 2、Mybatis概述：

​		是一个持久层框架，使用java编写，封装了JDBC操作的很多细节，使开发者只需要关注于SQL语句，无需关注注册驱动，和创建连接，它使用ORM思想封装结果集。

#### 2.1、ORM思想：Object Relatinal Mapping(对象关系映射)

简单来说就是让数据库表和实体类以及实体类的属性对应起来，让我们可以操作实体类从而来操作数据库表

### 3、Mybatis环境搭建

第一步：创建maven工程并导入坐标

* 建议使用阿里源 [settings.xml](settings.xml) ，可以更快的导入依赖包
* 配置pom.xml文件

第二步：创建实体类和dao的接口

* 在src的main包下创建相关的实体类和与dao想对应的接口

第三步：创建Mybatis的主配置文件

* SqlMapConifg.xml，配置文件中的内容在https://mybatis.org/mybatis-3/zh/getting-started.html下有

第四步：创建映射配置文件

* IUserDao.xml，配置文件中的内容在https://mybatis.org/mybatis-3/zh/getting-started.html下有

注意事项：

1、创建IUserDao.xml和IUserDao.java时名称是为了保持一致，在mybatis中它把持久层的操作接口名称和映射文件叫做：Mapper;

2、在idea中创建目录时，它和包是不一样的，包创建是com.chen.dao是一个三级结构，而目录创建时：com.chen.dao是一级目录

3、mybatis的映射配置文件位置必须和dao接口的包结构相同

4、映射配置文件的mapper标签namespace属性的取值必须是dao接口的全限定类名

5、映射配置文件的操作配置(select),  id属性的取值必须是dao接口的方法名

遵循第三，四，五点后，我们开发中就无需在写dao的实现类