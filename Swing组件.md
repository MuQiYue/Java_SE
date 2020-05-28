### Swing组件

#### swing特点

和AWT组件相比

AWT组件基于本地方法的c/c++程序，运行速度更快一些；swing使用java编写编译起来更慢
AWT的控件在不同的平台有不相同的表现，而swing所有平台一致	

swing使用纯java编写，任何平台通用，而且swing不使用本地方法不依赖操作系统，所有是轻量级组件

#### swing概述

窗体组件结构

![image-20200520181850409](G:\Typora\java\image-20200520181850409.png)

#### swing常用组件

三个常用的容器组件

* JFrame   窗体
* JDialog   对话框
* JPanel   面板

其他的常用组件

* JButton   按钮
* JLabel   标签

* JCheckBox   多选按钮

* JRadioButton   单选按钮
* JTextField    文本框
* JPassWrold    密码框
* JComBox   下拉框
* JTextArea   文本域
* JList   列表框
* JOpetionPane   小对话框

#### swing_窗体（JFrame）

首先实例化 JFrame类，

* `void setVisible(Boolean TF)`     设置窗口可见
* `setTitle(string name)` 设置窗体标题
* `setLocationRelativeTo`   居中窗体
* `setDefaultCloseOperation`（指定参数）
    * `DO_NOTHING_ON_CLOS`E （在WindowConstants定义）：不要做任何事情; 
    * `HIDE_ON_CLOSE` （在WindowConstants定义）：自动隐藏框架。 
    * `DISPOSE_ON_CLOSE` （在WindowConstants定义）：释放窗体
    * `EXIT_ON_CLOSE` （在WindowConstants定义）：停止窗体
* `setSize(int long, int witch)`    设置窗体大小，单位：像素
* `setLocation(int long, int witch)`    设置窗体坐标，单位：像素
* `setBounds(int long, int witch ,int long, int witch)`    设置坐标位置和窗体大小，单位：像素

第二个创建容器，使用Container getContentPane() 返回容器对象

* `void setFont(Font f)` 设置此容器的字体。  
* `void setBeckgroud(color.颜色)`    设置窗体背景颜色
* `void add(组件对象)`    添加组件对象
* `void remove(组件对象)`    删除组件对象
* `void validate()`     验证此容器及其所有子组件(比较耗时间，建议全部组件都添加好后再来测试)
* `void setResizeable(Boolean TF)`    设置窗体释放可以改变，true表示可以改变 

开发中一般使用一个类去继承JFrame这个父类（就是让这个类也成为窗体），然后不需要实例化JFrame对象

#### swing_JDialog（对话框）

继承了窗体，可以使用窗体的方法

常用方法：

* `void setVisible(Boolean TF)`     设置窗口可见
* `setTitle(string name)` 设置窗体标题
* `setBounds(int long, int witch ,int long, int witch)`    设置坐标位置和窗体大小，单位：像素
* `void setLayout(LayoutManager manager)`    设置窗体布局

如果要堵塞父窗体，具体步骤

* 创建一个按钮对象( new JButton("按钮"); )，
* 把按钮添加到容器( add()方法 )，
* 添加按钮对象的动作监听（ 按钮对象.addActionListener(new AbstractAction()）
* 使用内部类来实例化对话框，在里面实例化对话框对象，参数使用( new JFrame) 对象，建议在内部类的方法中来显示对话框窗体方法（void setVisible(Boolean TF)     设置窗口可见）
* 对话框类的构造方法调用参数（JFrame j)
* 使用JDialog类的JDialog(Frame owner, String title, boolean modal) 构造方法来堵塞父窗体
    * 第一个参数，父窗体对象
    * 第二个参数，对话框的标题
    * 第三个参数，是否堵塞父窗体

#### swing_JLabel（标签）

要在窗体容器中

构造方法：new JLabel（String name）参数为内容

常用方法: 

* `void  setText(string text)`   设置标签内容
* `void getText()`    打印标签内容
* `setFont（new Font(String name, int style, int size)）`  设置便签字体，样式，大小
* `setForegroud(Color. 颜色)`    设置字体颜色

#### swing_菜单栏

菜单栏组件添加到 JFrame 窗口后，在窗口的内容显示区域的顶部出现。实现一个菜单栏主要涉及三种类:

* **JMenuBar**  表示一个菜单栏。

*  **JMenu**  表示菜单栏上的一个一级菜单。


* **JMenuItem, JCheckBoxMenuItem, JRadioButtonMenuItem**

    三者分别表示 普通的子菜单、带复选框的子菜单、带单选按钮的子菜单，

注意：JCheckBoxMenuItem、JRadioButtonMenuItem、JMenu 继承自 JMenuItem。一个 JMenu 也可以当做是一个二级子菜单项，通过 JMenu 和 JMenuItem 之间的嵌套，可实现多级子菜单效果。

**JMenu**常用方法：

* 添加 子菜单 到 JMenu 中
    JMenuItem add(JMenuItem menuItem)
*  添加一个子菜单分割线
    void addSeparator()

**JMenuItem** 常用方法：

* 添加菜单被点击的监听器
    void addActionListener(ActionListener l)
