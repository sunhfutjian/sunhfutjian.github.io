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
### 常用快捷键
```bash
CTRL+A              移动到行首，同 <Home>
CTRL+B              向后移动，同 <Left>
CTRL+C              结束当前命令
CTRL+D              删除光标前的字符，同 <Delete> ，或者没有内容时，退出会话
CTRL+E              移动到行末，同 <End>
CTRL+F              向前移动，同 <Right>
CTRL+G              退出当前编辑（比如正在 CTRL+R 搜索历史时）
CTRL+H              删除光标左边的字符，同 <Backspace>
CTRL+K              删除光标位置到行末的内容
CTRL+L              清屏并重新显示
CTRL+N              移动到命令历史的下一行，同 <Down>
CTRL+O              类似回车，但是会显示一行历史
CTRL+P              移动到命令历史的上一行，同 <Up>
CTRL+R              历史命令反向搜索，使用 CTRL+G 退出搜索
CTRL+S              历史命令正向搜索，使用 CTRL+G 退出搜索
CTRL+T              交换前后两个字符
CTRL+U              删除字符到行首
CTRL+V              输入字符字面量，先按 CTRL+V 再按任意键
CTRL+W              删除光标左边的一个单词
CTRL+X              列出可能的补全
CTRL+Y              粘贴前面 CTRL+u/k/w 删除过的内容
CTRL+Z              暂停前台进程返回 bash，需要时可用 fg 将其切换回前台
CTRL+_              撤销（undo），有的终端将 CTRL+_ 映射为 CTRL+/ 或 CTRL+7
ALT+b               向后（左边）移动一个单词
ALT+d               删除光标后（右边）一个单词
ALT+f               向前（右边）移动一个单词
ALT+t               交换前后两个单词
ALT+BACKSPACE       删除光标前面一个单词，类似 CTRL+W，但不影响剪贴板
CTRL+X CTRL+X       连续按两次 CTRL+X，光标在当前位置和上一位置来回跳转 
CTRL+X CTRL+E       用你指定的编辑器，编辑当前命令
```
### 目录操作
```bash
cd                  返回自己 $HOME 目录
cd {dirname}        进入目录
pwd                 显示当前所在目录
mkdir {dirname}     创建目录
mkdir -p {dirname}  递归创建目录
pushd {dirname}     目录压栈并进入新目录
popd                弹出并进入栈顶的目录
dirs -v             列出当前目录栈
cd -                回到之前的目录
cd -{N}             切换到目录栈中的第 N 个目录，比如 cd -2 将切换到第二个文件操作
ls                  显示当前目录内容，后面可接目录名：ls {dir} 显示指定目录
ls -l               列表方式显示目录内容，包括文件日期，大小，权限等信息
ls -1               列表方式显示目录内容，只显示文件名称，减号后面是数字 1
ls -a               显示所有文件和目录，包括隐藏文件（.开头的文件/目录名）
ln -s {fn} {link}   给指定文件创建一个软链接
cp {src} {dest}     拷贝文件，cp -r dir1 dir2 可以递归拷贝（目录）
rm {fn}             删除文件，rm -r 递归删除目录，rm -f 强制删除
mv {src} {dest}     移动文件，如果 dest 是目录，则移动，是文件名则覆盖
touch {fn}          创建或者更新一下制定文件
cat {fn}            输出文件原始内容
any_cmd > {fn}      执行任意命令并将标准输出重定向到指定文件
more {fn}           逐屏显示某文件内容，空格翻页，q 退出
less {fn}           更高级点的 more，更多操作，q 退出
head {fn}           显示文件头部数行，可用 head -3 abc.txt 显示头三行
tail {fn}           显示文件尾部数行，可用 tail -3 abc.txt 显示尾部三行
tail -f {fn}        持续显示文件尾部数据，可用于监控日志
nano {fn}           使用 nano 编辑器编辑文件
vim {fn}            使用 vim 编辑文件
diff {f1} {f2}      比较两个文件的内容
wc {fn}             统计文件有多少行，多少个单词
chmod 644 {fn}      修改文件权限为 644，可以接 -R 对目录循环改权限
chgrp group {fn}    修改文件所属的用户组
chown user1 {fn}    修改文件所有人为 user1, chown user1:group1 fn 可以修改组
file {fn}           检测文件的类型和编码
basename {fn}       查看文件的名字（不包括路径）
dirname {fn}        查看文件的路径（不包括名字）
grep {pat} {fn}     在文件中查找出现过 pat 的内容
grep -r {pat} .     在当前目录下递归查找所有出现过 pat 的文件内容
stat {fn}           显示文件的详细信息
```
### 用户管理
```bash
whoami              显示我的用户名
w                   显示已登陆用户信息，w / who / users 内容略有不同
who                 显示已登陆用户信息，w / who / users 内容略有不同
users               显示已登陆用户信息，w / who / users 内容略有不同
passwd              修改密码，passwd {user} 可以用于 root 修改别人密码
finger {user}       显示某用户信息，包括 id, 名字, 登陆状态等
adduser {user}      添加用户
deluser {user}      删除用户
su                  切换到 root 用户
su -                切换到 root 用户并登陆（执行登陆脚本）
su {user}           切换到某用户
su -{user}          切换到某用户并登陆（执行登陆脚本）
id {user}           查看用户的 uid，gid 以及所属其他用户组
id -u {user}        打印用户 uid
id -g {user}        打印用户 gid
write {user}        向某用户发送一句消息
last                显示最近用户登陆列表
last {user}         显示登陆记录
lastb               显示失败登陆记录
lastlog             显示所有用户的最近登陆记录
sudo {command}      以 root 权限执行某命令
```
### 系统信息
```bash
uname -a            查看内核版本等信息
man {help}          查看帮助
man -k {keyword}    查看哪些帮助文档里包含了该关键字
man ascii           显示 ascii 表
info {help}         查看 info pages，比 man 更强的帮助系统
uptime              查看系统启动时间
date                显示日期
cal                 显示日历
vmstat              显示内存和 CPU 使用情况
free                显示内存和交换区使用情况
df                  显示磁盘使用情况
du                  显示当前目录占用，du . --max-depth=2 可以指定深度
uname               显示系统版本号
hostname            显示主机名称
exit                退出当前登陆
env                 显示环境变量
```
### 重定向
```bash
cmd1 | cmd2         管道，cmd1 的标准输出接到 cmd2 的标准输入
< file              将文件内容重定向为命令的标准输入
> file              将命令的标准输出重定向到文件，会覆盖文件
>> file             将命令的标准输出重定向到文件，追加不覆盖
>| file             强制输出到文件，即便设置过：set -o noclobber
n>| file            强制将文件描述符 n的输出重定向到文件
<> file             同时使用该文件作为标准输入和标准输出
n<> file            同时使用文件作为文件描述符 n 的输出和输入
n> file             重定向文件描述符 n 的输出到文件
n< file             重定向文件描述符 n 的输入为文件内容
n>&                 将标准输出 dup/合并 到文件描述符 n
n<&                 将标准输入 dump/合并 定向为描述符 n
n>&m                文件描述符 n 被作为描述符 m 的副本，输出用
n<&m                文件描述符 n 被作为描述符 m 的副本，输入用
&> file             将标准输出和标准错误重定向到文件
<&-                 关闭标准输入
>&-                 关闭标准输出
n>&-                关闭作为输出的文件描述符 n
n<&-                关闭作为输入的文件描述符 n
```
### 文本处理
```bash
cut -c 1-16                        截取每行头16个字符
cut -c 1-16 file                   截取指定文件中每行头 16个字符
cut -c3-                           截取每行从第三个字符开始到行末的内容
cut -d':' -f5                      截取用冒号分隔的第五列内容
cut -d';' -f2,10                   截取用分号分隔的第二和第十列内容
cut -d' ' -f3-7                    截取空格分隔的三到七列
awk '{print $5}' file              打印文件中以空格分隔的第五列
awk -F ',' '{print $5}' file       打印文件中以逗号分隔的第五列
awk '/str/ {print $2}' file        打印文件中包含 str 的所有行的第二列
awk -F ',' '{print $NF}' file      打印逗号分隔的文件中的每行最后一列 
awk '{s+=$1} END {print s}' file   计算所有第一列的和
awk 'NR%3==1' file                 从第一行开始，每隔三行打印一行
sed 's/find/replace/' file         替换文件中首次出现的字符串并输出结果 
sed '10s/find/replace/' file       替换文件第 10 行内容
sed '10,20s/find/replace/' file    替换文件中 10-20 行内容
sed -r 's/regex/replace/g' file    替换文件中所有出现的字符串
sed -i 's/find/replace/g' file     替换文件中所有出现的字符并且覆盖文件
sed -i '/find/i\newline' file      在文件的匹配文本前插入行
sed -i '/find/a\newline' file      在文件的匹配文本后插入行
sed 's#find#replace#' file         使用 替换 / 来避免 pattern 中有斜杆
sed -i -r 's/^\s+//g' file         删除文件每行头部空格
sed '/^$/d' file                   删除文件空行并打印
sed -i 's/\s\+$//' file            删除文件每行末尾多余空格
sed -n '2p' file                   打印文件第二行
sed -n '2,5p' file                 打印文件第二到第五行
```

