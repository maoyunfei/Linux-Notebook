# Linux dig 命令

dig是域信息检索器的简称(Domain Information Groper)，可以执行查询域名相关的任务。

## 语法
```dig [选项参数] {domian}```

> 示例一：

> dig www.baidu.com

<img src="https://github.com/maoyunfei/Linux-Notebook/blob/master/Linux-Command/images/pic1.png?raw=true" width = "350" height = "350" align=center />

> 示例二：+short 输出精简答复

> dig www.baidu.com +short

<img src="https://github.com/maoyunfei/Linux-Notebook/blob/master/Linux-Command/images/pic2.png?raw=true" width = "350" height = "70" align=center />

> 示例三：+trace 追踪DNS解析过程

> dig www.baidu.com +trace

<img src="https://github.com/maoyunfei/Linux-Notebook/blob/master/Linux-Command/images/pic3.png?raw=true" width = "350" height = "500" align=center />
