## 快速安装

- 鱼香ros插件安装
```bash
pip3 install distro
```

- 一键安装鱼香ros，配置国内源
- 安装VSCode + Chinese + Python + Background + C/C++及Pack
```bash
wget http://fishros.com/install -O fishros && . fishros
```

- 登录火狐浏览器
账号：hanbo_shi@163.com
密码：xxxx

- Github配置
```bash
sudo apt install git
```

```bash
ssh-keygen -t ed25519 -C "hanbo_shi@163.com" # 生成新的 SSH 密钥
eval "$(ssh-agent -s)" # 启动ssh代理
ssh-add ~/.ssh/id_ed25519 # 添加私钥
cat ~/.ssh/id_ed25519.pub # 全选复制
```
在Github设置界面找到SSH配置即可

- GCC安装
```bash
sudo apt install gcc
```

- SSH安装
```bash
# 安装网络工具，方便后续查看ubuntu的网络ip
sudo apt install net-tools
# 安装ssh
sudo apt install openssh-server 
sudo /etc/init.d/ssh start # 启动服务
# 查看ssh是否运行 
ps -e|grep ssh 
# 查看本机ip 
ifconfig
```

方法一：VSCode安装SSH插件，设置页面配置进入方法
```bash
Host ubuntu_2204 //随便起
    HostName 192.168.200.136 //修改为你自己的IP
    User robot
    Port 22
```

方法二：本机电脑终端进入方法
```
ssh -p 22 robot@192.168.32.141
```

- CMake安装
下载后解压  [官方下载链接](https://cmake.org/files/v3.15/)
```bash
tar -xzvf cmake-3.15.3-Linux-x86_64.tar.gz /home/robot/work/
cmake --version
```


## 板卡ADB调试

ADB原来是Android开发者工具包中的一个工具，用于 Android 应用开发和设备调试的，而现在，芯片公司的Linux SDK都已经移植了这个工具，现在我们也可以<mark style="background: #ABF7F7A6;">使用ADB指令对Linux系统进行开发和调试</mark>。​

**ADB安装**
```bash
sudo apt install adb -y
```

**ADB常用指令**
对于ADB，我们先了解以下几条常用指令即可

```c
adb devices //列出电脑上连接的设备
adb shell   //进入开发板设备的 shell 环境
```

如果我们需要把电脑的文件发送到开发板，或者开发板的文件下载到电脑，应该如何做呢？
```C
adb push <local> <remote> //从电脑传输文件到设备
adb pull <remote> <local> //从设备传输文件到电脑

FYI：
adb push file.txt /data
adb pull /data/file.txt ./
```
