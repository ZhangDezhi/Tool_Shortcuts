# svn 快捷操作查询

>
[文件标志意思]
```
- A：add，新增
- C：conflict，冲突
- D：delete，删除
- M：modify，本地已经修改
- G：modify and merGed，本地文件修改并且和服务器的进行合并
- U：update，从服务器更新
- R：replace，从服务器替换
- I：ignored，忽略
- ? ：文件、目录或是符号链item不在版本控制之下
- ! ：文件、目录或是符号链item在版本控制之下，但是已经丢失或者不完整，这可能因为使用非Subversion命令删除造成的，如果是一个目录，有可能是检出或是更新时的中断造成的，使用svn update可以重新从版本库获得文件或者目录，也可以使用svn revert file恢复原来的文件。
- I ：忽略文件、目录或是符号链 (svn status --no-ignore 可以查看到  
```

## 基本命令

``` bash
## 检出
$ svn co 
$ svn checkout svn://192.168.0.1/runoob01 -r101
$ svn checkout svn://192.168.0.1/runoob01 --username=user01

# 查看路径下目录
$ svn ls
$ svn list http://svn.test.com/svn     #查看目录中的文件。
$ svn list -v http://svn.test.com/svn  #查看详细的目录的信息(修订人,版本号,文件大小等)。
$ svn list [-v]                        #查看当前当前工作拷贝的版本库URL。

#比较文件差异
$ svn di
$ svn diff               #什么都不加，会坚持本地代码和缓存在本地.svn目录下的信息的不同;信息太多，没啥用处。
$ svn diff test.php   #将修改的文件与基础版本比较
$ svn diff -r 3          #比较你的本地代码和版本号为3的所有文件的不同。
$ svn diff -r 3 text.c   #比较你的本地代码和版本号为3的text.c文件的不同。
$ svn diff -r 5:6        #比较版本5和版本6之间所有文件的不同。
$ svn diff -r 200:201 test.php #对版本m和版本n比较差异
$ svn diff -r 5:6 text.c #比较版本5和版本6之间的text.c文件的变化。

$ svn status   查看工作副本的状态
$ svn add     将新建的文件添加到版本控制

## 提交
$ svn ci
$ svn commit -m "SVN readme."     # -m后面是本次提交的说明

# 加锁
$ svn lock -m “LockMessage“ [--force] PATH
$ svn unlock PATH

## 更新
$ svn up
$ svn update
$ svn up -r 版本号  文件名
$ svn up -r 123

## 版本回退
$ svn revert file
$ svn revert -R dir_name    #代码回滚到修改前状态
$ svn revert --depth=infinity .   # 忽略整个文件夹修改
$ svn revert DIR --depth=infinity

## 查看历史
### TortoiseSVN 无法显示日志,需要清理缓存. (另外,使用ver1.9.x版本最好)
### settings->saveDate->log message
$ svn log                              # 显示所有日志(版本、作者、日期、comment)
$ svn log -r                           # xxx 显示某一个版本信息
$ svn log -r 4:20 #只看版本4到版本20的日志信息，顺序显示。
$ svn log -r 20:5 #显示版本20到4之间的日志信息，逆序显示。
$ svn log -r {2020-04-06}:{2020-06-01} # 显示日期之间的版本信息
$ svn log test.c  #查看文件test.c的日志修改信息。
$ svn log -r 8 -v #显示版本8的详细修改日志，包括修改的所有文件列表信息。
$ svn log -r 8 -v -q   #显示版本8的详细提交日志，不包括comment。
$ svn log -v -r 88:866 #显示从版本88到版本866之间，当前代码目录下所有变更的详细信息 。
$ svn log -v dir  #查看目录的日志修改信息,需要加v。
$ svn log http://foo.com/svn/trunk/code/  #显示代码目录的日志信息。
$ svn log XXX.lib
$ svn log https://svn/xxx.lib
$ svn log -l  n   #显示日志条数
$ svn log -l N -v =>  # 查看每条日志提交详情


$ svn cat                              # 取得在特定版本的某文件显示在当前屏幕。
$ svn cat -r 4 test.c      #查看版本4中的文件test.c的内容,不进行比较。

$ svn info  # 查看当前代码录路径
$ svn info test.php


#删除文件
$ svn del/remove/rm
$ svn delete path -m "delete test fle"


#合并 合并分支
$ svn merge -r 200:205 test.php  #(200和205之间差异合并到当前文件夹)
$ svn merge 代码源路径链接
$ svn merge --reintegrate 分支链接

#帮助
$ svn help     #查看全部功能
$ svn help ci  #查看提交功能


#  代码库URL变更
$ svn switch (sw): 更新工作副本至不同的URL。


## 导出文件
$ svn export -r 2232 http://127.0.0.1/svn/project001    #默认为最新
$ svn export -r 123 http://127.0.0.1/svn/project  目标路径/    ## 导出(不包含.svn)
$ svn export -r 123 http://127.0.0.1/svn/project ~/Desktop --username Zhangdezhi

## 补丁使用
### -p0 从当前目录查找目录文件(夹)
### -p1 从当前目录查找目的文件,不包含patch中的最上级文件(夹)
$ svn diff > out.patch   #生成补丁 .patch / .diff
$ svn diff abc.cpp > out.patch 
$ patch -p0 < out.patch  #应用补丁

## 创建分支
# >  trunk分支 (主分支)
# >  branch分支 (开发)
# >  tag分支(归档分支) 不允许修改,用于回滚
$ svn cp -m"操作说明"  源分支链接 新分支链接路径
```

## 钩子 


## 忽略文件设置
>
修改 /用户名/.subversion/config
打开 global 注释 ，并添加如下：
global-ignores = *.o *.lo *.la *.al .libs *.so .so.[0-9] *.pyc *.pyo *.rej .DS_Store *.xcuserstate *.xcworkspace .xcuserdatad .xcscmblueprint ~ ## .# ..swp


## 快捷命令
```bash
$ find . -name ".svn" -exec rm -rf {} \;   #删除.svn目录
```
