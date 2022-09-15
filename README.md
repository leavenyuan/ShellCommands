# shell commands 🐚

#### 检查操作系统

	hostnamectl
	
#### 检查核数

	nproc

<details>
	<summary> Linux init、service、systemctl 三者区别 </summary>
	
init 是最初的进程管理方式
service 是init 的另一种实现
systemd 则是一种取代 initd 的解决方案
其中 systemctl 是 systemd 的主命令，用于管理系统以及服务。


init

历史上，Linux 的启动一直采用init 进程。
在类Unix 的计算机操作系统中，Init（初始化的简称）是在启动计算机系统期间启动的第一个进程。
Init 是一个守护进程，它将持续运行，直到系统关闭。它是所有其他进程的直接或间接的父进程。
因为init 的参数全在/etc/init.d目录下，所以使用 init 启动一个服务，应该这样做：
$ sudo /etc/init.d/nginx start


service

通过查看man 手册页可以得知，service是一个运行System V init的脚本命令。
那么什么是 System V init 呢？
也就是/etc/init.d 目录下的参数。
所以分析可知service 是去/etc/init.d目录下执行相关程序，服务配置文件的存放目录就是/etc/init.d.
使用 service 启动一个服务
$ service nginx start
可以理解成 service 就是init.d 的一种实现方式。
所以这两者启动方式（或者是停止、重启）并没有什么区别。
$ sudo /etc/init.d/nginx start
// 等价于
$ service nginx start
但是这两种方式均有如下缺点：
启动时间长。init 进程是串行启动，只有前一个进程启动完，才会启动下一个进程。
启动脚本复杂。init进程只是执行启动脚本，不管其他事情。脚本需要自己处理各种情况，这往往使得脚本变得很长。



systemd

Systemd 就是为了解决这些问题而诞生的。它包括 System and Service Manager，为系统的启动和管理提供一套完整的解决方案。
Systemd 是Linux 系统中最新的初始化系统（init），它主要的设计目的是克服 System V init 固有的缺点，提高系统的启动速度。
根据 Linux 惯例，字母d是守护进程（daemon）的缩写。 Systemd 这个名字的含义，就是它要守护整个系统。
使用了 Systemd，就不需要再用init 了。Systemd 取代了initd（Initd 的PID 是0） ，成为系统的第一个进程（Systemd 的PID 等于 1），其他进程都是它的子进程。
Systemd 的优点是功能强大，使用方便，缺点是体系庞大，非常复杂。
查看Systemd 的版本信息
$ systemctl --version

Systemd 并不是一个命令，而是一组命令，涉及到系统管理的方方面面。

systemctl
systemctl是 Systemd 的主命令，用于管理系统。
// 重启系统
$ sudo systemctl reboot
// 启动进入救援状态（单用户状态）
$ sudo systemctl rescue
// 管理服务
$ sudo systemctl start nginx

hostnamectl命令用于查看当前主机的信息。
// 显示当前主机信息
$ hostnamectl
   Static hostname: ubuntu
         Icon name: computer-laptop
           Chassis: laptop
        Machine ID: b5114b942a063c0d18870a896143220b
           Boot ID: 5903399a0b824c31a582fe3f99324c38
  Operating System: Ubuntu 16.04.7 LTS
            Kernel: Linux 4.4.0-186-generic
      Architecture: x86-64
// 设置主机名
$ sudo hostnamectl set-hostname BoodeUbuntu

localectl命令用于查看本地化设置。
// 查看本地化设置
$ localectl
// 设置本地化参数。
$ sudo localectl set-locale LANG=en_GB.utf8
$ sudo localectl set-keymap en_GB

timedatectl命令用于查看当前时区设置。
// 查看当前时区设置
$ timedatectl
// 显示所有可用的时区
$ timedatectl list-timezones                                                                                   
// 设置当前时区
$ sudo timedatectl set-timezone America/New_York


	
</details>





