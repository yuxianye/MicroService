# 安装配置Redis

1、redis是C语言开发说以先安装gcc环境

yum install -y gcc



2、下载redis安装包

wget http://download.redis.io/releases/redis-5.0.9.tar.gz

或则直接下载然后用xftp拷贝到root目录



3、解压

tar -zxvf redis-5.0.9.tar.gz



4、cd切换到redis解压目录下，执行编译

 cd redis-5.0.9

make



5、安装并指定安装目录
make install PREFIX=/usr/local/redis



6、启动

6.1、前台启动
 cd /usr/local/redis/bin/
 ./redis-server



6.2、后台启动
从 redis 的源码目录中复制 redis.conf 到 redis 的安装目录
 cp /usr/local/redis-5.0.3/redis.conf /usr/local/redis/bin/

修改 redis.conf 文件，把 daemonize no 改为 daemonize yes

./redis-server redis.conf



7、设置开机启动
添加开机启动服务
vi /etc/systemd/system/redis.service
复制粘贴以下内容：

[Unit]
Description=redis-server
After=network.target
[Service]
Type=forking
ExecStart=/usr/local/redis/bin/redis-server /usr/local/redis/bin/redis.conf
PrivateTmp=true
[Install]
WantedBy=multi-user.target

注意：ExecStart配置成自己的路径 



7、启动服务并设置开启启动

systemctl start redis.service
systemctl enable redis.service



8、如果需要远程访问，开启6379端口

firewall-cmd --zone=public --add-port=6379/tcp --permanent