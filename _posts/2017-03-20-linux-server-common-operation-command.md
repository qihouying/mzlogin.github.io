---
layout: post
titile: Linux服务器常用操作和命令
category: Linux
descroption: Linux常用命令
keywords: keyword1, keyword2
---
### 目录
* [1. 什么是linux服务器load average](#1)
* [2. 如何查看linux服务器负载](#2)
* [3. 服务器负载高怎么办？](#3)
* [4. 如何查看服务器内存使用率？](#4)
* [5. 如何查看单个进程占用的内存大小](#5)
* [6. 无法从linux服务器A登录到服务器B怎么办](#6)
* [7. 如何查看正在使用的服务和端口](#7)
* [8. 如何查看服务器进程信息？](#8)
* [9. 如何杀死进程](#9)
* [10. 如何查找僵尸进程？](#10)
* [11. 如何在内网服务器间传输数据](#11)
* [12. 为什么启动不了服务器端口？](#12)
* [13. 常用的linux服务器性能查看命令有哪些？](#13)
* [14. Cron不生效怎么办？](#14)
* [15. 如何设置opensuse服务器开机任务？](#15)
* [16. 为什么服务器硬盘只读？](#16)
* [17. 如何查看linux系统日志？](#17)
* [18. 如何查找文件系统大文件？](#18)
* [19. 如何查看服务器操作系统版本？](#19)
* [20. 如何重启服务器？](#20)
* [21. 为什么linux终端显示中文会出现乱码](#21)
* [22. 如何设置通过SecureCRT连接CVM服务器的超时时间？](#22)
* [23. 如何获得CVM的root权限？](#23())
* [24. 为什么删除linux服务器上的文件，硬盘空间不释放？](#24)
<h2 id="1"> 1. 什么是linux服务器load average？</h2>

Load是用来度量服务器工作量的大小，即计算机cpu任务执行队列的长度，值越大，表明包括正在运行和待运行的进程数越多。

参考资料：[http://en.wikipedia.org/wiki/Load_average](http://en.wikipedia.org/wiki/Load_average) 

<h2 id="2"> 2. 如何查看linux服务器负载 </h2>

可以通过w，top，uptime，procinfo命令，也可以通过/proc/loadavg文件查看。 

<h2 id="3"> 3. 服务器负载高怎么办？</h2>

服务器负载（load/load average）是根据进程队列的长度来显示的。
当服务器出现负载高的现象时（建议以15分钟平均值为参考），可能是由于CPU资源不足，I/O读写瓶颈，内存资源不足等原因造成，也可能是由于CPU正在进行密集型计算。

建议使用vmstat -x，iostat，top命令判断负载过高的原因，然后找到具体占用大量资源的进程进行优化处理。 

<h2 id="4"> 4. 如何查看服务器内存使用率？</h2>

可以通过free，top（执行后可通过shitf+m对内存排序），vmstat，procinfo命令，也可以通过/proc/meminfo文件查看。 

<h2 id="5"> 5. 如何查看单个进程占用的内存大小？</h2>

可以使用top -p PID，pmap -x PID，ps aux\|grep PID命令，也可以通过/proc/$process_id（进程的PID）/status文件查看，例如/proc/7159/status文件。 

<h2 id="6"> 6. 无法从linux服务器A登录到服务器B怎么办？</h2>

请开发者首先确认服务器A和B是属于同一个应用，不同应用无法交叉登录。

    * 当服务器A无法登录服务器B时，可以使用ping IP和telnet IP 36000命令确认服务器B是否死机，ssh服务是否正常。
如果有异常，登录open.qq.com管理中心重启服务器（详细操作说明见：[CVM_V2申请和管理#3.2 服务器重启](http://wiki.open.qq.com/wiki/CVM_V2%E7%94%B3%E8%AF%B7%E5%92%8C%E7%AE%A1%E7%90%86#3.2_.E6.9C.8D.E5.8A.A1.E5.99.A8.E9.87.8D.E5.90.AF)

    * 如果可以通过客户端直接访问服务器B，但是不能从服务器A登录服务器B，请通过企业QQ联系运维支持协助定位。 

<h2 id="7"> 7. 如何查看正在使用的服务和端口？</h2>

可以使用netstat -tunlp，netstat -antup，lsof -i:PORT命令查看。 

<h2 id="8"> 8. 如何查看服务器进程信息？</h2>

可以使用ps auxww\|grep PID，ps -ef，lsof -p PID，top -p PID命令查看。 

<h2 id="9"> 9. 如何杀死进程？</h2>

可以使用kill -9 PID（进程号），killall 程序名（比如killall cron）来杀死进程。
如果要杀死的是僵尸进程，则需要杀掉进程的父进程才有效果，命令为： kill -9 ppid（ppid为父进程ID号，可以通过ps -o ppid PID查找，例如ps -o ppid 32535）。 

<h2 id="10"> 10. 如何查找僵尸进程？</h2>

可以使用top命令查看僵尸进程（zombie）的总数，使用ps -ef \| grep defunct \| grep -v grep查找具体僵尸进程的信息。 

<h2 id="11"> 11. 如何在内网服务器间传输数据？</h2>

同一应用下的不同机器，可以通过如下命令实现文件传输：
scp -P port（使用36000端口） /home/user/localfilename（本地文件路径） user（使用appid）@serverip:/home/user/removefilename（目标文件路径）
rsync -e 'ssh -p port（使用36000端口） -q' /home/user/localfilename （本地文件路径） user（使用appid）@serverip:/home/user/removefilename（目标文件路径） 

<h2 id="12"> 12. 为什么启动不了服务器端口？</h2>

服务器端口的启动监听，需要从操作系统本身以及应用程序查看。
linux操作系统1024以下的端口只能由root用户启动，即需要先运行sudo su –获取root权限后再启用服务端口。
应用程序问题，建议通过应用程序启动日志来排查失败原因，例如端口冲突（腾讯服务器系统使用端口不能占用，比如36000），配置问题等。 

<h2 id="13"> 13. 常用的linux服务器性能查看命令有哪些？</h2>
         命令名称                                                说明
           top       进程监控命令，用来监控系统的整体性能。可以显示系统负载，进程，cpu，内存，分页等信息，常用shift+m和shift+p来按memory和cpu使用对进程进行排序。      

          vmstat    系统监控命令，重点侧重于虚拟内存，也可以监控cpu，进程，内存分页以及IO的状态信息例如，vmstat 3 10，每隔3秒输出结果，执行10次。                    
           
           df        用来检查系统的磁盘空间占用状况。例如：df -m，以MB为单位展现磁盘使用状况。                                                                                                  

           ps        进程查看命令，可以用来显示进程的详细信息。常用命令参数组合为，ps -ef，ps aux，推荐使用ps -A -o来自定义输出字段。 例如：ps -A -o pid,stat,uname,%cpu,%mem,rss,args,lstart,etime\ | sort -k6,6 -rn，按所列字段输出并以第六个字段进行排序; ps -A -o comm \ | sort -k1 \ | uniq -c\ | sort -k1 -rn\ | head，列出运行实例最多的进程。

其他常用的命令和文件，free -m，du，uptime，w，/proc/stat，/proc/cpuinfo，/proc/meminfo。 

参考资料：[http://en.wikipedia.org/wiki/Template:Unix_commands，http://www.linuxmanpages.com/](http://en.wikipedia.org/wiki/Template:Unix_commands，http://www.linuxmanpages.com/)

<h2 id="14"> 14. Cron不生效怎么办？</h2>

排查步骤如下：
* 确认crontab是否正常运行。可以运行命令crontab -e添加如下测试条目*/1 * * * * /bin/date >> /tmp/crontest 2>&1 &，然后观察/tmp/crontest文件。如果有问题，建议使用ps aux\|grep cron查找cron的pid，kill -9 PID结束cron进程，然后通过/etc/init.d/cron start重新启动cron。 
* 确认cron条目中的脚本路径为绝对路径。
* 查看运行cron的用户帐号是否正确，同时查看/etc/cron.deny中是否包含此账户。
* 检查脚本的执行权限，脚本目录以及日志的文件权限。
* 建议通过后台方式运行脚本，在脚本条目后添加“&”，例如，*/1 * * * * /bin/date >> /tmp/crontest 2>&1 & 

<h2 id="15"> 15. 如何设置opensuse服务器开机任务？</h2>

Linux内核启动顺序为：
> /sbin/init进程启动，

> 然后依次执行init初始脚本，

> 运行级别脚本/etc/rc.d/rc*.d，*号值等于运行模式，可以在/etc/inittab中查看，

> 最后是/etc/rc.d/rc.local。

> 如果需要配置开机任务，可以在/etc/rc.d/rc*.d中的S**rclocal文件配置，也可以在/etc/rc.d/rc.local中配置。 

<h2 id="16"> 16. 为什么服务器硬盘只读？</h2>

硬盘只读的常见原因如下：
*  磁盘空间满

  可以通过df -m命令查看磁盘使用情况，然后删除多余的文件释放磁盘空间（非第三方文件不建议删除，如果需要请联系企业QQ确认）； 

* 磁盘inode资源占用完

  可以通过df -i命令查看，确认相关的进程； 
* 硬件故障。

如果hosting应用通过上述方式仍无法确认原因，请通过企业QQ联系运维支持协助定位。 

<h2 id="17"> 17. 如何查看linux系统日志？</h2>

系统级别的日志文件存放路径为/var/log。
常用的系统日志为/var/log/messages 。

<h2 id="18"> 18. 如何查找文件系统大文件？</h2>

可以首先通过df命令查看磁盘分区使用情况，比如df -m；
然后：

通过du命令查看具体文件夹的大小，比如du -sh ./*，du -h --max-depth=1\|head -10；

使用ls命令列出文件以及大小，比如ls -lSh；

另外，也可以通过find命令直接查看特定目录下的文件大小，比如find / -type f -size +10M -exec ls -lrt {} \; 

<h2 id="19"> 19. 如何查看服务器操作系统版本？</h2>

可以通过下列命令查看系统版本：

uname -a，cat /proc/version，cat /etc/issue 

<h2 id="20"> 20. 如何重启服务器？</h2>

方式1：
登录open.qq.com管理中心重启服务器（详细操作说明见：CVM_V2申请和管理#3.2 服务器重启）。 

方式2：如果方式1不生效，可以尝试在服务器上以root运行reboot命令进行重启。 

<h2 id="21"> 21. 为什么linux终端显示中文会出现乱码？</h2>

服务器本身没有对显示语言有限制，如果是终端软件的影响中文的显示

可以尝试调整 选项-会话选项-外观（secureCRT设置，其他版本软件请查找相关设置）；

如果是纯Linux shell出现乱码，请使用export命令查看用户环境变量，查看LANG，LC_CTYPE等环境变量设置。

<h2 id="22"> 22. 如何设置通过SecureCRT连接CVM服务器的超时时间？</h2>

可以通过如下设置，使SecureCRT连接CVM时，不断开连接：

打开secureCRT选项(Options)，选择会话选项（Session Opetions），点击终端（Terminal），在右侧反空闲（Anti-idle）的框中勾选发送协议NO-OP（Send protocol NO-OP），时间设置为每120秒(every 120 seconds)。 

<h2 id="23"> 23. 如何获得CVM的root权限？</h2>

详见：root权限说明。 

<h2 id="24"> 24. 为什么删除linux服务器上的文件，硬盘空间不释放？</h2>

现象：

登录linux服务器，执行 rm 命令删除文件，用 df 命令查看硬盘空间，发现删除文件后，可用的硬盘空间没有增加。

原因：

通过 rm 命令删除文件的时候，如果正好有其它进程在访问该文件，通过 df 命令查看，删除的文件占用的空间是没有立即释放的。

解决方法：

使用root权限执行 lsof \|grep deleted ，查看正在使用被删除文件的进程的PID，通过命令 kill -9 PID 杀掉对应的进程即可。
