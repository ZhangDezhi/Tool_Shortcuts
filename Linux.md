


## 命令搜集
```bash
$ rmdir        # 删除空目录
$ ps aux       # 查看系统进程
$ kill -9 pid  # 杀死进程
$ w            # 显示在线用户

$ wc           # 统计文件
$ df           # 查看系统硬盘信息
$ free         # 查看系统内存信息
$ halt         # 关闭计算机

##ls
$ ls -a  # 查看所有文件
$ ls -l  # 查看详细信息
$ ls -lh # 文件大小显示为M

##查看内存
$ du                  # 显示目录下各个文件磁盘占用情况
$ du -s               # 显示目录下所有文件的大小
$ df -h               # 这个命令用于查看服务器空间
$ du -h --max-depth=1 # 这个命令用于查看当前目录，哪个文件占用最大
$ du -sh *            # 这个命令也用于查看当前目录下各文件及文件夹占用大小


## gui和cli切换 
$ init 5   #进入图形化界面
$ init 3   #进入命令介面

## 查看已安装的中文字体

$ fc-list :lang=zh


```


### 查看ascii

```bash
$ man 7 ascii
   Tables
       For convenience, let us give more compact tables in hex and decimal.

          2 3 4 5 6 7       30 40 50 60 70 80 90 100 110 120
        -------------      ---------------------------------
       0:   0 @ P ` p     0:    (  2  <  F  P  Z  d   n   x
       1: ! 1 A Q a q     1:    )  3  =  G  Q  [  e   o   y
       2: " 2 B R b r     2:    *  4  >  H  R  \  f   p   z
       3: # 3 C S c s     3: !  +  5  ?  I  S  ]  g   q   {
       4: $ 4 D T d t     4: "  ,  6  @  J  T  ^  h   r   |
       5: % 5 E U e u     5: #  -  7  A  K  U  _  i   s   }
       6: & 6 F V f v     6: $  .  8  B  L  V  `  j   t   ~
       7: ? 7 G W g w     7: %  /  9  C  M  W  a  k   u  DEL
       8: ( 8 H X h x     8: &  0  :  D  N  X  b  l   v
       9: ) 9 I Y i y     9: ?  1  ;  E  O  Y  c  m   w
       A: * : J Z j z
       B: + ; K [ k {
       C: , < L \ l |
       D: - = M ] m }
       E: . > N ^ n ~
       F: / ? O _ o DEL

    左侧为 16 进制，0-F：表示低位，2-7：高位；
    右侧为 10 进制，0-9：表示低位，30-120：高位；
```




```bash
# 有些时候查询大于多少M的文件时候需要显示文件大小，组合命令如下
$ find /opt/ -size +1G -exec ls -lh {} \;

#查找所有的core文件
find ~/ -name "core.[0-9]???"

#查找&显示文件大小
find ~/ -name "core.[0-9]???" -exec ls -lh {} \;

```


图元文件
 /home/mas/uif/element/patrolGroup


 将命令输出作为输入
 ```bash
 #方法1 是用 ``
 #方法2 使用xargs

#查看日期
$ date +%Y-%m-%d,%H:%m:%s

#查找某天修改的文件
$ find . -maxdepth 1 -newermt "2016-12-06"
$ find . -maxdepth 1 -newermt "12/06/16"
$ find . -maxdepth 1 -newermt "12/06/2016"
$ find . -maxdepth 1 -newermt  `date +%Y-%m-%d`

#将某天修改的文件复制到桌面
$ cp ` find . -maxdepth 1 -newermt "2020-05-15"` ~/Desktop/
$ cp ` find ~/lib/ -maxdepth 1 -newermt $(date +%Y-%m-%d)` ~/Desktop/


 ```



### ftp 




## 安装程序(RHEL)

```bash
## 安装vscode
$ rpm --import https://packages.microsoft.com/keys/microsoft.asc
$ sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
$ yum check-update
$ sudo yum install code

## 安装git相关命令
$ yum install gitg    #一个图形化客户端
$ yum install git-gui 
$ yum install gitk
$ yum install git-svn

## 安装xfce


## 
$ yum install dconf-editor  #gnome2 的 “注册表编辑器
$ yum install gconf-editor  #gnome2 的 “注册表编辑器(新)
$ yum install ntfs-3g       #读取ntfs硬盘
$ yum -y install alacarte   #自定义应用程序快捷方式

##

$ yum install gnome-tweak-tool
# https://extensions.gnome.org/
##

## 安装rar工具
wget http://rarlab.com/rar/rarlinux-x64-5.1.1.tar.gz
tar -zxvf rarlinux-x64-5.1.1.tar.gz
cd rar
su root
make
make install
```
