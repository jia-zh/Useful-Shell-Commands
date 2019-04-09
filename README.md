# Useful Shell Commands
[![](https://img.shields.io/badge/update-anytime-success.svg)](https://github.com/jia-zh/Useful-Shell-Commands)
  
一些常用的Shell命令长时间不用了总会忘记，收集以备查询

- [Linux Commands](#linux-commands)
- [About nohup](#about-nohup)
- [About Vim](#about-vim)
- [About Git](#about-git)
- [About Anaconda](#about-anaconda)
- [About Redis](#about-redis)

### Linux Commands
```shell
# 统计test.txt行数
cat test.txt |wc -l
wc -l test.txt

# 将一个大文件拆分为多个文件
# 文件拆分为大小为2G，拆分文件的前缀为test.tar.gz. ，默认拆分为test.tar.gz.aa,ab,ac...
cat test.tar.gz | split -b 2G - test.tar.gz.

# 将多个拆分的文件合并为一个文件
cat test.tar.gz.a* > test.tar.gz
```

### About nohup
```shell
# 提交后台运行作业
nohup command > log 2>1& &

# 查看当前有多少在后台执行的命令
jobs

# 将后台中的命令调至前台继续执行。
fg %jobnumber（是命令编号，不是进程号）
```

### About Vim
![](https://raw.githubusercontent.com/jia-zh/Useful-Shell-Commands/master/images/vim%20command.png)

### About Git
```shell
克隆项目
git clone git@github.com:jia-zh/Useful-Shell-Commands.git

提交修改到暂存区
git add -A

提交修改
git commit -m "Initial commit"

提交修改到仓库
git push

```

### About Anaconda
```shell
查看安装了哪些包
conda list

查看当前存在哪些虚拟环境
conda env list 或 conda info -e

检查更新当前conda
conda update conda

命令虚拟环境
conda create -n env_name python=X.X  X.X（2.7、3.6等）为python版本、env_name为虚拟环境名字

激活虚拟环境
source activate env_name

删除env_name环境及下属所有包
conda remove -n env_name --all

退出虚拟环境
source deactivate

Anaconda中虚拟cuda9.0环境
conda install -c anaconda cudatoolkit=9.0
conda install -c anaconda cudnn=7.1.2
```


### About Redis
- 安装
```shell
解压
tar -zxvf redis-5.0.0.tar.gz
进入目录
cd redis-5.0.0/
执行make 对Redis解压后文件进行编译
make
编译完成之后，可以看到解压文件redis-5.0.0中会有对应的src、conf等文件夹
编译成功后，进入src文件夹，执行make install进行Redis安装
cd src
make install
```
- 基本设置
```shell
创建bin文件夹，将redis-server、redis-cli、redis.conf 放到此文件夹下，便于后面命令的执行
cd /redis     进入redis目录下
mkdir bin 

mv redis.conf bin  移动，防止运行时运行到默认配置 所以建议保存一个配置信息
mv src/redis-server bin
mv src/redis-cli bin
```

- 设置redis 外网访问
```shell
vim redis.conf
将 bind 127.0.0.1 注释掉 
设置 protected-mode 为no 
```

- 后台启动redis服务
```shell
编辑conf文件，将daemonize属性改为yes（表明需要在后台运行）
vim redis.conf

再次启动redis服务，并指定启动服务配置文件
redis-server /usr/local/redis/etc/redis.conf
```

- 配置redis log文件路径和数据文件路径
配置log文件路径是为了方便查看log
配置数据文件路径是因为redis启动时会直接在当前目录下创建数据文件，当下次启动时路径不一样的话数据就回丢失
```shell
vim redis.conf

# logfile ""
# 修改为如下，意思为把log文件放在redis安装目下logs/redis.log(要自己创建好目录结构)
logfile "/home/zhengjia/redis-5.0.0/log/redis.log"

# The working directory.
# dir ./
dir /home/zhengjia/redis-5.0.0/data
```

- 关闭Redis服务
```shell
./redis-cli shutdown
```
