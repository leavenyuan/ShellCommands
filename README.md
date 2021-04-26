# Ubuntu

[Different between bash and shell](https://stackoverflow.com/questions/5725296/difference-between-sh-and-bash)

## Install git

```s
sudo add-apt-repository ppa:git-core/ppa
sudo apt-get update
sudo apt-get install git
```

## Install VSCode

```s
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
sudo apt-get update
sudo apt-get install code # or code-insiders
```

## Install gvm (VPN)

```s
bash < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)
sudo apt-get install bison
```

## Install Golang

```s
sudo add-apt-repository ppa:gophers/go
sudo apt-get update
# sudo apt-get install golang-stable
sudo apt-get install golang
```

## Backgroud task on Linux
```sh
option1:
   screen -S jmeter_ac -d -m bash -c './jmeter.sh -n -t Requests.jmx -l log'
option2:
   nohup kubectl logs -f pod-name --tail 0  > ~/log &

```

## Install nvm

```s
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
source ~/.bashrc
```

## Install node

```s
nvm install --lts=carbon
nvm use --lts=carbon
```

## Install Docker

```s
sudo apt-get remove docker docker-engine docker.io
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-get update
sudo apt-get install docker docker.io
```

## Install JDK

```s
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer

sudo update-alternatives --config java
sudo update-alternatives --config javac
sudo update-java-alternatives -l
```

## Install JDK from tar

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


## Install JDK From Source File

```s
Download jdk-8u211-linux-x64.tar.gz from oracle website
tar zxvf jdk-8u211-linux-x64.tar.gz
java -version
```

## Install Wireshark

```s
sudo apt-get install wireshark
```

## Install ZAP

```s
tar -zxvf ZAP_2.7.0_Linux.tar.gz
```

## Install MySQL Workbench

```s
sudo apt-get install mysql-workbench
```

## Install Robotframework

```s
sudo pip install robotframework
sudo pip install selenium
sudo pip install robotframework-selenium2library
sudo apt-get install python-wxgtk2.8
sudo pip install robotframework-ride
ride.py
```

## Install Chrome

```s
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
sudo apt-get update
sudo apt-get install google-chrome-stable
```

## Install VLC

```s
sudo add-apt-repository ppa:n-muench/vlc
sudo apt-get update
sudo apt-get install vlc
```

## Install Sogou Pinyin
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

## Install Python3.7
```s
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
sudo apt install python3.7
```
## Run Python3.9 docker
```s
sudo docker run -it python:3.9
```

## Install package in weak network
```s
sudo python3 -m pip install requests -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com
```

## Install Sublime Text
```s
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
sudo apt-get update
sudo apt-get install sublime-text
complie: cmd+B
run: shift+cmd+B
```


## Install tcpdump
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

## Truncate a file, empty a file to zero size
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

## Install hashlib on Ubuntu occur error
```sh
hashlib module is installed by default (I think Python 2.6+). You are trying to install a backport of it created for forward compatibility of old Python versions.
Just do import hashlib and do your stuff.
```

## Check logs in Unix
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

## Frequent Used Commands
```s
su {username}
```

## alias
```sh
$ vi .bashrc
> alias test='ls -l'
$ source ./.bashrc
```

## source filename 与 sh filename 及./filename执行脚本的区别
```sh
当shell脚本具有可执行权限时，用sh filename与./filename执行脚本是没有区别的。
./filename是因为当前目录没有在PATH中，”.”是用来表示当前目录的。
sh filename：重新建立一个子shell，在子shell中执行脚本里面的语句，该子shell继承父shell的环境变量，但子shell新建的、改变的变量不会被带回父shell。
source filename：这个命令其实只是简单地读取脚本里面的语句依次在当前shell里面执行，没有建立新的子shell。那么脚本里面所有新建、改变变量的语句都会保存在当前shell里面。
```

## chmod chown 文件权限
   sudo chmod -R 777 /var/www

## 切换root权限
   sudo su
   
## 生效配置
   source /etc/profile

## mount and umount
   fdisk -u /dev/vdb   # 分区数据盘
   fdisk -lu /dev/vdb  # 查看分区信息
   mkfs.ext4 /dev/vdb1  # 格式化分区
   mount /dev/vdb1 /mnt  # 手动临时挂载
   cat /etc/fstab   # 查看/etc/fstab中的新分区信息
   umount /dev/hda5
   
   more:
   cp /etc/fstab /etc/fstab.bak  # 备份etc/fstab文件
   echo /dev/vdb1 /mnt ext4 defaults 0 0 >> /etc/fstab  # 开机自动挂载.将磁盘挂载到某个目录下（如/mnt下）
