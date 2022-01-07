# 信创
## 信创计算机运维工程师比赛整理
统信 Ubantu
apt install 
apt update
kylin centos
dnf install 
/etc/dnf/dnf.conf

### 软件
git
下载git openssh
git config --global user.name "用户名"
git config --global user.email "邮箱"
初始话仓库
mkdir test
cd test

git init
ssh-keygen 
密码空
cat ~/.ssh/id_rsa.pub

复制到git设置中的ssh配置

克隆仓库
git clone http://www.github.com:用户名/仓库
git clone git@github.com:用户名/仓库
添加仓库文件
git add 文件名
git commit -m "描述信息"
git push -u origin master/main
测试连接与否
ssh -t git@www.github.com

配置打印机
dnf install cups
启动服务
service 服务名 操作
service cups start/restart/

