# Linux ps命令

Linux ps命令用于显示当前进程(process)的状态

## 语法

`ps [options] [--help]`

**参数**

ps 的参数非常多, 在此仅列出几个常用的参数并大略介绍含义

* -A 列出所有的行程
* -u 显示指定用户的进程
* -e 等于“-A”
* -f 以格式化显示
* a 显示所有涉及终端的进程信息
* u 显示面向用户的输出
* x 显示没有终端的进程

> au(x) 输出格式 :

> USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND


## 实例

**显示进程信息**

```
# ps -A 显示进程信息

PID TTY     TIME CMD
  1 ?    00:00:02 init
  2 ?    00:00:00 kthreadd
  3 ?    00:00:00 migration/0
  4 ?    00:00:00 ksoftirqd/0
  5 ?    00:00:00 watchdog/0
……省略部分结果
31160 ?    00:00:00 dhclient
31211 ?    00:00:00 aptd
31302 ?    00:00:00 sshd
31374 pts/2  00:00:00 bash
31396 pts/2  00:00:00 ps
```
**显示指定用户信息**

```
# ps -u root 显示root进程用户信息

 PID TTY     TIME CMD
  1 ?    00:00:02 init
  2 ?    00:00:00 kthreadd
  3 ?    00:00:00 migration/0
  4 ?    00:00:00 ksoftirqd/0
  5 ?    00:00:00 watchdog/0
……省略部分结果 
31160 ?    00:00:00 dhclient
31211 ?    00:00:00 aptd
31302 ?    00:00:00 sshd
31374 pts/2  00:00:00 bash
31397 pts/2  00:00:00 ps
```
**显示所有进程信息，连同命令行**

```
# ps -ef 显示所有命令，连带命令行

UID    PID PPID C STIME TTY     TIME CMD
root     1   0 0 10:22 ?    00:00:02 /sbin/init
root     2   0 0 10:22 ?    00:00:00 [kthreadd]
root     3   2 0 10:22 ?    00:00:00 [migration/0]
root     4   2 0 10:22 ?    00:00:00 [ksoftirqd/0]
root     5   2 0 10:22 ?    00:00:00 [watchdog/0]
……省略部分结果
root   31302 2095 0 17:42 ?    00:00:00 sshd: root@pts/2 
root   31374 31302 0 17:42 pts/2  00:00:00 -bash
root   31400   1 0 17:46 ?    00:00:00 /usr/bin/python /usr/sbin/aptd
root   31407 31374 0 17:48 pts/2  00:00:00 ps -ef
```

**ps与grep常用组合用法，查找特定进程**

```
# ps -ef | grep ssh

UID    PID PPID C STIME TTY     TIME CMD
root  2720   1  0 Nov02 ?        00:00:00 /usr/sbin/sshd
root 17394 2720  0 14:58 ?        00:00:00 sshd: root@pts/0 
root 17465 17398  0 15:57 pts/0    00:00:00 grep ssh
```
**列出目前所有的正在内存当中的程序**

```
# ps aux

USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.0  10368   676 ?        Ss   Nov02   0:00 init [3]                  
root         2  0.0  0.0      0     0 ?        S<   Nov02   0:01 [migration/0]
root         3  0.0  0.0      0     0 ?        SN   Nov02   0:00 [ksoftirqd/0]
root         4  0.0  0.0      0     0 ?        S<   Nov02   0:01 [migration/1]
root         5  0.0  0.0      0     0 ?        SN   Nov02   0:00 [ksoftirqd/1]
root         6  0.0  0.0      0     0 ?        S<   Nov02  29:57 [events/0]
root         7  0.0  0.0      0     0 ?        S<   Nov02   0:00 [events/1]
root         8  0.0  0.0      0     0 ?        S<   Nov02   0:00 
……省略部分结果
```

ps aux可以显示进程占用CPU和内存情况。