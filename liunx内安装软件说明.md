### Linux内安装软件的常用命令以及下载说明

#### apt-get install 或者 apt install

- 下载的软件存放位置：/var/cache/apt/archives

  可使用命令删除安装缓存： sudo apt-get autoclean（只删除低版本的deb包）

  ​											   sudo apt-get clean（全部删除）

- 一般的deb包默认安装位置有：/url/share，/usr，/usr/local

  查看具体安装的位置命令：dpkg -L XXX.deb （xxx是deb包的名称）

  dpkg -L firefox 可查看Firefox的安装位置；dpkg -L eclipse 可查看Eclipse的安装位置

- 可执行文件的位置：/usr/bin

- 配置文件位置：/etc

- lib文件位置：/usr/lib

- 更新软件包列表：sudo apt-get update

- 更新已安装的软件：sudo apt-get upgrade