* 设置修改键，使用键盘快捷键直接触发菜单项的动作
    void setAccelerator(KeyStroke keyStroke)
* 设置菜单的键盘助记符
    void setMnemonic(int mnemonic)

* 设置菜单显示的文本
    void setText(String text)
*  设置菜单显示的图标
    void setIcon(Icon defaultIcon)

**JCheckBoxMenuItem、JRadioButtonMenuItem** 常用方法:

*  设置 复选框/单选按钮 是否选中
    void setSelected(boolean b)
*  判断 复选框/单选按钮 是否选中
    boolean isSelected()
*  添加 复选框/单选按钮 状态被改变的监听器
    void addChangeListener(ChangeListener l)





#### swing_图片

要在窗体容器中

* 先设置一个标签对象（new JLabel()），

* 使用new  ImageIcon("图片路径")得到Icon对象，参数为图片路径加名字，
* 使用标签中的方法void setIcon(icon i) 来添加到标签，标签添加到容器

图片本身不能被设置大小，而且不会随着窗体改变而改变

### swing布局

#### swing布局——绝对布局(null)

概述：null

使用绝对布局的窗体通常都是固定大小，组件的位置和形状不会随着窗体改变而改变

void setLayout(null)    设置窗体为绝对布局

#### swing布局——流布局(FlowLayout)

概述：FlowLayout

流布局是从左到右排列，默认居中对齐；像流水一样，向某个方向流动，遇到阻碍就折回

void setLayout(new FlowLayout(参数，水平间距，垂直间距))    设置窗体为流布局

* `static int CENTER` 	居中对齐
* `static int LEFT`           左对齐
* `static int RIGHT`        右对齐

#### swing布局——边界布局(BorderLayout)

概述：

把一个窗体分为五个区域：东、西、南、北、中，注意添加组件时，需要添加指定区域，否则默认添加到中间区域（CENTER)，

`void setLayout(new BorderLayout())`    设置窗体为边界布局

添加至容器时还需要添加一个参数

* `void add（对象，BorderLayout.EAST);`        	//东边
* `void add（对象，BorderLayout.WEST);`           //西边
* `void add（对象，BorderLayout.SOUST);`         //南边
* `void add（对象，BorderLayout.NORTH);`        //北边
* `void add（对象，BorderLayout.CENTER);`       //中边

注意南北两边都是占一边，东西是不到顶的，同一个区域的组件会覆盖

#### swing布局——网格布局( )

概述：

可以把一个窗体划分为多个区域，每个区域空间都一样大

`void setLayout(new GridLayout(行数，列数，水平间距，垂直间距))`    设置窗体为边界布局，参数都是int类型，

#### swing布局——网格组布局（GridBagConstraints)

概述：

把一个页面分为多个区域，可以任意摆放里面的内容，但这样也会相较于前面的布局更为复杂

步骤：

* 创建网格组布局（new GridBagLayout）对象

* 让容器使用此布局，容器对象 . setLayout（网格组布局对象）

* 新建组件的约束对象new  GridBagConstrains
* 添加到容器中容器对象.add()

GridBagConstraints的常用方法

* `gridx,gridy`            组件所在位置
* `gridwidth,gridheight`      组件占用的行数和列数
* `anchor`      组件所在的方位
    * 东，南，西，北（E, S, W, N)
    * 东南，东北，西北，西南
* `fill`     组件的填充方式   三种填充方式
    * GridBagConstraints.HORIZONTAL;    // 水平填充
    * GridBagConstraints.VERTICAL;      // 垂直填充
    * GridBagConstraints.BOTH;          // 全填充
* `insets`    组件与单元格边缘的最小距离（需要创建对象 new insets()）
    * top 上边、left 左边、bottom 下边、right 右边
* `ipadx, ipady`      组件的首先大小
    * 正数表示大
    * 负数表示小
* ``       一个单元格的最大宽高

操作步骤：

* 创建窗体对象new JFrame()
* 创建容器对象void get ContentPane();
* 设置布局为网格组布局 setLayout（new GridBagLayout）
* 新建一个类，类中创建约束对象 new GridBagConstrains()
* 约束对象调用方法
* 添加到容器当中，void add(对象 ， 约束对象)

### swing——按钮（jButton）

构造方法:

* JButton(String text) 创建一个带文本的按钮。  
* sJButton(String text, Icon icon) 创建一个包含初始文本和图标的按钮。  

* JButton(Icon icon) 创建一个带图标的按钮。  

成员方法：

* void setSelected(boolean b) 设置按钮的状态。  
* void setIcon(Icon defaultIcon) 设置按钮的默认图标。 
* void setSelectedIcon(Icon selectedIcon) 设置按钮的选定图标。  
* void setText(String text) 设置按钮的文本。
* String getText() 返回按钮的文本。  
* void setModel(ButtonModel newModel) 设置此按钮表示的模型。 
* void setPressedIcon(Icon pressedIcon) 设置按钮的按下图标。 

#### swing——单选框和多选框(JRadioButton和JCheckBox)

单选框：继承了按钮的成员方法，也就是说可以直接使用按钮的方法

构造方法

