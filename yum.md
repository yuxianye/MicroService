# 设置yum源

1、把yum更新到最新

yum update



2、设置yum源（选择其中一个）

中央仓库

yum-config-manager --add-repo http://download.docker.com/linux/centos/docker-ce.repo

阿里仓库

yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo





