---
layout:		post
title:		Bash and Vim
subtitle:	常用指令和快捷键
date:		2019-08-24
author:		LLX
header-img:	img/post-bg-2015.jpg
catalog:	true
tags:
    - Linux
---

## Bash
### 常用快捷键（默认使用 Emacs 键位）
```
CTRL+A              # 移动到行首，同 <Home>
CTRL+B              # 向后移动，同 <Left>
CTRL+C              # 结束当前命令
CTRL+D              # 删除光标前的字符，同 <Delete> ，或者没有内容时，退出会话
CTRL+E              # 移动到行末，同 <End>
CTRL+F              # 向前移动，同 <Right>
CTRL+G              # 退出当前编辑（比如正在 CTRL+R 搜索历史时）
CTRL+H              # 删除光标左边的字符，同 <Backspace>
CTRL+K              # 删除光标位置到行末的内容
CTRL+L              # 清屏并重新显示
CTRL+N              # 移动到命令历史的下一行，同 <Down>
CTRL+O              # 类似回车，但是会显示一行历史
CTRL+P              # 移动到命令历史的上一行，同 <Up>
CTRL+R              # 历史命令反向搜索，使用 CTRL+G 退出搜索
CTRL+S              # 历史命令正向搜索，使用 CTRL+G 退出搜索
CTRL+T              # 交换前后两个字符
CTRL+U              # 删除字符到行首
CTRL+V              # 输入字符字面量，先按 CTRL+V 再按任意键
CTRL+W              # 删除光标左边的一个单词
CTRL+X              # 列出可能的补全
CTRL+Y              # 粘贴前面 CTRL+u/k/w 删除过的内容
CTRL+Z              # 暂停前台进程返回 bash，需要时可用 fg 将其切换回前台
CTRL+_              # 撤销（undo），有的终端将 CTRL+_ 映射为 CTRL+/ 或 CTRL+7
ALT+b               # 向后（左边）移动一个单词
ALT+d               # 删除光标后（右边）一个单词
ALT+f               # 向前（右边）移动一个单词
ALT+t               # 交换前后两个单词
ALT+BACKSPACE       # 删除光标前面一个单词，类似 CTRL+W，但不影响剪贴板
CTRL+X CTRL+X       # 连续按两次 CTRL+X，光标在当前位置和上一位置来回跳转 
CTRL+X CTRL+E       # 用你指定的编辑器，编辑当前命令
```
### 基本操作
```
exit                # 退出当前登陆
env                 # 显示环境变量
echo $SHELL         # 显示你在使用什么 SHELL
bash                # 使用 bash，用 exit 返回
which bash          # 搜索 $PATH，查找哪个程序对应命令 bash
whereis bash        # 搜索可执行，头文件和帮助信息的位置，使用系统内建数据库
whatis bash         # 查看某个命令的解释，一句话告诉你这是干什么的
clear               # 清初屏幕内容
reset               # 重置终端（当你不小心 cat 了一个二进制，终端状态乱掉时使用）
```
### 目录操作
```
cd                  # 返回自己 $HOME 目录
cd {dirname}        # 进入目录
pwd                 # 显示当前所在目录
mkdir {dirname}     # 创建目录
mkdir -p {dirname}  # 递归创建目录
pushd {dirname}     # 目录压栈并进入新目录
popd                # 弹出并进入栈顶的目录
dirs -v             # 列出当前目录栈
cd -                # 回到之前的目录
cd -{N}             # 切换到目录栈中的第 N个目录，比如 cd -2 将切换到第二个文件操作
ls                  # 显示当前目录内容，后面可接目录名：ls {dir} 显示指定目录
ls -l               # 列表方式显示目录内容，包括文件日期，大小，权限等信息
ls -1               # 列表方式显示目录内容，只显示文件名称，减号后面是数字 1
ls -a               # 显示所有文件和目录，包括隐藏文件（.开头的文件/目录名）
ln -s {fn} {link}   # 给指定文件创建一个软链接
cp {src} {dest}     # 拷贝文件，cp -r dir1 dir2 可以递归拷贝（目录）
rm {fn}             # 删除文件，rm -r 递归删除目录，rm -f 强制删除
mv {src} {dest}     # 移动文件，如果 dest 是目录，则移动，是文件名则覆盖
touch {fn}          # 创建或者更新一下制定文件
cat {fn}            # 输出文件原始内容
any_cmd > {fn}      # 执行任意命令并将标准输出重定向到指定文件
more {fn}           # 逐屏显示某文件内容，空格翻页，q 退出
less {fn}           # 更高级点的 more，更多操作，q 退出
head {fn}           # 显示文件头部数行，可用 head -3 abc.txt 显示头三行
tail {fn}           # 显示文件尾部数行，可用 tail -3 abc.txt 显示尾部三行
tail -f {fn}        # 持续显示文件尾部数据，可用于监控日志
nano {fn}           # 使用 nano 编辑器编辑文件
vim {fn}            # 使用 vim 编辑文件
diff {f1} {f2}      # 比较两个文件的内容
wc {fn}             # 统计文件有多少行，多少个单词
chmod 644 {fn}      # 修改文件权限为 644，可以接 -R 对目录循环改权限
chgrp group {fn}    # 修改文件所属的用户组
chown user1 {fn}    # 修改文件所有人为 user1, chown user1:group1 fn 可以修改组
file {fn}           # 检测文件的类型和编码
basename {fn}       # 查看文件的名字（不包括路径）
dirname {fn}        # 查看文件的路径（不包括名字）
grep {pat} {fn}     # 在文件中查找出现过 pat 的内容
grep -r {pat} .     # 在当前目录下递归查找所有出现过 pat 的文件内容
stat {fn}           # 显示文件的详细信息
```
### 用户管理
```
whoami              # 显示我的用户名
who                 # 显示已登陆用户信息，w / who / users 内容略有不同
w                   # 显示已登陆用户信息，w / who / users 内容略有不同
users               # 显示已登陆用户信息，w / who / users 内容略有不同
passwd              # 修改密码，passwd {user} 可以用于 root 修改别人密码
finger {user}       # 显示某用户信息，包括 id, 名字, 登陆状态等
adduser {user}      # 添加用户
deluser {user}      # 删除用户
w                   # 查看谁在线
su                  # 切换到 root 用户
su -                # 切换到 root 用户并登陆（执行登陆脚本）
su {user}           # 切换到某用户
su -{user}          # 切换到某用户并登陆（执行登陆脚本）
id {user}           # 查看用户的 uid，gid 以及所属其他用户组
id -u {user}        # 打印用户 uid
id -g {user}        # 打印用户 gid
write {user}        # 向某用户发送一句消息
last                # 显示最近用户登陆列表
last {user}         # 显示登陆记录
lastb               # 显示失败登陆记录
lastlog             # 显示所有用户的最近登陆记录
sudo {command}      # 以 root 权限执行某命令
```
### 进程管理
```
ps                        # 查看当前会话进程
ps ax                     # 查看所有进程，类似 ps -e
ps aux                    # 查看所有进程详细信息，类似 ps -ef
ps auxww                  # 查看所有进程，并且显示进程的完整启动命令
ps -u {user}              # 查看某用户进程
ps axjf                   # 列出进程树
ps xjf -u {user}          # 列出某用户的进程树
ps -eo pid,user,command   # 按用户指定的格式查看进程
ps aux | grep httpd       # 查看名为 httpd 的所有进程
ps --ppid {pid}           # 查看父进程为 pid 的所有进程
pstree                    # 树形列出所有进程，pstree 默认一般不带，需安装
pstree {user}             # 进程树列出某用户的进程
pstree -u                 # 树形列出所有进程以及所属用户
pgrep {procname}          # 搜索名字匹配的进程的 pid，比如 pgrep apache2
kill {pid}                # 结束进程
kill -9 {pid}             # 强制结束进程，9/SIGKILL 是强制不可捕获结束信号
kill -KILL {pid}          # 强制执行进程，kill -9 的另外一种写法
kill -l                   # 查看所有信号
kill -l TERM              # 查看 TERM 信号的编号
killall {procname}        # 按名称结束所有进程
pkill {procname}          # 按名称结束进程，除名称外还可以有其他参数
top                       # 查看最活跃的进程
top -u {user}             # 查看某用户最活跃的进程
any_command &             # 在后台运行某命令，也可用 CTRL+Z 将当前进程挂到后台
jobs                      # 查看所有后台进程（jobs）
bg                        # 查看后台进程，并切换过去
fg                        # 切换后台进程到前台
fg {job}                  # 切换特定后台进程到前台
trap cmd sig1 sig2        # 在脚本中设置信号处理命令
trap "" sig1 sig2         # 在脚本中屏蔽某信号
trap - sig1 sig2          # 恢复默认信号处理行为
nohup {command}           # 长期运行某程序，在你退出登陆都保持它运行
nohup {command} &         # 在后台长期运行某程序
disown {PID|JID}          # 将进程从后台任务列表（jobs）移除
wait                      # 等待所有后台进程任务结束
```
### 系统信息
```
uname -a                  # 查看内核版本等信息
man {help}                # 查看帮助
man -k {keyword}          # 查看哪些帮助文档里包含了该关键字
info {help}               # 查看 info pages，比 man 更强的帮助系统
uptime                    # 查看系统启动时间
date                      # 显示日期
cal                       # 显示日历
vmstat                    # 显示内存和 CPU 使用情况
vmstat 10                 # 每 10 秒打印一行内存和 CPU情况，CTRL+C 退出
free                      # 显示内存和交换区使用情况
df                        # 显示磁盘使用情况
du                        # 显示当前目录占用，du . --max-depth=2 可以指定深度
uname                     # 显示系统版本号
hostname                  # 显示主机名称
showkey -a                # 查看终端发送的按键编码
```
### 重定向
```
cmd1 | cmd2                        # 管道，cmd1 的标准输出接到 cmd2 的标准输入
< file                             # 将文件内容重定向为命令的标准输入
> file                             # 将命令的标准输出重定向到文件，会覆盖文件
>> file                            # 将命令的标准输出重定向到文件，追加不覆盖
>| file                            # 强制输出到文件，即便设置过：set -o noclobber
n>| file                           # 强制将文件描述符 n的输出重定向到文件
<> file                            # 同时使用该文件作为标准输入和标准输出
n<> file                           # 同时使用文件作为文件描述符 n 的输出和输入
n> file                            # 重定向文件描述符 n 的输出到文件
n< file                            # 重定向文件描述符 n 的输入为文件内容
n>&                                # 将标准输出 dup/合并 到文件描述符 n
n<&                                # 将标准输入 dump/合并 定向为描述符 n
n>&m                               # 文件描述符 n 被作为描述符 m 的副本，输出用
n<&m                               # 文件描述符 n 被作为描述符 m 的副本，输入用
&>file                             # 将标准输出和标准错误重定向到文件
<&-                                # 关闭标准输入
>&-                                # 关闭标准输出
n>&-                               # 关闭作为输出的文件描述符 n
n<&-                               # 关闭作为输入的文件描述符 n
diff <(cmd1) <(cmd2)               # 比较两个命令的输出
```
### 文本处理
```
cut -c 1-16                        # 截取每行头16个字符
cut -c 1-16 file                   # 截取指定文件中每行头 16个字符
cut -c3-                           # 截取每行从第三个字符开始到行末的内容
cut -d':' -f5                      # 截取用冒号分隔的第五列内容
cut -d';' -f2,10                   # 截取用分号分隔的第二和第十列内容
cut -d' ' -f3-7                    # 截取空格分隔的三到七列
echo "hello" | cut -c1-3           # 显示 hel
echo "hello sir" | cut -d' ' -f2   # 显示 sir
ps | tr -s " " | cut -d " " -f 2,3,4  # cut 搭配 tr 压缩字符
awk '{print $5}' file              # 打印文件中以空格分隔的第五列
awk -F ',' '{print $5}' file       # 打印文件中以逗号分隔的第五列
awk '/str/ {print $2}' file        # 打印文件中包含 str 的所有行的第二列
awk -F ',' '{print $NF}' file      # 打印逗号分隔的文件中的每行最后一列 
awk '{s+=$1} END {print s}' file   # 计算所有第一列的合
awk 'NR%3==1' file                 # 从第一行开始，每隔三行打印一行
sed 's/find/replace/' file         # 替换文件中首次出现的字符串并输出结果 
sed '10s/find/replace/' file       # 替换文件第 10 行内容
sed '10,20s/find/replace/' file    # 替换文件中 10-20 行内容
sed -r 's/regex/replace/g' file    # 替换文件中所有出现的字符串
sed -i 's/find/replace/g' file     # 替换文件中所有出现的字符并且覆盖文件
sed -i '/find/i\newline' file      # 在文件的匹配文本前插入行
sed -i '/find/a\newline' file      # 在文件的匹配文本后插入行
sed '/line/s/find/replace/' file   # 先搜索行特征再执行替换
sed -e 's/f/r/' -e 's/f/r' file    # 执行多次替换
sed 's#find#replace#' file         # 使用 # 替换 / 来避免 pattern 中有斜杆
sed -i -r 's/^\s+//g' file         # 删除文件每行头部空格
sed '/^$/d' file                   # 删除文件空行并打印
sed -i 's/\s\+$//' file            # 删除文件每行末尾多余空格
sed -n '2p' file                   # 打印文件第二行
sed -n '2,5p' file                 # 打印文件第二到第五行
```
### 排序
```
sort file                          # 排序文件
sort -r file                       # 反向排序（降序）
sort -n file                       # 使用数字而不是字符串进行比较
sort -t: -k 3n /etc/passwd         # 按 passwd 文件的第三列进行排序
sort -u file                       # 去重排序
```
### 网络管理
```
ping {host}               # ping 远程主机并显示结果，CTRL+C 退出
ping -c N {host}          # ping 远程主机 N 次
traceroute {host}         # 侦测路由连通情况
mtr {host}                # 高级版本 traceroute
host {domain}             # DNS 查询，{domain} 前面可加 -a 查看详细信息
whois {domain}            # 取得域名 whois 信息
dig {domain}              # 取得域名 dns 信息
route -n                  # 查看路由表
netstat -a                # 列出所有端口
netstat -an               # 查看所有连接信息，不解析域名
netstat -anp              # 查看所有连接信息，包含进程信息（需要 sudo）
netstat -l                # 查看所有监听的端口
netstat -t                # 查看所有 TCP 链接
netstat -lntu             # 显示所有正在监听的 TCP 和 UDP 信息
netstat -lntup            # 显示所有正在监听的 socket 及进程信息
netstat -i                # 显示网卡信息
netstat -rn               # 显示当前系统路由表，同 route -n
ip a                               # 显示所有网络地址，同 ip address
ip a show eth1                     # 显示网卡 IP 地址
ip a add 172.16.1.23/24 dev eth1   # 添加网卡 IP 地址
ip a del 172.16.1.23/24 dev eth1   # 删除网卡 IP 地址
ip link show dev eth0              # 显示网卡设备属性
ip link set eth1 up                # 激活网卡
ip link set eth1 down              # 关闭网卡
ip link set eth1 address {mac}     # 修改 MAC 地址
ip neighbour                       # 查看 ARP 缓存
ip route                           # 查看路由表
ip route add 10.1.0.0/24 via 10.0.0.253 dev eth0    # 添加静态路由
ip route del 10.1.0.0/24           # 删除静态路由
ifconfig                           # 显示所有网卡和接口信息
ifconfig -a                        # 显示所有网卡（包括开机没启动的）信息
ifconfig eth0                      # 指定设备显示信息
ifconfig eth0 up                   # 激活网卡
ifconfig eth0 down                 # 关闭网卡
ifconfig eth0 192.168.120.56       # 给网卡配置 IP 地址
ifconfig eth0 10.0.0.8 netmask 255.255.255.0 up     # 配置 IP 并启动
ifconfig eth0 hw ether 00:aa:bb:cc:dd:ee            # 修改 MAC 地址
nmap 10.0.0.12                     # 扫描主机 1-1000 端口
nmap -p 1024-65535 10.0.0.12       # 扫描给定端口
nmap 10.0.0.0/24                   # 给定网段扫描局域网内所有主机
nmap -O -sV 10.0.0.12              # 探测主机服务和操作系统版本
```
### 其他常用命令
```
man hier                           # 查看文件系统的结构和含义
man test                           # 查看 posix sh 的条件判断帮助
man ascii                          # 显示 ascii 表
getconf LONG_BIT                   # 查看系统是 32 位还是 64 位
bind -P                            # 列出所有 bash 的快捷键
mount | column -t                  # 漂亮的列出当前加载的文件系统
curl ip.cn                         # 取得外网 ip 地址和服务商信息
disown -a && exit                  # 关闭所有后台任务并退出
cat /etc/issue                     # 查看 Linux 发行版信息
lsof -i port:80                    # 哪个程序在使用 80 端口？
showkey -a                         # 取得按键的 ASCII 码
svn diff | view -                  # 使用 Vim 来显示带色彩的 diff 输出
mv filename.{old,new}              # 快速文件改名
time read                          # 使用 CTRL-D 停止，最简单的计时功能
cp file.txt{,.bak}                 # 快速备份文件
sudo touch /forcefsck              # 强制在下次重启时扫描磁盘
find ~ -mmin 60 -type f            # 查找 $HOME 目录中，60 分钟内修改过的文件
curl wttr.in/~beijing              # 查看北京的天气预报
echo ${SSH_CLIENT%% *}             # 取得你是从什么 IP 链接到当前主机上的
echo $[RANDOM%X+1]                 # 取得 1 到 X 之间的随机数
bind -x '"\C-l":ls -l'             # 设置 CTRL+l 为执行 ls -l 命令
find / -type f -size +5M           # 查找大于 5M 的文件
chmod --reference f1 f2            # 将 f2 的权限设置成 f1 一模一样的
curl -L cheat.sh                   # 速查表大全
```

