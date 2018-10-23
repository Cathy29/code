linux系统循环登录，无法进入桌面，ssh远程登录 很多命令无法正常使用：

可能是因为环境变量被改变 
ssh登录
echo $PATH
export $PATH为正确路径 一定要包括/usr/bin
改过之后就可以用命令了
vi /etc/profile
source /etc/profile
好啦～