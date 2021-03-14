### 修改apt下载源

1. 首先备份之前的源：sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

2. 在修改之前查看一下系统版本：lsb_release -a

3. 打开源文件进行修改：sudo vim /etc/apt/sources.list

   通过lsb_release -a可以查看版本的codename，每个版本不一样，关联的源也不同，不然后续会出现apt依赖问题

   \#Ubuntu 18.04是 bionic
   deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse 
   deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse 
   deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse 
   deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse 
   deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse 
   deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse 
   deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse 
   deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse 
   deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse

   

   \# Ubuntu 20.04是 focal
   deb http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
   deb-src http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
   deb http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
   deb-src http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
   deb http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
   deb-src http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
   deb http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
   deb-src http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
   deb http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
   deb-src http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
   
4. 更新软件列表：sudo apt-get update

5. 更新软件包：sudo apt-get upgrade

