ctrl + ⇧+ c  复制

ctrl + ⇧ + v   粘贴



F11 全屏

## rpm

```bash
$ rpm -i example.rpm    # 安装
$ rpm -iv example.rpm   # 安装 包并在安装过程中显示正在安装的文件信息；
$ rpm -ivh example.rpm  # 安装 包并在安装过程中显示正在安装的文件信息及安装进度；

$ rpm -qa | grep jdk    #查看已经安装软件
$ rpm -e --nodeps java-1.6  #卸载软件

$ rpm -ivh python27-2.7.9-1.x86_64.rpm --replacefiles
$ rpm -ivh  --force  demo.rpm
```

## yum

```bash.shortcuts
$ yum search  example   #查找包
$ yum list   #列出所有的安装包
$ yum list updates  #列出所有可更新包
$ yum list installed #列出所有已安装的包
$ yum list extras   #列出所有不在 Yum Repository 内的软件包
$ yum info     #获取软件包信息

$ yum -y remove python-2.7.5-76.el7.x86_64  #卸载包

```





## 操作

Shift + 双击文件夹   | 在本文件夹内打开.  (默认是在新窗口打开)
backspace | 返回上层目录
Shift + backspace  | 在本文件夹内 返回上层目录

Ctrl + shift + 上/下    开启虚拟桌面.然后左右移动进行切换



```bash
gnome-screensaver-command -l   #锁屏

```