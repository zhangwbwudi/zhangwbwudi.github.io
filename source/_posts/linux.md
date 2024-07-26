---
title: linux
author: 蜗牛
coverImg: /medias/banner/6.jpg
top: true
cover: false
toc: true
mathjax: false
summary: linux常用命令
tags:
  - PicGo
  - GitHub图床
categories:
  - linux
abbrlink: 7f1ae6do
reprintPolicy: cc_by
date: 2020-03-15 00:00:00
img:
password:
---
## 目录结构

bin sbin etc home usr root tmp

## vim快捷键

![image-20230425191658866](../images/typora-user-images/image-20230425191658866.png)

## 关机和重启的命令

```bash
shutdown -h now			立刻进行关机
shutdown -h 1			”hello，1分钟后会关机了“
shutdown -r now			现在重新启动计算机
halt					关机
reboot					重新启动
syn					把内存的数据同步到磁盘
```

> 注意：目前的shutdown/reboot/halt 等命令均已经在关机前进行了sync，但是在执行关机或重启前sync一下，小心驶得万年船

## 用户管理

> 用户切换

```bash
[halo@zwb-lucky root]$ su root
Password: 
[root@zwb-lucky ~]#
```

su - 用户名“**命令来切换**

**注意**

1.从权限高的用户切换到权限低的用户时，不需要输入密码，反之需要

2.当需要返回到原来用户时，使用exit/logout指令

> 添加用户

- 基本语法

```bash
useradd 用户名
```

- 实列(root权限下)

```bah
useradd hucheng
添加一个用户chucheng，默认该用户的家目录在/home/hucheng
```

- 细节说明

```
1、当用户创建成功后果，会自动的创建和用户同名的家目录
2、也可以通过useradd -d 指定目录  新的用户名     来给新创建的用户指定家目录
12
```

![在这里插入图片描述](../images/typora-user-images/20210620104231917.png)

```bash
新建用户zhanzhiwen的home目录下的文件夹名称是muluming
```

> 指定/修改密码

```bash
passwd 用户名	
```

注意：修改密码要在root下

```bash
[zhangsan@zwb-lucky home]$ passwd zhangsan
passwd: Only root can specify a user name.
```

> 删除用户

```bash
userdel   用户名
userdel -r 用户名
```

> 查询用户信息指令

```bash
id 用户名
```

```bash
[root@zwb-lucky ~]# id root
uid=0(root) gid=0(root) groups=0(root)
[root@zwb-lucky ~]# id halo
uid=1000(halo) gid=1000(halo) groups=1000(halo),10(wheel)
```

> 查看当前用户/登录用户

```bash
whoami/who am i
```

> 用户组

类似于角色，系统可以对有共性/权限的多个用户进行统一的管理

新增组

```bash
指令：groupadd 组名
```

删除组

```bash
指令（基本语法）：groupdel 组名
```

注意：如果当添加用户时没有指定组，会默认创建和这个**用户同名的组**，同时把用户放到该组里

增加用户时直接加上组

```bash
指令：useradd -g 用户组 用户名
```

移动组

```bash
usermod -g 组名 用户名
```

## 运行级别说明：

0：关机

1：单用户【找回丢失密码】

2：多用户状态没有网络服务

3：多用户状态有网络服务

4：系统未使用保留给用户

5：图形界面

6：系统重启

常用运行级别是3和5，也可以指定默认运行级别

## 帮助指令

- man获得帮助信息

```bash
基本语法：man [命令或配置文件]（功能描述：获得帮助信息）
```

在linux下隐藏文件是以 “.” 开头的

- help指令

```bash
基本语法：help 命令 （功能描述：获得shell内置命令的帮助信息）
```

## 文件目录类

- pwd指令

```
基本语法：pwd    （功能描述：显示当前工作目录的绝对路径）
```

- ls指令

```
基本语法：ls [选项] [目录或是文件]
```

常用选项

-a ： 显示当前目录所有的文件和目录，包括隐藏的

-l ： 以列表的方式显示信息

- cd指令

```
基本语法：cd [参数] （功能描述：切换到指定的目录）
```

理解：绝对路径和相对路径（相对路径是针对当前位置的路径）

cd ~ 或者cd 回到自己的家目录

cd … 回到当前目录的上一级目录

- mkdir指令

```
基本语法：mkdir [选项] 要创建的目录
```

理解：mkdir指令用于创建目录（默认只能创建一级目录）

-p :创建多级目录

- rmdir指令（用于删除空目录）

```
基本语法：rmdir [选项] 要删除的空目录
```

使用细节：

rmdir删除的是空目录，如果欲删除的目录下有内容则无法删除

==如果需要删除非空目录，需要使用rm -rf 要删除的目录

- touch指令（用于创建空文件）

```
touch 文件名称
```

- cp指令（copy拷贝文件导指定目录）

```
cp [选项] source dest
```

常用选项：-r 递归复制真个文件夹

应用实例:

```bash
将 /home/hello.txt 拷贝到 /home/bbb 目录下
cp /home/hello.txt /home/bbb
递归复制整个文件夹，将/home/aaa 目录下的文件全部拷贝到/home/bbb下
cp -r /home/aaa /hom/bbb
(是将整个目录和目录本身拷贝进来)
```

- rm指令（remove，移除文件或目录）=一定要小心！！！

```
基本语法：rm [选项] 要删除的文件或目录
```

常用选项

-r : 递归删除整个文件夹

-f ：强制删除不提示

使用细节：强制删除不提示的方式，带上-f参数即可

- cat指令（查看文件内容）

```
cat [选项] 要查看的文件
```

常用选项： -n 显示行号

使用细节：cat只能浏览文件，而不能修改文件，为了浏览方便，一般会带上管道命令 |more

```
cat -n /etc/profile |more
```





输入到控制台

查看历史

过滤查找，带行号

