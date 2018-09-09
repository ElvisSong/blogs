+++

title = "进程管理"
date = 2017-08-21T00:00:00+08:00
categories = ["读书笔记"]
toc = true
author = "ElvisSong"
author_homepage =  "https://elvissong.github.io/post/"
+++

## 进程管理

### 进程管理的作用
1. 判断服务器健康状态
	. 查看系统中	所有进程
3. 杀死进程

### 查看所有进程
* ps aux (BSD 操作系统格式)
* ps -le  (Linux 标准命令格式 )

```
-a  显示一个终端的所有进程，除了会话引线
-u  显示一个进程的归属用户和内存使用情况
-x  显示没有控制终端的进程
-l  长格式显示，显示更加详细的信息
-e  显示所有进程，和-A作用一致
```

### 查看进程数
* pstree
```
-p  显示进程的PID 
-u  显示进程所属用户
```

### 查看系统健康状态

* top 命令选项
```
-d  指定 top 命令刷新频率，默认 3s
-b  使用批处理模式输出
-n  指定 top 命令执行次数，和-b共用  
```
e.g. 执行两次并输出到 top.log文件
> top -b -n 2 > top.log

在 top 交互模式下可执行命令

* ? 或 h： 显示帮助信息
* P ：以 CPU 占用率排序（默认）
* M ：以 内存使用率牌序
* N ：以 PID 进行排序
* q : 退出 top

### 杀死进程

#### 使用 kill 命令

> kill -[信号] 进程号

Linux中的重要信号

信号代号 | 信号名称 | 说明 
---|---|---
1 | SIGHUP | 让进程立即关闭，重新读取配置文件后重启
2 | SIGINT | 程序终止信号，用于终止让前台程序，相当于ctrl+c
8 | SIGFPE | 在发生致命的算术错误时发出，不仅包括浮点运算错误，还包括溢出及除数为0等其他所有的算术错误
9 | SIGKILL| 用来立即结束程序的运行，本信号不能被阻塞，处理和忽略，常用于强制终止进程
14 | SIGALRM | 时钟定时信号，计算的是实际的时间或时钟时间，alarm 函数使用该符号
15 | SIGTERM | 正常结束进程的信号，kill 命令默认的信号，若进程产生问题，无法正常终止，则会使用信号9
18 | SIGCONT | 让暂停的进程恢复执行，不能被阻断
19 | SIGSTOP | 暂停前台进程，相当于 ctrl+z 快捷键，不能被阻断

重启进程
> kill -1 2345

强制杀死进程
> kill -9 2345

#### 使用 killall 命令

killall 按照进程名来杀死进程

> killall [选项][信号] 进程名
```
-i :交互式, 询问是否要杀死某个进程
-I :忽略进程名大小写
```

#### 使用 pkill 命令

pkill 按照进程名来终止进程

> pkill [选项][信号] 进程名
```
-t 终端号: 按照终端号踢出用户
```

补充： w -查询本机已经登录的用户

强制杀死从 pts/1 虚拟终端登陆的进程
> pkill -t -9 pts/1

## 工作管理

### 把进程放入后台

使用 ‘&’ 把命令放入后台，并在后台执行
> tar -zxvf test.tar.gz /home/test &

使用 CTRL + z ,把命令放在后台并暂停

### 查看后台的工作

显示后台工作的 PID
> jobs -l 

### 将后台工作恢复到前台

> fg %[工作号]

### 把后台暂停的工作恢复到前台

> bg %[工作号]

### 后台命令脱离终端后仍能够执行方法

* 把需要执行的命令加入 /etc/rc.local 文件
* 使用系统定时任务, 让系统在指定的时间执行某个后台命令
* 使用 nohup 命令

> nohup [命令] &

## 系统资源查看

### vmstat 监控系统资源

> vmstat [刷新延时 刷新次数]

### dmesg 检测内核信息
> dmesg
> dmesg |grep CPU 

### free 查看内存使用
> free [-b|-k|-m-g] 以 byte,KB,MB,GB 为单位显示

### 查看 CPU 信息
> cat /proc/cpuinfo

### uptime
显示系统的启动时间和平均负载，也就是 top 命令的第一行信息，用 w 命令也可以查看

### 查看系统内核相关信息
> uname [选项]
```
-a : 查看系统所有相关信息 
-r : 查看内核版本
-s : 查看内核名称
```

### 判断操作系统位数
执行一个本地命令即可查看到
> file /bin/ls

### 查询当前 Linux 系统版本
> lsb_release -a (centos 7 没有)

### 列出进程打开或使用的文件信息
> lsof [选项]
```
-c 字符串: 只列出以字符串开头的进程打开的文件
-u 用户名: 只列出某个用户打开的文件
-p pid: 只列出某个进程打开的文件
```

查询某个文件被哪个进程调用
> lsof /sbin/init

查询 httpd 进程调用哪些文件
> lsof -c httpd 

## 系统定时任务

### at 一次性定时任务
确定 at 服务已安装
> chkconfig --list | grep atd (centos 6.x 及之前)

