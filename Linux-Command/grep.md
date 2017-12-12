# Linux grep命令

Linux grep命令用于查找文件里符合条件的字符串。
若不指定任何文件名称，或是所给予的文件名为“-”，则grep指令会从标准输入设备读取数据。

## 语法

`grep [-abcEFGhHilLnqrsvVwxy][-A<显示列数>][-B<显示列数>][-C<显示列数>][-d<进行动作>][-e<范本样式>][-f<范本文件>][--help][范本样式][文件或目录...]`

**参数**

* -a或--text 不要忽略二进制的数据。
* -A<显示列数>或--after-context=<显示列数> 除了显示符合范本样式的那一列之外，并显示该列之后的内容。
* -b或--byte-offset 在显示符合范本样式的那一列之前，标示出该列第一个字符的位编号。
* -B<显示列数>或--before-context=<显示列数> 除了显示符合范本样式的那一列之外，并显示该列之前的内容。
* -c或--count 计算符合范本样式的列数。
* -C<显示列数>或--context=<显示列数>或-<显示列数> 除了显示符合范本样式的那一列之外，并显示该列之前后的内容。
* -d<进行动作>或--directories=<进行动作> 当指定要查找的是目录而非文件时，必须使用这项参数，否则grep指令将回报信息并停止动作。
* -e<范本样式>或--regexp=<范本样式> 指定字符串做为查找文件内容的范本样式。
* -E或--extended-regexp 将范本样式为延伸的普通表示法来使用。
* -f<范本文件>或--file=<范本文件> 指定范本文件，其内容含有一个或多个范本样式，让grep查找符合范本条件的文件内容，格式为每列一个范本样式。
* -F或--fixed-regexp 将范本样式视为固定字符串的列表。
* -G或--basic-regexp 将范本样式视为普通的表示法来使用。
* -h或--no-filename 在显示符合范本样式的那一列之前，不标示该列所属的文件名称。
* -H或--with-filename 在显示符合范本样式的那一列之前，表示该列所属的文件名称。
* **-i或--ignore-case 忽略字符大小写的差别**。
* -l或--file-with-matches 列出文件内容符合指定的范本样式的文件名称。
* -L或--files-without-match 列出文件内容不符合指定的范本样式的文件名称。
* -n或--line-number 在显示符合范本样式的那一列之前，标示出该列的列数编号。
* -q或--quiet或--silent 不显示任何信息。
* **-r或--recursive 此参数的效果和指定"-d recurse"参数相同**。
* -s或--no-messages 不显示错误信息。
* **-v或--revert-match 反转查找**。
* -V或--version 显示版本信息。
* -w或--word-regexp 只显示全字符合的列。
* -x或--line-regexp 只显示全列符合的列。
* -y 此参数的效果和指定"-i"参数相同。
* --help 在线帮助。

## 实例

```
$ grep test test* #查找后缀有“test”的文件包含“test”字符串的文件  

testfile1:This a Linux testfile! #列出testfile1 文件中包含test字符的行  
testfile_2:This is a linux testfile! #列出testfile_2 文件中包含test字符的行  
testfile_2:Linux test #列出testfile_2 文件中包含test字符的行 
```
```
$ grep -r update /etc/acpi #以递归的方式查找“etc/acpi”下包含“update”的文件
  
/etc/acpi/ac.d/85-anacron.sh:# (Things like the slocate updatedb cause a lot of IO.)  
Rather than  
/etc/acpi/resume.d/85-anacron.sh:# (Things like the slocate updatedb cause a lot of  
IO.) Rather than  
/etc/acpi/events/thinkpad-cmos:action=/usr/sbin/thinkpad-keys--update 
```
```
$ grep -v test *test* #查找文件名中包含test 的文件中不包含test的行

testfile1:helLinux!  
testfile1:Linis a free Unix-type operating system.  
testfile1:Lin  
testfile_1:HELLO LINUX!  
testfile_1:LINUX IS A FREE UNIX-TYPE OPTERATING SYSTEM.  
testfile_1:THIS IS A LINUX TESTFILE!  
testfile_2:HELLO LINUX!  
testfile_2:Linux is a free unix-type opterating system.
```

