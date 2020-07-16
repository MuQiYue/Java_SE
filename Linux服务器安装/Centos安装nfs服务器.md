## linux安装nfs服务器

### 1、检查是否安装nfs服务

检查系统是否安装nfs服务

```bash
rpm -qa | grep nfs-utils
rpm -qa | grep rpcbind 
```

### 2、安装nfs服务

安装nfs服务

```
yum -y install rpcbind nfs-utils
```

### 3、启动nfs服务

```bash
查看状态
systemctl status rpcbind.service
systemctl status nfs.service

启动nfs服务
systemctl start rpcbind.service
systemctl start nfs.service
```

### 4、配置nfs服务器

7 配置简单，只需配置/etc/exprots文件，启动服务即可，但Centos7默认没有exports文件，需要手动添加

```
格式：
共享目录 [客户端1 (参数)] [客户端2 (参数)]
1、共享目录：nfs服务器需要共享的实际路径（绝对路径）
2、客户端：可以是指定IP地址，网段，域名和*（星号表示为所有网络）
3、参数(分为三种，访问权限参数、用户映射参数、其他参数)
	访问权限：ro  设置共享目录为只读
			rw  设置共享目录为可读写
	用户映射：all_squash  将远程访问的所有普通用户和用户组映射为匿名用户或用户组
			no_all_squash  不将远程访问的所有普通用户和用户组映射为匿名用户或用户组（默认）
			root_squash  将root用户及所属用户组都映射为匿名用户或用户组（默认）
			no_root_squash  不将root用户及所属用户组都映射为匿名用户或用户组
			anonuid = xxx  将远程访问的所有用户映射为匿名用户，并指定该匿名用户账号为本地用户账号（UID = XXX）
			anongid = xxx  将远程访问的所有用户组映射为匿名用户组账号，并指定该匿名用户组账号为本地用户组账号（GID = 								XXX）
	其他参数：secure  限制客户端只能从小与1024的TCP/IP端口连接nfs服务器(默认)
			insecure  不限制客户端只能从小与1024的TCP/IP端口连接nfs服务器
			sync  将数据同步写入内存缓冲区域磁盘中，效率较低，但可以保证数据的一致性
			async  将数据先保存在内存区，必要时写入磁盘
			wdelay  检查是否相关的写操作，如果有则将这些写操作一起执行，可以提高效率（默认）
			no_wdelay  若有写操作则立刻执行，应与sync配合使用
            subtree_check  若输出目录是一个子目录，则nfs服务器将检查父目录的权限（默认）
			no_subtree_check  即使输出是一个子目录，也不会去检查权限
```

### 5、配置nfs客户端

​		nfs客户端可以使用showmount命令查看nfs服务器上有哪些共享目录，使用前该命令前建议关闭防火墙或者设置防火墙的过滤规则，同时将selinux设置为允许

```
格式：
showmount [选项] （参数）
	-d: 仅显示已被nfs客户端加载的共享目录
	-e: 显示nfs服务器上所有的共享目录
```



















   