* JRadioButton(String text) 创建具有指定文本的未选定单选按钮。  
* JRadioButton(String text, boolean selected) 创建具有指定文本和选择状态的单选按钮。
* JRadioButton(String text, Icon icon) 创建一个具有指定文本和图像的单选按钮，该按钮最初未被选中。
* JRadioButton(String text, Icon icon, boolean selected) 创建具有指定文本，图像和选择状态的单选按钮。  



复选框：继承了按钮的成员方法，也就是说可以直接使用按钮的方法

构造方法：

* JCheckBox(String text) 创建一个带有文本的最初未选中的复选框。  
* JCheckBox(String text, boolean selected) 创建一个带有文本的复选框，并指定它是否最初被选中 
* JCheckBox(String text, Icon icon) 使用指定的文本和图标创建最初未选中的复选框。  
* JCheckBox(String text, Icon icon, boolean selected) 创建一个带有文本和图标的复选框，并指定它是否最初被选中。  

#### swing——下拉框（JComboBox)

概述：继承了按钮的成员方法，也就是说可以直接使用按钮的方法

就如名字所说，添加下拉框

添加下拉框方法一：

* 创建下拉框对象new JComboBox()
* 添加对象中的方法void addItem（）方法，添加下拉框数据
* 添加到容器

添加下拉框方法二

* 创建一个数组对象，数组中的数据为下拉列表数据

* 创建下拉框对象new JComboBox(参数)，参数为数组对象
* 添加到容器

添加下拉框方法三：下拉列表框模型

* 创建下拉框对象new JComboBox()
* 创建一个数组对象，数组中的数据为下拉列表数据
* 创建下拉框模型对象new ComboBoxModel（参数），参数为数组对象
* 下拉框对象方法void setModel(参数)，参数为下拉框模型对象
* 添加到容器

### swing——列表框（JList）

添加方法一：

* 创建一个数组对象，数组中的数据为下拉列表数据
* 创建列表框对象new JList(参数)，参数为数组对象

添加方法二：列表框模型

* 创建一个数组对象，数组中的数据为下拉列表数据
* 创建列表框模型对象, new DefaultListModel<>()
* 使用增强for循环来遍历数组元素，在循环中使用addElement()来添加到列表框模型中
* 创建列表框对象new JList，使用它的setModule( 参数 )方法，参数为列表框模型

设置选择模式：列表框对象 . setSelectionMode(ListSelectionMode.模式)

* 第一种模式（单选）：SINGLE_SELECTION
* 第二种模式（邻选）：SINGLE_INTERVAL_SELECTION
* 第三种模式（随便选）：MULTPLE_INTREVAL_SELECTCTION

### swing——滚动框（JScrollPane）

添加滚动框：new JScrollPane(参数) ，参数为列表框对象

注意：你添加了滚动框，就不用设置列表框的大小了，直接使用滚动框的setbounds方法

得到列表框的元素方法：getSelectedValuesList(),返回一个list集合

### swing——文本框（JTextField）

概述：

一个输入框

常用方法：

* void setColumns(int columns) 设置此文本框长度，然后使布局无效。 
* void setFont(Font f) 设置当前字体。 
* void setText() 设置文本
* string getText() 得到文本
* void removeNotify()  获得光标

### swing——密码框（JPasswordField）

概述：

看不见的输入框

常用方法：

* void setColumns(int columns) 设置此文本框长度，然后使布局无效。 
* void setFont(Font f) 设置当前字体。 
* void setEchoChar(char c) 设置此 JPasswordField的回显字符。 
* char[] getPassword() 返回此 TextComponent包含的文本。  
* void setText() 设置文本

* string getText() 得到文本
* void removeNotify()  获得光标

### swing——文本域

概述：

JTextArea是一个显示纯文本的多行区域

常用方法：

* void setRows(int rows) 设置此TextArea的行数。  
* void setFont(Font f) 设置当前字体。  
* void setColumns(int columns) 设置此TextArea的列数。 
* void setText() 设置文本（如果在设置则覆盖）
* void addend(string name) (追加内容)
* void insert(String str, int pos) 在指定位置插入指定的文本。 

### Swing——监听和事件

* KeyLisetener				键盘监听

    * keyEvent				键盘事件

    

* MonuseListener           鼠标监听

    * MouseEvent		   鼠标事件

    

* WindowListener           窗体监听

    * WindowEvent		窗体事件

    

* ActionListener              动作监听

    * ActionEvent			动作事件

#### swing——动作事件监听器

使用组件中的addActionListener（new ActionListener）方法，来添加动作监听

步骤：

* 创建要监听的组件
* 使用组件的addActionListener()方法
* 在方法中使用匿名内部类形式来监听对象
* 里面的内容由你自己来编写

#### swing——焦点事件监听器

使用组件中的addFocusListener (new FocusListener())方法，来添加焦点监听

方法一：

* 常见要监听的组件
* 使用组件的addFocusListener方来创建FoucusListener对象
* 在方法中使用内部类来监听对象
* 内部类中有两个成员方法
    * focusGained（FocusEvent e）  得到焦点时的动作
    * focusLost   (FocusEvent e)      失去焦点时动作