#### 0724

##### 脚本需求

###写一个脚本，遍历/data目录下所有的txt文件

###将这些txt文件都做一个备份，备份的文件后面都增加一个年月日的后缀，如abc.txt 备份为 abc.txt_20231001

##### 脚本代码

```bash
#!/bin/bash
#author= zwj
#version=1.0
#date=2025-0724

##定义后缀变量，注意反引号的含义
suffix=`date +%Y%m%d`
echo "${suffix}"

##找到/data下所有的txt文件
for f in `find /data -type f -name "*.txt"`
do
	echo "backupfile:${f}...."
    cp ${f} ${f}_${suffix}
done

```

##### 执行结果

![](https://raw.githubusercontent.com/Romantic-1/ImgBed/main/20250724170745436.png)

##### 总结关键：

###### 1.定义变量

shell支持三种定义变量的方式

```bash
var=var
var='var'
var="var"
```

如果变量值不包含任何空白符（空格，tab，缩进等），那么可以不用引号

注意赋值的等号周围是不能有空格的

shell变量命名规范：

​	变量名由数字、字母、下划线组成

​	必须由字母或者下划线开头

​	不能使用shell里面的关键字，如help，ll等等

###### 2.使用变量

使用定义过的变量，只需要在变量名前面加美元符合即可，如：

```bash
a="hello"
echo $a
echo ${a}
```

变量名外面的花括号`{ }`是可选的，加不加都行，加花括号是为了帮助解释器识别变量的边界

推荐给所有变量加上花括号`{ }`，这是个良好的编程习惯。

###### 3.修改变量的值

已定义的变量，可以被重新赋值，如：

```bash
a="hello"
echo ${a}
a="bi"
echo ${a}
```

第二次对变量赋值时不能在变量名前加`$`，只有在使用变量时才能加`$`。

###### 4.单引号和双引号的区别

示例：

```bash
#!/bin/bash
a="hello"
b1='print:$a'
b2="print:$a"
echo $b1
echo $b2

运行结果
print:$a
print:hello
```

以单引号`' '`包围变量的值时，单引号里面是什么就输出什么，即使内容中有变量和命令（命令需要反引起来）也会把它们原样输出。

以双引号`" "`包围变量的值时，输出时会先解析里面的变量和命令，而不是把双引号中的变量名和命令原样输出。

###### 5.反引号的含义

反引号用于[命令替换](https://zhida.zhihu.com/search?content_id=125063556&content_type=Article&match_order=1&q=命令替换&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3NTM1MjQzNTMsInEiOiLlkb3ku6Tmm7_mjaIiLCJ6aGlkYV9zb3VyY2UiOiJlbnRpdHkiLCJjb250ZW50X2lkIjoxMjUwNjM1NTYsImNvbnRlbnRfdHlwZSI6IkFydGljbGUiLCJtYXRjaF9vcmRlciI6MSwiemRfdG9rZW4iOm51bGx9.ut3kxFlMlmJPUOR9_lqE0sh792goEpcIhs8oqP2gb84&zhida_source=entity)，即先执行反引号中的语句，再把结果加入到原命令中。

反引号的用法示例如下，先执行date命令，再将结果与字符串"date: "连起来，最后再echo出来。

```bash
echo "date:`date`"
```

![](https://raw.githubusercontent.com/Romantic-1/ImgBed/main/20250724180842057.png)

###### 6.for循环

for循环知识点较多，后续补充

###### 7.find命令的参数



```bash
-name   filename                #查找名为filename的文件
-type   b/d/c/p/l/f             #查是块设备、目录、字符设备、管道、符号链接、普通文件
-size   n[c]                    #查长度为n块[或n字节]的文件
-follow                         #如果遇到符号链接文件，就跟踪链接所指的文件

少用：
-perm                              #按执行权限来查找
-user     username                 #按文件属主来查找
-group    groupname                #按组来查找
-mtime    -n +n                    #按文件更改时间来查找文件，-n指n天以内，+n指n天以前
-atime    -n +n                    #按文件访问时间来查找文件，-n指n天以内，+n指n天以前
-ctime    -n +n                    #按文件创建时间来查找文件，-n指n天以内，+n指n天以前
```

参考：[Linux下find命令详解_linux find命令详解-CSDN博客](https://blog.csdn.net/l_liangkk/article/details/81294260)





