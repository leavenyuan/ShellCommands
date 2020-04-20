# Ubuntu

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