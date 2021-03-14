### windows自带的linux子系统(WSL)  使用 vncview连接wsl桌面

自行安装桌面程序（xfce4等）

安装tigervnc服务：sudo apt install tightvncserver

修改配置文件：一般会先备份一下原来的配置文件  cp ~/.vnc/xstartup ~/.vnc/xstartup.bak

​						  打开配置文件xstartup，打开相应的注释，添加一行 startxfce4 &  （这里是跟安装的桌面程序有关）

启动vnc服务：vncserver -geometry 1440x900 :0      

​						 vncserver -geometry 1440x900 :1

​						端口号默认从5900开始，0代表5900, 1代表5901，依次类推

关闭vnc服务：vncserver -kill :0

​						 vncserver -kill :1

vncview.exe启动连接，127.0.0.1:5900