#### Linux终端彻底清空屏幕
```sh
Linux用户基本上都习惯使用clear命令或Ctrl+L组合快捷键来清空终端屏幕。这样做其实并没有真正地清空屏幕，但当用鼠标向上滚时，你仍然能看到之前的命令操作留下来的输出。

命令 printf “\033c” 或者 printf “\ec”真正地清空了终端屏幕.

它的工作原理是什么？\033 == \x1B == 27 == ESC 于是，这个命令变成了c，它是VT-XXX中表示“Full Reset (RIS)”的转义码。printf是bash里内置的命令，内置命令的优先级比其它可执行文件要高。

reset也是真正地清空终端屏幕。这个命令执行起来有点慢，但它的兼容性显然比之前的那个要好。reset命令在你的终端控制错乱时非常有用。
```

#### pid为1的进程systemd
[ref](https://shareinto.github.io/2019/01/30/docker-init(1)/)


#### docker-proxy
[ref](https://www.jianshu.com/p/91002d316185)


#### kill占用某个端口的进程及其相关进程
[ref link](https://blog.csdn.net/m0_37828989/article/details/115721880)
```sh
$ sudo -s
$ netstat -nlpt | grep 9094   #查看端口对应的进程占用
$ kill `lsof -t -i:9094`      # kill占用端口的所有进程
$ pstree -asp pid  # 查询该进程的依赖关系
$ systemctl stop pname   #停止进程
```

#### Systemctl命令常见用法

   -  列出所有可用单元文件：systemctl list-unit-files
   -  列出所有可用单元：systemctl list-units
   -  列出所有失败单元：systemctl --failed
   -  检查某个单元是否启动：systemctl is-enabled httpd.service
   -  检查某个服务的运行状态：systemctl status httpd.service
   -  列出所有服务：systemctl list-unit-files --type=service
   -  启动，停止，重启服务等：systemctl restart|restart|stop|reload httpd.service
   -  查询服务是否激活，和配置是否开机启动：systemctl is-active httpd
   -  使用systemctl命令杀死服务: systemctl kill httpd
   -  列出系统的各项服务，挂载，设备等：systemctl list-unit-files --type
   -  获得系统默认启动级别和设置默认启动级别：systemctl get-default/systemctl set-default multi-user.target
   -  启动运行等级：systemctl isolate multiuser.target
   -  重启、停止，挂起、休眠系统等：systemctl reboot|halt|suspend|hibernate|hybrid-sleep

```

#### 写入数据到某个文件的进程
```sh
比如我知道该文件目录下有这两个文件：
nebula@nebula:/opt/gateway-setup-v0.3.0/compose/data/symphony-agent/data.db$ ll
total 460
lrwxrwxrwx 1 root root     44 11月  4 11:49 active -> /opt/symphony/data.db/conn-10.53.24.51-32012
-rw------- 1 root root 524288 11月  8 14:44 conn-10.53.24.51-32012

于是我想知道写入这个文件的进程号
$ sudo lsof 2>/dev/null | grep conn-10.53.24.51-32012
symphony- 14437 14439             root  mem-W     REG                8,2              4063388 /opt/symphony/data.db/conn-10.53.24.51-32012 (stat: No such file or directory)
symphony- 14437 14439             root    3uW     REG                8,2    524288    4063388 /opt/symphony/data.db/conn-10.53.24.51-32012

通过返回，我看到了这个进程14437
$ sudo ps -ef | grep 14437
nebula   13628 12567  0 14:47 pts/0    00:00:00 grep --color=auto 14437
root     14437 14376  0 11月04 ?      00:19:56 /opt/symphony/symphony-agent serve --config /opt/symphony/config/config.yml --verbose

于是我找到了是这个进程在往conn文件中写入信息

```

#### 查找docker部署的服务连接某个服务
```sh

$ netstat a | grep 3307

tcp6       0      0 10.151.**.217:3307     172.29.0.14:35564       ESTABLISHED
tcp6       0      0 10.151.**.217:3307     172.29.0.14:35540       ESTABLISHED

$ docker network ls

$ docker network inspect f0e  #查找上面的 172.29.0.14

"cccf545eb7750192d6bb6b697800ecaec2652d23f718e4dc3d24a5e90bc7801e": {
                "Name": "compose_gateway_1",
                "EndpointID": "150939f9268670ae6cdabc23886545d8fdfee302a6f8a376da57fb5d2851e7e6",
                "MacAddress": "02:42:ac:1d:00:0e",
                "IPv4Address": "172.29.0.14/16",
                "IPv6Address": ""

```
#### 去除空格
```sh
$ echo "   lol  " | xargs

Note: this doesn't remove all internal spaces so "foo bar" stays the same; it does NOT become "foobar". However, multiple spaces will be condensed to single spaces, so "foo    bar" will become "foo bar". In addition it doesn't remove end of lines characters.

$ echo "   3918912k " | sed 's/ //g'


```

#### diff比较两个string
```sh
$ diff  <(echo "$string1" ) <(echo "$string2")

or with a named pipe

$ mkfifo ./p
$ diff - p <<< "$string1" & echo "$string2" > p

Greg's Bash FAQ: Working with Named Pipes

Named pipe is also known as a FIFO.

The - on its own is for standard input.

<<< is a "here string".

& is like ; but puts it in the background
```

#### apt
```sh
# check version of installed package
$ apt-cache policy [package name]
```

#### Calculate file numbers recursively
```sh
$ find [filePath] -type f | wc -l
```

#### check mtime, ctime, atime of a file
```sh
# Modified timestamp indicates the last time the contents of a file were modified.
$ ls -l [filename]   

# Changed timestamp indicates the last time some metadata of a file was changed.
$ ls -lc [filename]

# Access timestamp refers to the last time a file was read by a user.
$ ls -lu [filename]
```

#### 设置开启启动
```sh
https://www.cnblogs.com/downey-blog/p/10473939.html

[Unit]
Description=
Documentation=
After=network.target
Wants=
Requires=

[Service]
ExecStart=/home/downey/test.sh
ExecStop=
ExecReload=/home/downey/test.sh
Type=simple

[Install]
WantedBy=multi-user.target


sudo systemctl start test.service  
sudo systemctl enable test.service  
```

#### 检查系统重启历史
```sh
last reboot
```


#### netstat
```sh
Below result returned while I perfoming invoking interface expose on 18020 on 10.151.116.214, so there is a ESTABLISHED record.

root@cn0614006923l:~# netstat -anpt | grep 18020
tcp6       0      0 :::18020                :::*                    LISTEN      28188/symphony-agen 
tcp6       0    247 10.151.116.214:18020    10.151.124.65:58701     ESTABLISHED 28188/symphony-agen 
```


#### lsof

每隔2秒查询端口被谁连接

```sh
lsof -i :18001 -r 2
```

#### netcat
```sh
apt get install netcat
nc -l -p 33902  # listen on port
nc localhost 33902   # another server

# transmit tar file
接收端: nc -l 9009 > tar -xzv
发送端: tar -zcvf - foldername |  nc in-server-ip 9009

接收端: nc -l 9555 > file
发送端: nc [接收端 ip] 9555 < file
validate: md5sum [filename]

```

#### add root user  and enable root login via ssh

```sh
$ sudo passwd root 
# enter： 输入当前用户密码，并输入两次新密码
$ su root

$ vi /etc/ssh/sshd_config
________________
# Authentication:
#LoginGraceTime 2m
PermitRootLogin yes
#StrictModes yes
#MaxAuthTries 6
#MaxSessions 10
________________

$ service sshd restart

```

#### download file from telnet

   1. telnet 10.151.116.222 23023 | tee telnet.log
   2. 将要写入到telnet.log的文件写出到stdout
   3. exit
   4. vi/cat telnet.log


### grep(s)

   grep from previous output & grep result meet any item in given list
   ```sh   
   cat nohup.out  | grep test_ | tee tempfile | grep -v line | tee tempfile | grep -E "ERR|OK|FAIL"
   ```
   exclue some word, excluede multiple word
   ```sh
   grep -v word
   egrep -v "kibana|nacos|rocket|web"
   ```
   
   match whole word
   ```sh
   grep -w word
   ```
   
   colour the matched
   ```sh
   grep word --colour
   ```

- output to file

   if you want stderr as well use this:
   ```sh
   SomeCommand &> SomeFile.txt
   ```
   or this to append:
   ```sh
   SomeCommand &>> SomeFile.txt  
   ```
   if you want to have both stderr and output displayed on the console and in a file use this:
   ```sh
   SomeCommand 2>&1 | tee SomeFile.txt
   ```

[Different between bash and shell](https://stackoverflow.com/questions/5725296/difference-between-sh-and-bash)


#### xargs
   - cat filename | xargs     #输出去除换行符的文本
      
      
#### sed
   - sed -i 's/xx/yy/g' filename      # -i: 将替换作用于源文件， g: 替换所有的匹配

#### Install git

```s
sudo add-apt-repository ppa:git-core/ppa
sudo apt-get update
sudo apt-get install git
```

#### Install VSCode

```s
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
sudo apt-get update
sudo apt-get install code # or code-insiders
```

#### Install gvm (VPN)

```s
bash < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)
sudo apt-get install bison
```

#### Install Golang

```s
sudo add-apt-repository ppa:gophers/go
sudo apt-get update
# sudo apt-get install golang-stable
sudo apt-get install golang
```

#### Backgroud task on Linux
```sh
option1:
   screen -S jmeter_ac -d -m bash -c './jmeter.sh -n -t Requests.jmx -l log'
option2:
   nohup kubectl logs -f pod-name --tail 0  > ~/log &
option3:
   setsid tail -f xx.log &> tail.log
   
几种方式的原理解析: https://www.playpi.org/2019051501.html
```

#### Install nvm

```s
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
source ~/.bashrc
```

#### Install node

```s
nvm install --lts=carbon
nvm use --lts=carbon
```

#### Install Docker

```s
sudo apt-get remove docker docker-engine docker.io
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-get update
sudo apt-get install docker docker.io
```

#### Install JDK

```s
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer

sudo update-alternatives --config java
sudo update-alternatives --config javac
sudo update-java-alternatives -l
```

#### Install JDK from tar

```s
1. download JDK from oracle website
2. mkdir /usr/local/java/
3. tar -zxvf jdk-8u171-linux-x64.tar.gz -C /usr/local/java/
4. vim /etc/profile
   添加
export JAVA_HOME=/usr/local/java/jdk1.8.0_171
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
5. source /etc/profile
6. ln -s /usr/local/java/jdk1.8.0_171/bin/java /usr/bin/java
6. java -version
```


#### Install JDK From Source File

```s
Download jdk-8u211-linux-x64.tar.gz from oracle website
tar zxvf jdk-8u211-linux-x64.tar.gz
java -version
```

#### Install Wireshark

```s
sudo apt-get install wireshark
```

#### Install ZAP

```s
tar -zxvf ZAP_2.7.0_Linux.tar.gz
```

#### Install MySQL Workbench

```s
sudo apt-get install mysql-workbench
```

#### Install Robotframework

```s
sudo pip install robotframework
sudo pip install selenium
sudo pip install robotframework-selenium2library
sudo apt-get install python-wxgtk2.8
sudo pip install robotframework-ride
ride.py
```

#### Install Chrome

```s
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
sudo apt-get update
sudo apt-get install google-chrome-stable
```

#### Install VLC

```s
sudo add-apt-repository ppa:n-muench/vlc
sudo apt-get update
sudo apt-get install vlc
```

#### Install Sogou Pinyin
```s
Step1:
Install Fcitx in that Sogou Pinyin develop based on fcitx keyboard input system, while Ubuntu's default one is iBus

Step2:
Install Sogou Pinyin

Step3:
Configuration

Step1 Details:
    1. Add repository
    sudo add-apt-repository ppa:fcitx-team/nightly
    2. Update apps managed by apt
    sudo apt-get update
    3. Install Fcitx
    sudo apt-get install fcitx
    4. Install configuration tools for fcitx
    sudo apt-get install fcitx-config-gtk
    5. Install fcitx table-all
    sudo apt-get install fcitx-table-all
    6. Verify installation of fcitx in Installed apps
    Search fcitx
    
Step2 Details:
    1. Download 32-bit/64-bit Sogou Pinyin Installer for Linux from official website
    2. sudo dpkg -i sogoupinyin_2.3.1.0112_amd64.deb
    3. Ignore error like "No such key 'Gtk/IMModule' in schema 'org.gnome.settings-daemon.plugins.xsettings' as specified in   override file '/usr/share/glib-2.0/schemas/50_sogoupinyin.gschema.override'; ignoring override for this key.
    
Step3 Details:
    1. Configure <Language Support>, modify <Keyboard input method system> from defualt iBus to fcitx
    2. log out and log in
    3. Configure Fcitx, click "+" to add "Sogou Pinyin" 
    4. Switch to Sogou input
    
```

#### Install Python3.7
```s
------ install from repo -----
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
sudo apt install python3.7

----- install from source code -----
$ sudo apt update
$ sudo apt install build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libsqlite3-dev libreadline-dev libffi-dev wget libbz2-dev
$ wget https://www.python.org/ftp/python/3.7.4/Python-3.7.4.tgz
$ tar -xf Python-3.7.4.tgz
$ cd Python-3.7.4
$ ./configure --enable-optimizations
$ make -j 8(core numbers)
$ sudo make altinstall




```
#### Run Python3.9 docker
```s
sudo docker run -it python:3.9
```

#### Install package in weak network
```s
sudo python3 -m pip install requests -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com
```

#### Install Sublime Text
```s
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
sudo apt-get update
sudo apt-get install sublime-text
complie: cmd+B
run: shift+cmd+B
```


#### Install tcpdump
```s
Download the rpm package for tcpdump.
Log in to DSVA via SSH as DSVA user. The default password is “dsva”.
Switch to root user using this command: $sudo -s
Upload the package to DSVA under path:/home/dsva. You can use WinSCP for the transmission.
Unpack the tar package:

$ tar xzvf tcpdump_dsva9.5.tar.gz
libpcap-1.4.0-1.20130826git2dbcaa1.el6.x86_64.rpm
tcpdump-4.0.0-3.20090921gitdf3cb4.2.el6.x86_64.rpm

Install the rpm packages:

$ rpm -ivh tcpdump-4.0.0-3.20090921gitdf3cb4.2.el6.x86_64.rpm

$ tcpdump -h
```

#### Truncate a file, empty a file to zero size
```s
Method1:
    : > filename

    ":" means True and produces no output
    ">" redircts the output of preceding output to the following file

Method2: output the content of /dev/null device, which returns only an end-of-file character 
    cat /dev/null > filename

Method3:
    echo -n > filename
    "-n" option tells echo not to append a newline
```

#### Install hashlib on Ubuntu occur error
```sh
hashlib module is installed by default (I think Python 2.6+). You are trying to install a backport of it created for forward compatibility of old Python versions.
Just do import hashlib and do your stuff.
```

#### Check logs in Unix
```sh
ls -l /var/log             # what is logged
who                        # see who logged in
last | grep sysadmin       # 
the login history of the user: sysadmin
cat /etc/rsyslog.conf     #LOG FILE SUMMARY

direcotry:
/var/log/messages    # log messages
/var/log/cron        # Log cron stuff
/var/log/boot.log    #  Save boot messages also to boot.log
```

#### Frequent Used Commands
```s
su {username}
```

#### alias
```sh
$ vi .bashrc
> alias test='ls -l'
$ source ./.bashrc
```

#### source filename 与 sh filename 及./filename执行脚本的区别
```sh
当shell脚本具有可执行权限时，用sh filename与./filename执行脚本是没有区别的。
./filename是因为当前目录没有在PATH中，”.”是用来表示当前目录的。
sh filename：重新建立一个子shell，在子shell中执行脚本里面的语句，该子shell继承父shell的环境变量，但子shell新建的、改变的变量不会被带回父shell。
source filename：这个命令其实只是简单地读取脚本里面的语句依次在当前shell里面执行，没有建立新的子shell。那么脚本里面所有新建、改变变量的语句都会保存在当前shell里面。
```

#### chmod chown 文件权限
   sudo chmod -R 777 /var/www

#### 切换root权限
   sudo su
   
#### 生效配置
   source /etc/profile


<details>
   <summary> mount and umount </summary>

   ```sh
   fdisk -u /dev/vdb   # 分区数据盘
   fdisk -lu /dev/vdb  # 查看分区信息
   mkfs.ext4 /dev/vdb1  # 格式化分区
   mount /dev/vdb1 /mnt  # 手动临时挂载
   cat /etc/fstab   # 查看/etc/fstab中的新分区信息
   umount /dev/hda5
   
   more:
   cp /etc/fstab /etc/fstab.bak  # 备份etc/fstab文件
   echo /dev/vdb1 /mnt ext4 defaults 0 0 >> /etc/fstab  # 开机自动挂载.将磁盘挂载到某个目录下（如/mnt下）
   
   遇到报错: Mount: /dev/xxx already mounted or /mnt busy
   dmsetup ls
   dmsetup remove xxxxxx
   dmsetup ls
   ```
</details>

   
#### systemctl 
   ```sh
   # check service logs
   journalctl -u docker.service
   
   ```
   
   [uninstall docker](https://askubuntu.com/questions/935569/how-to-completely-uninstall-docker)
   
#### Install ssh
   [how to enable ssh on ubuntu](https://linuxize.com/post/how-to-enable-ssh-on-ubuntu-20-04/)
   
   
   
<details>
   <summary> Opening a port on Linux </summary>
   
   ### 1.List all open ports
      We can use the netstat command to list all open ports, including those of TCP, UDP, which are the most common protocols for packet transmission in the network layer.
      NOTE: If your distribution doesn’t have netstat, it is not a problem. You can use the ss command to display open ports via listening sockets.
   ```sh
      netstat -lntu
   ```
      This will print all listening sockets (-l) along with the port number (-n), with TCP ports (-t) and UDP ports (-u) also listed in the output.
   
      OR
   ```sh
      ss -lntu
   ```
   
   ### 2. Opening a port on Linux to Allow TCP Connections
      
      Let’s open a closed port and make it listen to TCP Connections, for the sake of this example.

      Since port 4000 is not being used in my system, I choose to open port 4000. If that port is not open in your system, feel free to choose another closed port. Just make sure that it’s greater than 1023!

      Again, just to make sure, let’s ensure that port 4000 is not used, using the netstat or the ss command.
   ```sh
      netstat -na | grep :4000
      ss -na | grep :4000
   ```
      The output must remain blank, thus verifying that it is not currently used, so that we can add the port rules manually to the system iptables firewall.
   
   #### 2.1 For Ubuntu Users and ufw firewall based Systems
   ```sh
   sudo ufw allow 4000
   ```
   
   #### 2.2 For CentOS and firewalld based Systems
      For these types of systems, if you have firewalld as your primary firewall, it is recommended that you use the firewall-cmd to update your firewall rules, instead of the old iptables firewall.
   ```sh
      firewall-cmd --add-port=4000/tcp
   ```
      NOTE: This will reset the firewalld rules to default on a reboot, so if you want to modify this setting permanently, add the --permanent flag to the command.
   ```sh
      firewall-cmd --add-port=4000/tcp --permanent
   ```

   ### 3. Test the newly opened port for TCP Connections
      First, we will start netcat (nc) and listen on port 4000, while sending the output of ls to any connected client. So after a client has opened a TCP connection on port 4000, they will receive the output of ls.
   ```sh
      ls | nc -l -p 4000
   ```
      This makes netcat listen on port 4000. Leave this session alone for now.
      Open another terminal session on the same machine.
      Since I’ve opened a TCP port, I’ll use telnet to check for TCP Connectivity. If the command doesn’t exists, again, install it using your package manager.
      Format for telnet:
   
   ```sh
      telnet [hostname/IP address] [port number]
   ```
   
   ### 4. Need to update rules after every reboot
      The approach presented in this article will only temporarily update the firewall rules until the system shuts down/reboots. So similar steps must be repeated to open the same port again after a restart.
   #### 4.1 For ufw Firewall
      The ufw rules are not reset on reboot, so if you’re a Ubuntu user, you need not worry about this part!
      This is because it is integrated into the boot process and the kernel saves the firewall rules using ufw, via appropriate config files.
   #### 4.2 For firewalld
      As mentioned earlier, firewalld also suffers from the same problem, but this can be avoided by appending a --permananent flag to the initial command, when opening a port or setting any other rule.
      For example, you can open the TCP Port 4000 permanently using the below command:
   ```sh
      firewall-cmd --zone=public --add-port=400/tcp --permanent
   ```
   #### 4.3 For iptables
      For the iptables firewall, although this inconvenience cannot be avoided, we could minimize the hassle.
      We can save the iptables rules to a config file, such as /etc/iptables.conf.
   ```sh
      sudo iptables-save | sudo tee -a /etc/iptables.conf
   ```
      We can then retrieve it from the config file after we reboot, using the below command:
   ```sh
      sudo iptables-restore < /etc/iptables.conf
   ```
</details>

   
   
#### crontab python脚本不执行分析&解决
      $ sudo tail -f /var/mail/xiaolu    #输出crontab的执行命令和返回
      $  tail /var/log/syslog -f
      在服务器直接执行py，打出sys.path, 发现python为 /usr/local/lib/python3.7
      crontab触发执行py,python为 /usr/lib/python3.7
      $ crontab -e
      # 注意执行的文件要能定位到，比如./要加上
      */10 * * * *  cd /home/xiaolu/automation-aix && /usr/local/bin/python3.7 ./tests/api/perf/Face_record_postback_multiprocessing.py > /dev/null >2&1
      * * * * *  cd /home/xiaolu/automation-aix && git add ./tests/api/perf/report.md && git commit -m "commit report" && git push origin Gateway >/dev/null >2&1

#### 修改网络配置和DNS
   ```sh
   # Debian/Ubuntu OS
   $ vi /etc/network/interfaces
   auto lo
   iface lo inet loopback

   auto ens3
   iface ens3 inet static        #IPv4配置
   address 132.98.174.248       #IPv4
   gateway 132.98.174.193       #IPv4网关
   netmask 255.255.255.192      #子网掩码

   iface ens3 inet6 static       #IPv6配置
   address 1200:7e45:0:f6::1e4a:3705    #IPv6地址
   netmask 48   #掩码
   gateway 1200:7e45:0:f6::1    #IPv6网关

   iface ens3 inet6 static
   address 1200:7e45:0:f6::235e:3b7e  #添加额外IPv6地址
   netmask 48 #掩码
   
   # 生效
   $ 执行 sudo /etc/init.d/networking restart
   $ reboot
   
   # for more usage
   $ man interfaces
   
   
   # RedHat
   $ vi /etc/sysconfig/network-scripts
   
   ```
   
   
   ```sh
   # 修改DNS
   $ vi /etc/resolv.conf
   ```
   

#### 1. Compare paramter 参数的比较 [Bash warning - argument expected](https://stackoverflow.com/questions/29178135/bash-warning-argument-expected)
```
if [ ${OUTPUT} = "" ]
                   ^--- Required
if [ "${OUTPUT}" = "" ]
     ^-- Here -^
```     
#### shell脚本中用awk避免unexpected newline or end of string报错
```
xxx.sh
ssh root@${ip} 'helm list --col-width 200 | sed 1d | awk '{print $9}' | sort | uniq'

改成
line='$9'
ssh root@${ip} "helm list --col-width 200 | sed 1d | awk '{print $line}' | sort | uniq"
   
# 分隔符取列
  cat filename | awk -F "msg=" '{print $2}' | sort | uniq
```

#### shell脚本中要远程登录目标机器并执行命令
```s
if [ -z "$1" ];
then
ip="";
else
ip=$1;
fi

ssh root@${ip} 'kubectl logs -f -n nebula podname --tail 0' > ./${filename}.txt

```
#### Multiple threads in shell script比如发送请求同时记录日志
```s
read_cfg cfgA &
read_cfg cfgB &
read_cfg cfgC &
wait

all those jobs will then run in the background simultaneously. The optional wait command will then wait for all the jobs to finish.
```
#### while循环总是为true的写法
```s
Colon is always "true":
while :; do foo; sleep 2; done
```

```s
preparation step:
echo $SHELL
>>> /bin/bash
$SHELL --version
>>> GNU bash, version 4.3.48(1)-release (x86_64-pc-linux-gnu)
version_local=`echo $chart_local | sed "s/aurora-//g"`;  //correct, match rest of content except quried
version_local=`echo $(chart_local) | sed "s/aurora-//g"`;  //chart_local: not found
```

#### find用法
   * find不显示permission denied
   ```sh
   $ find . -iname "helm" -print 2>/dev/null
   ```
   * find 排除某些文件
   ```sh
   $ find . -type f ! -name "*.log*" | xargs grep -i bucketname --colour
   ```
   
   * find and remove
   ```sh
   $  find . -type f -name "*.log" -exec rm {} \;
   ```
   
   * find file by size
   ```sh
   find . -size +100000k 2>/dev/null
   ```
   
   * 从指定文件夹查找
   ```sh
   find ./tests -type f | xargs grep -i "tag" --colour
   ```

#### 标准输出重定向
   ```sh
   0 */3 * * * /usr/local/apache2/apachectl restart >/dev/null 2>&1
   “/dev/null 2>&1”表示先将标准输出重定向到/dev/null，然后将标准错误重定向到标准输出，由于标准输出已经重定向到了/dev/null，因此标准错误也会重定向到/dev/null，这样日志输出问题就解决了。
   /dev/null（或称空设备）在类Unix系统中是一个特殊的设备文件，它丢弃一切写入其中的数据（但报告写入操作成功），读取它则会立即得到一个EOF[1]。
   在程序员行话，尤其是Unix行话中，/dev/null被称为比特桶[2]或者黑洞。
   ```

#### 重启命令比较

   ```sh
   init 6 Stop the operating system and reboot to the state defined by the initdefault entry in /etc/inittab.

reboot - reboot performs a sync(1M) operation on the disks, and then a
multi- user reboot is initiated. See init(1M) for details.

"init 6" 基于一系列/etc/inittab文件，并且每个应用都会有一个相应shutdown脚本。
'init 6' 调用一系列shutdown脚本(/etc/rc0.d/K*)来使系统优雅关机;
'reboot'并不执行这些过程，reboot更是一个 kernel级别的命令，不对应用使用shutdown脚本。 .
我们应该在通常情况下使用 init 6.
在出问题的状况下或强制重启 时使用reboot.

reboot is a more aggresive command to use. init 6 is much graceful

use of `init 6` will give the cleanest and orderly reboot (init informs svc.startd of the runlevel change and will move to the appropriate milestone).
use of `shutdown -y -g0 -i6 **message**` will invoke init as well as give you grace period and messages to user (shutdown invoked the same as init above).
halt,reboot,poweroff will not run any of the shutdown scripts and should be last resort.
   ```

#### add alias in bash on mac
   
   ```sh
   1. cd ~
   2. touch ./bash_profile
   3. vi ./bash_profile
      alias ll="ls -l"
   4. source ./bash_profile
   ```

#### 设置字符集

查询当前字符集: $ locale

设置项: export LANG="en_US.UTF-8"

可通过修改以下文件设置，一般为 ~/bash_profile

| 文件名  | 描述 |
| ------------- | ------------- |
| /etc/profile | 此文件为系统的每个用户设置环境信息,当用户第一次登录时,该文件被执行. 并从/etc/profile.d目录的配置文件中搜集shell的设置. |
| /etc/bashrc | 为每一个运行bash shell的用户执行此文件.当bash shell被打开时,该文件被读取. |
| ~/.bash_profile | 每个用户都可使用该文件输入专用于自己使用的shell信息,当用户登录时,该文件仅仅执行一次!默认情况下,他设置一些环境变量,执行用户的.bashrc文件. |
| ~/.bashrc | 该文件包含专用于你的bash shell的bash信息,当登录时以及每次打开新的shell时,该文件被读取. |
| ~/.bash_logout | 当每次退出系统(退出bash shell)时,执行该文件. |


#### 安装anaconda

```
下载指定版本: https://repo.anaconda.com/archive/
赋予可执行权限: chmod +x Anaconda...sh
执行安装: ./Anaconda...sh
sudo vi ~/.bashrc 在文件末尾添加一行: export PATH=/root/anaconda3/bin:$PATH
检查版本: conda -V
[installation step-by-step](https://blog.csdn.net/wyf2017/article/details/118676765)	
```




