# Linux awk 命令
[原文链接](http://www.runoob.com/linux/linux-comm-awk.html)

AWK是一种处理文本文件的语言，是一个强大的文本分析工具。

之所以叫AWK是因为其取了三位创始人Alfred Aho，Peter Weinberger, 和 Brian Kernighan 的Family Name的首字符。

## 语法
```
awk [选项参数] 'script' var=value file(s)
或
awk [选项参数] -f scriptfile var=value file(s)
```
### 常用选项参数说明
* -F fs </br>指定输入文件的分隔符，fs是一个字符串或者是一个正则表达式，如-F:。
* -V var=value </br>赋值一个用户定义变量
* -f scripfile </br>从脚本文件中读取awk命令。

### 基本用法
log.txt文本内容如下：

```
2 this is a test
3 Are you like awk
This's a test
10 There are orange,apple,mongo
```
#### 用法一
> awk '{[pattern] action}' {filenames}   # 行匹配语句 awk '' 只能用单引号

实例：

```
# 每行按空格或TAB分割，输出文本中的1、4项
 $ awk '{print $1,$4}' log.txt
 ---------------------------------------------
 2 a
 3 like
 This's
 10 orange,apple,mongo
 
 # 格式化输出
 $ awk '{printf "%-8s %-10s\n",$1,$4}' log.txt
 ---------------------------------------------
 2        a
 3        like
 This's
 10       orange,apple,mongo
```
#### 用法二
> awk -F  #-F相当于内置变量FS, 指定分割字符

实例：

```
# 使用","分割
 $  awk -F, '{print $1,$2}' log.txt
 ---------------------------------------------
 2 this is a test
 3 Are you like awk
 This's a test
 10 There are orange apple
 
 # 或者使用内建变量
 $ awk 'BEGIN{FS=","} {print $1,$2}' log.txt
 ---------------------------------------------
 2 this is a test
 3 Are you like awk
 This's a test
 10 There are orange apple
 
 # 使用多个分隔符.先使用空格分割，然后对分割结果再使用","分割
 $ awk -F '[ ,]'  '{print $1,$2,$5}' log.txt
 ---------------------------------------------
 2 this test
 3 Are awk
 This's a
 10 There apple
```
#### 用法三
> awk -v  # 设置变量

实例：

```
$ awk -va=1 '{print $1,$1+a}' log.txt
 ---------------------------------------------
 2 3
 3 4
 This's 1
 10 11
 
 $ awk -va=1 -vb=s '{print $1,$1+a,$1b}' log.txt
 ---------------------------------------------
 2 3 2s
 3 4 3s
 This's 1 This'ss
 10 11 10s
```
#### 用法四
> awk -f {awk脚本} {文件名}

实例：

` $ awk -f cal.awk log.txt `
### 运算符
<table class="reference">
<thead>
<tr>
<th>运算符</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td>= += -= *= /= %= ^= **=</td>
<td>赋值</td>
</tr>
<tr>
<td>?:</td>
<td>C条件表达式</td>
</tr>
<tr>
<td>||</td>
<td>逻辑或</td>
</tr>
<tr>
<td>&amp;&amp;</td>
<td>逻辑与</td>
</tr>
<tr>
<td>~ ~!</td>
<td>匹配正则表达式和不匹配正则表达式</td>
</tr>
<tr>
<td>&lt; &lt;= &gt; &gt;= != ==</td>
<td>关系运算符</td>
</tr>
<tr>
<td>空格</td>
<td>连接</td>
</tr>
<tr>
<td>+ -</td>
<td>加，减</td>
</tr>
<tr>
<td>* / %</td>
<td>乘，除与求余</td>
</tr>
<tr>
<td>+ - !</td>
<td>一元加，减和逻辑非</td>
</tr>
<tr>
<td>^ ***</td>
<td>求幂</td>
</tr>
<tr>
<td>++ --</td>
<td>增加或减少，作为前缀或后缀</td>
</tr>
<tr>
<td>$</td>
<td>字段引用</td>
</tr>
<tr>
<td>in</td>
<td>数组成员</td>
</tr>
</tbody>
</table>
* 过滤第一列大于2的行

```
$ awk '$1>2' log.txt    #命令
#输出
3 Are you like awk
This's a test
10 There are orange,apple,mongo
```
* 过滤第一列等于2的行

```
$ awk '$1==2 {print $1,$3}' log.txt    #命令
#输出
2 is
```

* 过滤第一列大于2并且第二列等于'Are'的行

```
$ awk '$1>2 && $2=="Are" {print $1,$2,$3}' log.txt    #命令
#输出
3 Are you
```
### 内置变量
<table class="reference">
<thead>
<tr>
<th>变量</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td>\$n</td>
<td>当前记录的第n个字段，字段间由FS分隔</td>
</tr>
<tr>
<td>\$0</td>
<td>完整的输入记录</td>
</tr>
<tr>
<td>ARGC</td>
<td>命令行参数的数目</td>
</tr>
<tr>
<td>ARGIND</td>
<td>命令行中当前文件的位置(从0开始算)</td>
</tr>
<tr>
<td>ARGV</td>
<td>包含命令行参数的数组</td>
</tr>
<tr>
<td>CONVFMT</td>
<td>数字转换格式(默认值为%.6g)ENVIRON环境变量关联数组</td>
</tr>
<tr>
<td>ERRNO</td>
<td>最后一个系统错误的描述</td>
</tr>
<tr>
<td>FIELDWIDTHS</td>
<td>字段宽度列表(用空格键分隔)</td>
</tr>
<tr>
<td>FILENAME</td>
<td>当前文件名</td>
</tr>
<tr>
<td>FNR</td>
<td>各文件分别计数的行号</td>
</tr>
<tr>
<td>FS</td>
<td>字段分隔符(默认是任何空格)</td>
</tr>
<tr>
<td>IGNORECASE</td>
<td>如果为真，则进行忽略大小写的匹配</td>
</tr>
<tr>
<td>NF</td>
<td>输入字段分割符</td>
</tr>
<tr>
<td>NR</td>
<td>已经读出的记录数，就是行号，从1开始</td>
</tr>
<tr>
<td>OFMT</td>
<td>数字的输出格式(默认值是%.6g)</td>
</tr>
<tr>
<td>OFS</td>
<td>输出记录分隔符（输出换行符），输出时用指定的符号代替换行符</td>
</tr>
<tr>
<td>ORS</td>
<td>输出记录分隔符(默认值是一个换行符)</td>
</tr>
<tr>
<td>RLENGTH</td>
<td>由match函数所匹配的字符串的长度</td>
</tr>
<tr>
<td>RS</td>
<td>记录分隔符(默认是一个换行符)</td>
</tr>
<tr>
<td>RSTART</td>
<td>由match函数所匹配的字符串的第一个位置</td>
</tr>
<tr>
<td>SUBSEP</td>
<td>数组下标分隔符(默认值是/034)</td>
</tr>
</tbody>
</table>
### 使用正则，字符串匹配

```
# 输出第二列包含 "th"，并打印第二列与第四列
$ awk '$2 ~ /th/ {print $2,$4}' log.txt
---------------------------------------------
this a
```
**~ 表示模式开始。//中是模式**

```
# 输出包含"re" 的行
$ awk '/re/ ' log.txt
---------------------------------------------
3 Are you like awk
10 There are orange,apple,mongo
```
### 忽略大小写

```
$ awk 'BEGIN{IGNORECASE=1} /this/' log.txt
---------------------------------------------
2 this is a test
This's a test
```
### 模式取反

```
$ awk '$2 !~ /th/ {print $2,$4}' log.txt
---------------------------------------------
Are like
a
There orange,apple,mongo

$ awk '!/th/ {print $2,$4}' log.txt
---------------------------------------------
Are like
a
There orange,apple,mongo
```
### awk脚本
关于awk脚本，我们需要注意两个关键词BEGIN和END。

* BEGIN{ 这里面放的是执行前的语句 }
* END {这里面放的是处理完所有的行后要执行的语句 }
* {这里面放的是处理每一行时要执行的语句}

假设有这么一个文件（学生成绩表）：

```
$ cat score.txt
Marry   2143 78 84 77
Jack    2321 66 78 45
Tom     2122 48 77 71
Mike    2537 87 97 95
Bob     2415 40 57 62
```
我们的awk脚本如下：

```
$ cat cal.awk
#!/bin/awk -f
#运行前
BEGIN {
    math = 0
    english = 0
    computer = 0
 
    printf "NAME    NO.   MATH  ENGLISH  COMPUTER   TOTAL\n"
    printf "---------------------------------------------\n"
}
#运行中
{
    math+=$3
    english+=$4
    computer+=$5
    printf "%-6s %-6s %4d %8d %8d %8d\n", $1, $2, $3,$4,$5, $3+$4+$5
}
#运行后
END {
    printf "---------------------------------------------\n"
    printf "  TOTAL:%10d %8d %8d \n", math, english, computer
    printf "AVERAGE:%10.2f %8.2f %8.2f\n", math/NR, english/NR, computer/NR
}
```
我们来看一下执行结果：

```
$ awk -f cal.awk score.txt
NAME    NO.   MATH  ENGLISH  COMPUTER   TOTAL
---------------------------------------------
Marry  2143     78       84       77      239
Jack   2321     66       78       45      189
Tom    2122     48       77       71      196
Mike   2537     87       97       95      279
Bob    2415     40       57       62      159
---------------------------------------------
  TOTAL:       319      393      350
AVERAGE:     63.80    78.60    70.00
```