## Vim
### 光标移动
```vim
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
```vim
i                   在光标处进入插入模式
I                   在行首进入插入模式
a                   在光标后进入插入模式
A                   在行尾进入插入模式
o                   在下一行插入新行并进入插入模式
O                   在上一行插入新行并进入插入模式
gi                  进入到上一次插入模式的位置
<ESC>               退出插入模式
CTRL-[              退出插入模式（同 ESC 等价，但更顺手）
<S-Left>            按住 SHIFT 按左键，向左移动一个单词
<S-Right>           按住 SHIFT 按右键，向右移动一个单词
<S-Up>              按住 SHIFT 按上键，向上翻页
<S-Down>            按住 SHIFT 按下键，向下翻页
```
### 文件操作
```vim
:w                  保存文件
:w <filename>       按名称保存文件
:e <filename>       打开文件并编辑
:saveas <filename>  另存为文件
:r <filename>       读取文件并将内容插入到光标后
:close              关闭文件
:q                  退出
:q!                 强制退出
:wa                 保存所有文件
:pwd                显示 Vim 当前路径
```
### 帮助信息
```vim
:h tutor            入门文档
:h quickref         快速帮助
:h index            查询 Vim 所有键盘命令定义
:h summary          帮助你更好的使用内置帮助系统
:h CTRL-H           查询普通模式下 CTRL-H 是干什么的
:h i_CTRL-H         查询插入模式下 CTRL-H 是干什么的
:h i_<Up>           查询插入模式下方向键上是干什么的
:h tips             查看 Vim 内置的常用技巧文档
:version            显示当前 Vim 的版本号和特性
```

## References
For more information, please refer to the [Bash Cheatsheet](https://github.com/skywind3000/awesome-cheatsheets/blob/master/languages/bash.sh "Bash速查表") and [Vim Cheatsheet](https://github.com/skywind3000/awesome-cheatsheets/blob/master/editors/vim.txt "Vim速查表").