## Vim
### 光标移动
```
h                   光标左移，同 <Left> 键
j                   光标下移，同 <Down> 键
k                   光标上移，同 <Up> 键
l                   光标右移，同 <Right> 键
CTRL-F              下一页
CTRL-B              上一页
CTRL-U              上移半屏
CTRL-D              下移半屏
0                   跳到行首（是数字零，不是字母O），效用等同于 <Home> 键
^                   跳到从行首开始第一个非空白字符
$                   跳到行尾，效用等同于 <End> 键
gg                  跳到第一行，效用等同于 CTRL+<Home>
G                   跳到最后一行，效用等同于 CTRL+<End>
nG                  跳到第n行，比如 10G 是移动到第十行
:n                  跳到第n行，比如 :10<回车> 是移动到第十行
10%                 移动到文件 10% 处
15|                 移动到当前行的 15列
w                   跳到下一个单词开头 (word: 标点或空格分隔的单词)
W                   跳到下一个单词开头 (WORD: 空格分隔的单词)
e                   跳到下一个单词尾部 (word: 标点或空格分隔的单词)
E                   跳到下一个单词尾部 (WORD: 空格分隔的单词)
b                   上一个单词头 (word: 标点或空格分隔的单词)
B                   上一个单词头 (WORD: 空格分隔的单词)
ge                  上一个单词尾
)                   向前移动一个句子（句号分隔）
(                   向后移动一个句子（句号分隔）
}                   向前移动一个段落（空行分隔）
{                   向后移动一个段落（空行分隔）
<enter>             移动到下一行首个非空字符
+                   移动到下一行首个非空字符（同回车键）
-                   移动到上一行首个非空字符
H                   移动到屏幕上部
M                   移动到屏幕中部
L                   移动到屏幕下部
fx                  跳转到下一个为 x 的字符，2f/ 可以找到第二个斜杆
Fx                  跳转到上一个为 x 的字符
tx                  跳转到下一个为 x 的字符前
Tx                  跳转到上一个为 x 的字符前
;                   跳到下一个 f/t 搜索的结果
,                   跳到上一个 f/t 搜索的结果
<S-Left>            按住 SHIFT 按左键，向左移动一个单词
<S-Right>           按住 SHIFT 按右键，向右移动一个单词
<S-Up>              按住 SHIFT 按上键，向上翻页
<S-Down>            按住 SHIFT 按下键，向下翻页
gm                  移动到行中
gj                  光标下移一行（忽略自动换行）
gk                  光标上移一行（忽略自动换行）
```
### 插入模式
```
i                   在光标处进入插入模式
I                   在行首进入插入模式
a                   在光标后进入插入模式
A                   在行尾进入插入模式
o                   在下一行插入新行并进入插入模式
O                   在上一行插入新行并进入插入模式
gi                  进入到上一次插入模式的位置
<ESC>               退出插入模式
CTRL-[              退出插入模式（同 ESC 等价，但更顺手）
INSERT MODE - 由 i, I, a, A, o, O 等命令进入插入模式后
<Up>                光标向上移动
<Down>              光标向下移动
<Left>              光标向左移动
<Right>             光标向右移动
<S-Left>            按住 SHIFT 按左键，向左移动一个单词
<S-Right>           按住 SHIFT 按右键，向右移动一个单词
<S-Up>              按住 SHIFT 按上键，向上翻页
<S-Down>            按住 SHIFT 按下键，向下翻页
<PageUp>            上翻页
<PageDown>          下翻页
<Delete>            删除光标处字符
<BS>                Backspace 向后删除字符
<Home>              光标跳转行首
<End>               光标跳转行尾
CTRL-W              向后删除单词
```
### 文件操作
```
:w                  保存文件
:w <filename>       按名称保存文件
:e <filename>       打开文件并编辑
:saveas <filename>  另存为文件
:r <filename>       读取文件并将内容插入到光标后
:r !dir             将 dir 命令的输出捕获并插入到光标后
:close              关闭文件
:q                  退出
:q!                 强制退出
:wa                 保存所有文件
:cd <path>          切换 Vim 当前路径
:pwd                显示 Vim 当前路径
:new                打开一个新的窗口编辑新文件
:enew               在当前窗口创建新文件
:vnew               在左右切分的新窗口中编辑新文件
:tabnew             在新的标签页中编辑新文件
```
### 帮助信息
```
:h tutor            入门文档
:h quickref         快速帮助
:h index            查询 Vim 所有键盘命令定义
:h summary          帮助你更好的使用内置帮助系统
:h CTRL-H           查询普通模式下 CTRL-H 是干什么的
:h i_CTRL-H         查询插入模式下 CTRL-H 是干什么的
:h i_<Up>           查询插入模式下方向键上是干什么的
:h pattern.txt      正则表达式帮助
:h eval             脚本编写帮助
:h windows.txt      窗口使用帮助
:h tabpage.txt      标签页使用帮助
:h :!               查看如何运行外部命令
:h tips             查看 Vim 内置的常用技巧文档
:viusage            NORMAL 模式帮助
:version            显示当前 Vim 的版本号和特性
```

## References
For more information please refer to [Bash Cheatsheet](https://github.com/skywind3000/awesome-cheatsheets/blob/master/languages/bash.sh "Bash速查表") and [Vim cheatsheet](https://github.com/skywind3000/awesome-cheatsheets/blob/master/editors/vim.txt "Vim速查表")