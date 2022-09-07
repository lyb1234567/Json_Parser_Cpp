# Rookie Linux
- [Link](#Link)
  - [Symlink](#symbolic-link软链接)
  - [Hardlik](#hard-link硬连接)
- [Manipulating Files And Directories](#manipulating-files-and-directories)



## Link
Linux文件系统中，有所谓的链接(link)，我们可以将其视为档案的别名，而链接又可分为两种 : 硬链接(hard link)与软链接(symbolic link)，硬链接的意思是一个档案可以有多个名称，而软链接的方式则是产生一个特殊的档案，该档案的内容是指向另一个档案的位置。硬链接是存在同一个文件系统中，而软链接却可以跨越不同的文件系统。
不论是硬链接或软链接都不会将原本的档案复制一份，只会占用非常少量的磁碟空间。

### Symbolic link(软链接)
1. 软链接，以路径的形式存在。类似于Windows操作系统中的快捷方式
2. 软链接可以 跨文件系统 ，硬链接不可以
3. 软链接可以对一个不存在的文件名进行链接
4. 软链接可以对目录进行链接

```shell
ln -s filename othername
```
比如说我有一个文件 **test**,我可以用上述命令行创建一个软连接 **test_link**，同样可以进入test文件，包括其内容，就类似于一种快捷方式。
我们使用```ls -l```查看所有内容，可以发现 **test_link** 是指向test文件的。
```shell
drwxr-xr-x  3 mirage mirage   4096 Sep  6 11:01  test
lrwxrwxrwx  1 mirage mirage      4 Sep  7 14:28  test_link -> test
```
其中第一列权限字符前面有个'l'字符，这就是 **link**标志。

### Hard link(硬连接)
- [ ] Description
- [ ] Implementation


## Manipulating Files And Directories
At this point, we are ready for some real work! This chapter will introduce the following commands:
- cp – Copy files and directories
- mv – Move/rename files and directories
- mkdir – Create directories
- rm – Remove files and directories
- ln – Create hard and symbolic links

**Wild card**
类似于正则表达式，可以在**shell**中匹配一个或者多个字符
| Wildcard      | Meaning |
| ----------- | ----------- |
| *      | Match any characters       |
| [character]   | Matches any character that is a member of the set characters|
| !characters   | Matches any character that is not a member of the set characters|
| [:class:]  | Matches any character that is a member of the specified class|

比如说，如果我们想将目录 **dir1**中所有文件移动到文件**dir2**中，那么我们可以使用命令 ```mv dir1/* dir2```.

同时我们也可以利用 wildcard进行大规模的同类型文件删除：
1.首先我们先创建几个txt: ```touch file1.txt file2.txt```
```
 CS_Self_Study
 Json_Parser
 Json_Parser_Cpp
 Linux_rookie
 file1.txt
 file2.txt
 gcc-3.4-ubuntu.tar.gz
 hit-oslab-linux-20110823.tar.gz
 json-tutorial
 project_2
 projects
 test
```
然后我们可以用wildcard 对目前所有含有txt后缀名的文本文件进行删除。
```rm *.txt```,其结果如下：
```
 CS_Self_Study
 Json_Parser
 Json_Parser_Cpp
 Linux_rookie
 gcc-3.4-ubuntu.tar.gz
 hit-oslab-linux-20110823.tar.gz
 json-tutorial
 project_2
 projects
 test
```

**命令行的结合使用**
在Linux 终端中，我们是可以结合不同的命令连续使用的。比如如果我们想看到目前文件夹中所有文件的属性。那么我们可以使用```ls -l```来进行查看。但是如果我们想让目前的内容以时间的先后顺序进行显示，那么我们可以使用命令```ls -lt```,其结果如下：
```
total 296
drwxr-xr-x  3 mirage mirage   4096 Sep  7 21:22  test
drwxr-xr-x  3 mirage mirage   4096 Sep  7 14:22  Linux_rookie
drwxr-xr-x  5 mirage mirage   4096 Sep  6 21:40  Json_Parser
drwxr-xr-x 18 mirage mirage   4096 Sep  5 11:22  json-tutorial
drwxr-xr-x  3 mirage mirage   4096 Sep  4 15:22  Json_Parser_Cpp
-rw-r--r--  1 mirage mirage 135210 Aug 30 11:06  hit-oslab-linux-20110823.tar.gz
-rw-r--r--  1 mirage mirage 130030 Aug 30 11:05  gcc-3.4-ubuntu.tar.gz
drwxr-xr-x 11 mirage mirage   4096 Aug  2 00:00  CS_Self_Study
drwxr-xr-x  4 mirage mirage   4096 Aug  1 21:21  project_2
drwxr-xr-x  4 mirage mirage   4096 Aug  1 20:10  projects
```
我们会发现第五列文件大小显示不够直观，那么我们还可以结合 **ls** 中 **h**进行调用显示 ```ls -lt -lh```(前后顺序无所谓)：
```
total 296K
drwxr-xr-x  3 mirage mirage 4.0K Sep  7 21:22  test
drwxr-xr-x  3 mirage mirage 4.0K Sep  7 14:22  Linux_rookie
drwxr-xr-x  5 mirage mirage 4.0K Sep  6 21:40  Json_Parser
drwxr-xr-x 18 mirage mirage 4.0K Sep  5 11:22  json-tutorial
drwxr-xr-x  3 mirage mirage 4.0K Sep  4 15:22  Json_Parser_Cpp
-rw-r--r--  1 mirage mirage 133K Aug 30 11:06  hit-oslab-linux-20110823.tar.gz
-rw-r--r--  1 mirage mirage 127K Aug 30 11:05  gcc-3.4-ubuntu.tar.gz
drwxr-xr-x 11 mirage mirage 4.0K Aug  2 00:00  CS_Self_Study
drwxr-xr-x  4 mirage mirage 4.0K Aug  1 21:21  project_2
drwxr-xr-x  4 mirage mirage 4.0K Aug  1 20:10  projects
```

next
