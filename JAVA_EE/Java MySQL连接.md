## Java MySQL连接

### 1、下载连接MySQL驱动包

Java 连接 MySQL 需要驱动包，最新版下载地址为：**http://dev.mysql.com/downloads/connector/j/**，解压后得到 jar 库文件，然后在对应的项目中导入该库文件。

#### idea导包：

单击"File",选择"Project structrue",找到左上角的"Modules",中间的位置找到"Dependencies",最后单击"+",选择"JAR or directories",最后把你要的包导入就行了

如果是MySQL8.0以上版本

* 需要下载MySQLmysql-connector-java-8.0.16.jar

* com.mysql.jdbc.Driver更换为 com.mysql.cj.jdbc.Driver。
* MySQL 8.0 以上版本不需要建立 SSL 连接的，需要显示关闭。
* allowPublicKeyRetrieval=true 允许客户端从服务器获取公钥。
* 最后还需要设置 CST。

### 2、连接MySQL数据库

MySQL 8.0 以下版本 - JDBC 驱动名及数据库 URL 

* static final String JDBC_DRIVER = "com.mysql.jdbc.Driver";	// 不需要更改

* static final String DB_URL = "jdbc:mysql://localhost:3306/RUNOOB";	// 主机名和协议号如果是网络地址的话可以更改，最后一个参数是java连接的数据库名称。

MySQL 8.0 以上版本 - JDBC 驱动名及数据库 UR

* static final String JDBC_DRIVER = "com.mysql.cj.jdbc.Driver";	// 不需要更改

* static final String DB_URL = "jdbc:mysql://localhost:3306/RUNOOB?\useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC";		
    // 主机名和协议号如果是网络地址的话可以更改，RUNOOB参数是java连接的数据库名称需要改成自己的数据库，useSSL需要使用的话可以设置为true，allowPublicKeyRetrieval=true 允许客户端从服务器获取公钥，服务器的时区：UTC

数据库的用户名与密码，需要根据自己的设置(把用户名和密码设置为常量有利于代码的重复使用，而且需要修改时只要修改常量就可以)   

* static final String USER = "root";    
* static final String PASS = "123456";

注册JDBC驱动

* Class.forName(JDBC_DRIVER);

Connection类：与特定数据库的连接（会话），执行SQL语句并在连接的上下文中返回结果。
实例化对象: DriverManager.getConnection(DB_URL, USER, PASS);

Sratement类：用于执行静态SQL语句并返回其生成的结果的对象。 
实例化对象：Statement sta = conn.createStatement();

### 3、Java中给MySQL增删改查

* 定义插入的sql语句

    String sql = "insert into 表名 （字段列表） values  (值列表)";		//定义插入
    sta.executeUpdate(sql);		// 更新数据库

* 定义删除的sql语句

    String sql = "delete from 表名 where 条件";		//定义删除
    sta.executeUpdate(sql);		// 更新数据库

* 定义修改的sql语句

    String sql = "update 表名 set 字段名 = 数值 where 条件";		//定义更新
    sta.executeUpdate(sql);		// 更新数据库

* 定义查询的sql语句

    String sql = "select (字段名) from 数据表"；		// 定义查询

    ResultSet rs = stmt.executeQuery(sql);				// 执行查询数据库的操作，并将查询结果存放在ResultSet对象rs中

使用while(rs.next())循环输出查询出的记录
格式：while(rs.next()) {

​	.....

}

关闭连接

st.close();		// 关闭st对象
con.close;		// 关闭连接
rs.close;			// 关闭查询		









