## Centos安装Samba服务器

### 概述：实现不同操作系统之间的文件和打印机共享

### 相关进程：smbd和nmbd两个进程组成

### 工作流程：

1、协议协商：客户端发送自身支持的所有smb协议版本，服务端选择最优的smb进行回应

2、建立连接：协议确定后，客户端发送认证给服务端，服务器选择允许或者拒绝本次连接

3、访问共享资源：客户端发送报文列出想要访问的网络资源，服务器端判断客户端是否拥有相关权限

4、断开连接：客户端向发送tree disconnect报文关闭共享，服务器端关闭连接

### Samba功能

1、文件和打印机共享

2、身份验证和权限设置

3、名称解析

4、浏览服务

### 安装samba服务器

#### 1、安装samba服务器

```bash
yum -y install samba
```

#### 2、samba服务器启动与停止

```
// 启动服务
systemctl start smb.service
// 停止服务
systemctl stop smb.service
// 重启服务
systemctl restart smb.service
// 重载服务
systemctl reload smb.service

# 开机自启
// 查看是否开机自启
systemctl list-unit-files | grep smb
// 设置开机自启
systemctl enable smb.service
// 关闭开机自启
systemctl disable smb.service

# 查看状态
systemctl status smb.service
active		// 开启状态
inactive 	// 关闭状态
```

### 配置samba服务器

#### 注意：文件存放在/etc/samba目录下，testparm命令可以测试配置文件的正确性

#### 1、全局变量

在smb.conf的配置文件中[global]部分为全局变量，其作用范围适用于samba服务器的所有共享资源

常用字段：

* workgroup（设置samba服务器的工作组）
    格式：workgroup = 工作组

* server string(注解)
    格式：server string = 说明

* hosts allow(允许哪个ip网段或者IP地址连接)

    格式：hosts allow = ip地址

* security (访问级别)

* 格式：security = 等级

    * share 客户端不需要提交用户名和密码即可访问共享资源
    * user 客户端需要提交用户名和密码，而且身份必须通过验证，验证通过即可访问共享资源
    * server 客户端需要提交用户名和密码，身份有samba服务器进行验证，验证失败则使用user级别访问

* passdb backend = tdbsam（把密码文件保存到数据库）

* encrypt passworks = yes/no(是否对samba进行加密)

* smb passwd file = 密码文件位置（设置密码文件位置）

#### 2、共享服务

默认开启本地家目录[home]和打印机[printer]的共享，也可以自行创建共享

常用的字段

* comment :注释说明

* path：共享资源的完整路径名称，除了要路径正确，相关目录的权限也要设置正确

* browseable: 设置浏览资源时是否显示共享目录，取值为"yes/no";
* public：设置是否允许匿名访问，取值为"yes/no",为no是进行身份验证
* read only :设置是否以只读的方式访问共享资源，取值“yes/no”

* writable: 设置共享目录是否允许用户写操作，取值”yes/no“

* write user: 设置允许指定的用户或者用户组访问共享资源
* write list :允许写操作的用户或者组

#### 3、日志与账户

日志文件默认存放在/var/log/samba目录下，每次连接都会分别建立日志文件，可以修改smb.conf文件来修改日志文件的存储位置和最大容量

log file = 设置日志文件的存储位置

max log size = 设置日志文件的最大容量，单位为kb

#### 4、密码文件

当客户端访问samba服务器是，用户提交的用户名和密码会和smbpasswd存放的信息对比，两者相同则允许访问

samba账号不能直接创建，必须存在对应的同名系统账号（意思是你要先添加相应的普通用户）

samba添加账号命令为smbpasswd ,格式为：smbpasswd -a 用户名

### linux客户端访问samba服务器

linux有两种方法

1、smbclient命令

格式为：smbclient -L 目的ip地址或者主机名 -U 用户名 @ 密码

2、mount命令

格式为：mount - t cifs //目标ip地址/共享目录名 挂载点 -o username = 用户名，password = 密码

### Windows客户端访问samba服务器

win + r 键打开“运行”，执行unc路径直接进行访问





