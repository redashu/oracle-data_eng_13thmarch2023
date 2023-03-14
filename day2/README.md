## hadoop by apache foundation -- hadoop v2 / hadoop v3 

### setup of hadoop v3 / v2 -- multinode cluster -- 1 namenode , 2 datanode 

<img src="setup.png">

### creating 3 vms of oracle linux / redhat linux / amazon linux / ubuntu 20 or later 
### i am using ubuntu linux 22 

## common steps to all the vm 

### checking os version 
```
ubuntu@ip-172-31-37-1:~$ cat /etc/os-release 
PRETTY_NAME="Ubuntu 22.04.1 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.1 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy

```

### update apt repo 

```
ubuntu@ip-172-31-37-1:~$ sudo apt update 
Hit:1 http://ap-south-1.ec2.archive.ubuntu.com/ubuntu jammy InRelease
Get:2 http://ap-south-1.ec2.archive.ubuntu.com/ubuntu jammy-updates InRelease [119 kB]
Get:3 http://security.ubuntu.com/ubuntu jammy-security InRelease [110 kB]             

```

### Installing jdk8 & setup path of java 

```
ubuntu@ip-172-31-37-1:~$ sudo apt install openjdk-8-jdk 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  adwaita-icon-theme alsa-topology-conf alsa-ucm-conf at-spi2-core ca-certificates-java dconf-gsettings-backend
  dconf-service fontconfig fontconfig-config fonts-d
  
  =========>checking java version 
  
  
  ubuntu@ip-172-31-37-1:~$ java -version 
openjdk version "1.8.0_362"
OpenJDK Runtime Environment (build 1.8.0_362-8u362-ga-0ubuntu1~22.04-b09)
OpenJDK 64-Bit Server VM (build 25.362-b09, mixed mode)
ubuntu@ip-172-31-37-1:~$ 

===============> setup java path 

ubuntu@ip-172-31-37-1:~$ cd  /usr/lib/jvm/
ubuntu@ip-172-31-37-1:/usr/lib/jvm$ ls
java-1.8.0-openjdk-amd64  java-8-openjdk-amd64
ubuntu@ip-172-31-37-1:/usr/lib/jvm$ cd java-8-openjdk-amd64/
ubuntu@ip-172-31-37-1:/usr/lib/jvm/java-8-openjdk-amd64$ ls
ASSEMBLY_EXCEPTION  THIRD_PARTY_README  bin  docs  include  jre  lib  man  src.zip
ubuntu@ip-172-31-37-1:/usr/lib/jvm/java-8-openjdk-amd64$ pwd
/usr/lib/jvm/java-8-openjdk-amd64
ubuntu@ip-172-31-37-1:/usr/lib/jvm/java-8-openjdk-amd64$ vim  ~/.bashrc 
ubuntu@ip-172-31-37-1:/usr/lib/jvm/java-8-openjdk-amd64$ tail -4  ~/.bashrc 

export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
PATH=$PATH:$JAVA_HOME/bin
export PATH
ubuntu@ip-172-31-37-1:/usr/lib/jvm/java-8-openjdk-amd64$ source ~/.bashrc 
ubuntu@ip-172-31-37-1:/usr/lib/jvm/java-8-openjdk-amd64$ 
ubuntu@ip-172-31-37-1:/usr/lib/jvm/java-8-openjdk-amd64$ echo $JAVA_HOME
/usr/lib/jvm/java-8-openjdk-amd64


```

### Download apache hadoop tar 

```

ubuntu@ip-172-31-37-1:~$ wget https://downloads.apache.org/hadoop/common/hadoop-3.2.4/hadoop-3.2.4.tar.gz
--2023-03-14 05:02:01--  https://downloads.apache.org/hadoop/common/hadoop-3.2.4/hadoop-3.2.4.tar.gz
Resolving downloads.apache.org (downloads.apache.org)... 88.99.95.219, 135.181.214.104, 2a01:4f9:3a:2c57::2, ...
Connecting to downloads.apache.org (downloads.apache.org)|88.99.95.219|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 492368219 (470M) [application/x-gzip]
Saving to: ‘hadoop-3.2.4.tar.gz’

hadoop-3.2.4.tar.gz            43%[====================>                             ] 203.70M 

====>
tar xvzf  hadoop-3.2.4.tar.gz
ubuntu@ip-172-31-37-1:~$ ls
hadoop-3.2.4  hadoop-3.2.4.tar.gz

```







