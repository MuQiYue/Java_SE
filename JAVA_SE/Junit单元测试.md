### Junit单元测试

#### 1、测试分类：

* 黑盒测试：不需要关注内部的东西，只需要关注输入和输出
* 白盒测试：需要关注程序内部的流程。

#### 2、junit的使用：白盒测试

步骤：

* 定义一个测试类(测试用例)：
    * 推荐测试类名：被测试的类名Test
    * 包名：xxx.xxx.test

* 定义测试方法：可以独立运行
    * 方法名：test测试方法名（testAdd）
    * 返回值：void
    * 参数列表为空

* 给方法加@Test注解

* 导入junit依赖

判定结果：

* 红色为失败
* 绿色为成功
* 但我们一般都会使用断言操作来处理结果
    * Assert.assertEquals(期望的结果，运算的结果)

### 3、junit的其他注解

@Before
初始化方法：适用于测试方法中申请资源，每次测试方法运行时都先会执行一次被@Before注解的方法。

@After
释放资源方法：在所有测试方法执行完毕之后，都会自动执行该方法

