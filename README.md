# shell commands

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
   exclue some word
   ```sh
   grep -v word
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
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
sudo apt install python3.7
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
last | grep sysadmin       # find the login history of the user: sysadmin
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

#### find不显示permission denied
      $ find . -iname "helm" -print 2>/dev/null