> systemctl list-unit-files | grep atd (centos 7)

重启 at 服务
> service atd restart

### 了解 at 的访问控制
* 如果 /etc/at.allow 文件存在，那么只有写入 at.allow 文件（白名单）中的用户可以使用 at 命令 
* 如果 /etc/at.deny 文件存在，则写入 at.deny 文件（黑名单）中的用户不能使用 at 命令，对root 用户无效
* 如果两个文件都不存在，则只有 root 用户能够执行 at 命令
* 白名单的权限高于黑名单

### at 命令
at [选项] 时间
```
选项

-m : 当 at 工作完成后，无论是否有命令输出，都通过 Email 通知执行该 at 命令的用户
-c 工作号 ：显示该 at 的实际工作内容

时间

- HH:MM 
- HH:MM YYYY-MM-DD
- HH:MM [am][pm] [month][date]
- HH:MM [am][pm] + [minutes|hours|days|weeks] 
```

## crond 服务管理
### crond 访问控制

与 at 服务类似
* 系统中存在 /etc/cron.allow 文件时，只有写入该文件中的用户可以使用 crond 命令
* 系统中只有 /etc/cron.deny 文件时，只有写入该文件中的用户不能够使用 crond 命令

### crond 服务
重启 crond 服务
> service crond restart

或者
> chkconfig crond on 

ps : centos7 会将其转为 systemctl enable crond.service 来执行

### 用户的 crontab 设置
crond [选项]
```
-e : 编辑 crontab 定时任务 
-l : 查询 crontab 任务
-r : 删除当前用户的所有 crontab 任务
```

crontab -e 进入编辑定时任务界面，会打开 vim 编辑工作

格式如下：
\* * * * * 你要执行的任务

 项目 | 含义 | 范围 
 ---|---|---
 第一个‘*’| 一小时当中的第几分钟 | 0-59 
 第二个‘*’| 一天当中的第几小时 | 0-23 
 第三个‘*’| 一个月当中的第几天 | 0-31 
 第四个‘*’| 一年当中的第几个月 | 1-12 
 第五个‘*’| 一周当中的星期几 | 0-7 

 特殊符号 | 含义
 ---|---
 \* | 代表任何时间，比如第一个‘*’表示一个小时中每分钟都执行一次
 , | 代表不连续的时间，比如‘0 8,16 * * *’命令表示在每天的8点0分，16点0分都执行一次的意思
 \- | 代表连续的时间，比如‘0 5 * * 1-5’命令表示每周一到周五的5点0分执行一次任务
 \*/n | 代表每隔多久执行一次，比如‘*/10 * * * *’表示每隔10 分钟执行一次任务

 ### crond 注意事项
 * 六个选项都不能为空，必须填写，如果不确定使用‘*’代替任意时间
 * crontab 最小有效时间是分钟，最大有效时间是月
 * 在定义时间时，日期和星期最好不要在同一条命令中出现，容易让管理员混乱
 * 在定时任务中，不管是直接写命令还是在脚本写命令，都必须使用绝对路径

## 系统的定时任务
上一小节讲的是用户的定时任务，这一节来讲一下系统的定时任务，也就是要编辑 /etc/crontab 这个配置文件

### 执行系统定时任务方法
* 手工执行定时任务
* 系统定时任务

1. 把需要定时执行的脚本复制到 /etc/cron.{daily,weekly,monthly} 目录中的任意一个
1. 修改 /etc/crontab 配置文件

## anacron 
anacron 服务是用来保证在系统关机的时候错过的定时任务，可以在系统开机之后再执行

### anacron 检测周期
* anacron 会使用一天，一星期，一个月作为检测周期
* 在系统的 /var/spool/anacron/ 目录中存在 cron.{daily,weekly,monthly}文件，用于记录上次执行 cron 的时间
* 和当前时间做比较，如果两个时间的差值超过了 anacron 的指定时间差值，证明有 cron 任务被执行

### anacron 配置文件
```
vi /etc/anacrontab
- RANDOM_DELAY=45 #最大随机延迟
- START_HOURS_RANGE=3-22 #anacron的执行时间范围是3：00-22：00
- 1     5    cron.daily   nice run-parts /etc/cron.daily
- 7     25   cron.weekly   nice run-parts /etc/cron.weekly
- @montyly    45   cron.monthly    nice  run-parts  /etc/cron.monthly
  # 天数      强制延迟（分）      工作名称       实际执行的命令
```
### cron.daily 工作过程，其他类似
* 首先读取 /var/spool/anacron/cron.daily 中的上一次 anacron 执行的时间
* 和当前时间比较，如果两个时间的差值超过 1 天，就执行 cron.daily 工作
* 执行这个工作只能在 03：00 -22：00 之间
* 执行工作时强制延迟时间为 5 分钟，再随机延迟 0-45 分钟时间
* 使用 nice 命令指定默认优先级，使用 run-parts 脚本执行 /etc/cron.daily 目录中的所有可执行文件
