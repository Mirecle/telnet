# ubuntu 下的 telnet 配置说明 

标签（空格分隔）： linux


>不知道为什么，突然想在虚拟机上实现telnet 远程登录的实践
其实很简单：

### 1、	首先查看 netstat –a|grep telnet
```netstat –a|grep telnet```
发现输出为空，表示没有开启该服务。（这个地方我纳闷了很久，我想着是不是我telnet没装）

---

###2、	安装 openbsd-inetd
（关于openbsd－inetd 的介绍看下链接https://blog.csdn.net/a1964543590/article/details/69485836
```apt-get install openbsd-inetd```
如果已经安装完成了，会提示安装过了，直接跳过。

---

###4、	安装telnetd
安装完之后，查看/etc/inetd.conf的内容多了一行

```cat /etc/inetd.conf  | grep telnet```
>输出： telnet stream  tcp nowait  telnetd /usr/sbin/tcpd /usr/sbin/in.telnetd
![img](/Users/mac/Pictures/图片1.png)
---

###5、重启openbsd-inetd
```/etc/init.d/openbsd-inetd restart```
>输出：* Restarting internet superserver inetd

---

###6、查看telnet运行状态
```netstat -a | grep telnet```
>输出：tcp　　0　　0 *:telnet　　*:*　　LISTEN

此时表明已经开启了telnet服务。
###7、telnet登陆测试
```telnet 127.0.0.1```
输出：
>Trying 127.0.0.1...
Connected to 127.0.0.1.e
Escape character is '^]'. （停在这里的时候要按Ctrl+） 然后回车）
telnet>  （表示登陆成功）


----------


内容整理自<https://blog.csdn.net/a1964543590/article/details/69485836>



