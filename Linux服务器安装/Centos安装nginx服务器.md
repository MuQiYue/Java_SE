## Centos安装nginx服务器

### 1、安装依赖包

```bash
yum -y install gcc zlib zlib-devel pcre-devel openssl openssl-devel
```

### 2、下载并解压压缩包

```bash
// 建立一个文件夹
cd /usr/local
mkdir nginx
// 下载tar包
wget http://wget http://nginx.org/download/nginx-1.18.0.tar.gz
tar -xvf nginx-1.18.0.tar.gz
```

### 3、安装nginx

```bash
//进入Nginx文件夹
cd nginx-1.18.0
//执行下列命令
./configure
make
make install
```

### 4、检查安装

```bash
// 进入配置的安装目录
cd /usr/local/nginx
./sbin/nginx -t
```

正常情况的信息输出：

nginx: the configuration file /usr/local/nginx/conf/nginx.conf syntax is ok
nginx: configuration file /usr/local/nginx/conf/nginx.conf test is successful

### 5、启动nginx

```
// 进入nginx文件夹
cd /usr/local/nginx/nginx-1.18.0/sbin
// 启动nginx
./nginx
```

### 6、配置开机启动

#### 6.1、先停止nginx服务

```bash
// 停止服务
nginx /usr/loacl/nginx/sbin/nginx -s stop
```

#### 6.2、创建脚本文件

```bash
vim /etc/init.d/nginx
```

#### 6.3、添加相关数据

```
#! /bin/bash
# chkconfig: - 85 15
PATH=/usr/local/nginx				// 环境变量
DESC="nginx daemon"			
NAME=nginx							// 名字
DAEMON=$PATH/sbin/$NAME				// 修改成nginx执行程序的路径
CONFIGFILE=$PATH/conf/$NAME.conf	// 修改成配置文件的路径
PIDFILE=$PATH/logs/$NAME.pid
SCRIPTNAME=/etc/init.d/$NAME
set -e
[ -x "$DAEMON" ] || exit 0

do_start() {
    $DAEMON -c $CONFIGFILE || echo -n "nginx already running"
}

do_stop() {
    $DAEMON -s stop || echo -n "nginx not running"
}

do_reload() {
    $DAEMON -s reload || echo -n "nginx can't reload"
}

case "$1" in
    start)
        echo -n "Starting $DESC: $NAME"
        do_start
        echo "."
    ;;
    stop)
        echo -n "Stopping $DESC: $NAME"
        do_stop
        echo "."
    ;;
    reload|graceful)
        echo -n "Reloading $DESC configuration..."
        do_reload
        echo "."
    ;;
    restart)
        echo -n "Restarting $DESC: $NAME"
        do_stop
        do_start
        echo "."
    ;;
    *)
        echo "Usage: $SCRIPTNAME {start|stop|reload|restart}" >&2
        exit 3
    ;;
esac
exit 0
```

#### 6.4、添加执行权限

```bash
chmod a+x /ext/init.d/nginx
```

#### 6.5、启动和关闭自启

```bash
/etc/init.d/nginx start
/etc/init.d/nginx stop
```

