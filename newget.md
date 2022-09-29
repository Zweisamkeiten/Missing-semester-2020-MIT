---
date created: 2022-04-08 10:21
date updated: 2022-09-29 16:10
---

一. 课程概览和shell

1. `--` 双破折号的作用 [[01.course_overview+the_shell#^131fd6]]
2. 重定向修改文本的权限 [[01.course_overview+the_shell#^e629b1]]
3. 脚本的 `shebang` [[01.course_overview+the_shell#^c5de5f]] [[02.Shell_Tools_and_Scripting#^7bf617]]
4. find 搜索软链接入口中的文件 [[01.course_overview+the_shell#^3b2ff3]]
5. grep 忽略大小写 [[01.course_overview+the_shell#^bf97e7]]
6. tail 简单用法 [[01.course_overview+the_shell#^e02519]]
7. cut 分割管道传来的输入， 并选择 field [[01.course_overview+the_shell#^b38b9f]]

---

二. Shell 工具和脚本

1. 单引号 双引号在 shell 中的区别 [[02.Shell_Tools_and_Scripting#^2d7dca]]
2. shell 中的特殊变量 $ 0  $#等 [[02.Shell_Tools_and_Scripting#^7f0d5f]]
   1. 上一条命令最后一个参数的快速引用， 很有用 [[02.Shell_Tools_and_Scripting#^f0aac3]]
3. shell 中 && || 为短路操作符 [[02.Shell_Tools_and_Scripting#^a9565e]]
4. $(CMD) <(CMD) 后者会创建为临时文件而不是输入流重定向[[02.Shell_Tools_and_Scripting#^c5e80b]]
5. shell 扩展表达式 {a..z} `*` 等 [[02.Shell_Tools_and_Scripting#^3c8521]]
6. shell 函数 与 脚本 的区别 **很重要** [[02.Shell_Tools_and_Scripting#^abcf04]] [[11.Q&A#^71b1df]]
7. find 命令 基础使用 [[02.Shell_Tools_and_Scripting#^9910d3]]
8. grep 命令 基础使用 [[02.Shell_Tools_and_Scripting#^977e4e]]
9. shell history fc -A 等命令的使用 [[02.Shell_Tools_and_Scripting#^73fa2c]]
10. shell 基础算术运算 [Bash Arithmetic 算术运算](Bash%20Arithmetic%20算术运算)
11. shell for while until 三种循环写法 [[02.Shell_Tools_and_Scripting#^c59cfa]]
12. shell 中 比较判断 man test 
13. 在 bash 中使用 `[[ .. )` 代替 `[` 解释是 前者为 bash 内置比较器， 后者实际上是 `test` 执行程序的另一名字，后者实际上在执行 `[` 程序 , `[` 与 `test` 的唯一区别是它需要用 `]` 来结尾. [[02.Shell_Tools_and_Scripting#^06341f]][[02.Shell_Tools_and_Scripting#^ac8740]] [[2019-other#^61c85f]]

---

三. 编辑器 VIM

1. Vim 设计哲学 [[03.Editors (Vim)#^5641c5]]
2. Vim 列出 buffers [[03.Editors (Vim)#^6624b2]]
3. Vim movement about Screen 屏幕顶部中部底部移动 [[03.Editors (Vim)#^b87bc1]]
4. Vim Find `f` `t` `F` `T` 等关于 `,`/ `;` 匹配项导航到 [[03.Editors (Vim)#^105588]]
5. Vim 翻转当前字符的大小写 [[03.Editors (Vim)#^9710be]]
6. Vim 内置包管理器 (Vim 8.0) [[03.Editors (Vim)#^47a2e3]] [[00_missing-semester/ref/vim-plugins]]
7. [Vimrc 结构化](https://github.com/romainl/idiomatic-vimrc)
8. vim 需要知道帮助文件何时更新，因此它可以知道 `NERDtree`标签应该指向。 在 vim 中运行以下命令应该可以修复它：
   ```
   :helptags ~/.vim/doc
   ```
9. vim `set termguicolors` 设置启用真色彩

---

四. 数据整理

1. ssh 远端执行命令输出 传输到本地 [[04.Data-Wrangling#^c4a81a]]
2. sed 简单正则 [[04.Data-Wrangling#^325387]]
3. perl 简单正则 [[04.Data-Wrangling#^79c4e3]] [[04.Data-Wrangling#^4b309a]]
4. `uniq -c` 合并连续且想通的行， 前缀为出现次数 [[04.Data-Wrangling#^9707b3]]
5. `sort -nk1,1` 使用 [[04.Data-Wrangling#^01ae7a]]
6. `paste -sd,` 把输出以特定分隔符拼接 [[04.Data-Wrangling#^e78405]]
7. `awk` 基础用法， 够用 [[04.Data-Wrangling#^7864a6]]
8. `R` 语言 summary() 统计数据 [[04.Data-Wrangling#^07e324]]
9. `ffmpeg` pipe 管道与标准输入 `-`(dash) 相关用法 [[04.Data-Wrangling#^873101]]
10. 输出大小写转换的三种方法 `awk tolower()`, `sed 'y/source/dest'` ,`tr "[:upper:] "[:lower:]"` [[04.Data-Wrangling#^ef3b58]]
11. sed 原地替换的弊端 即 把输出文件替换后重新写入原文件 原因： 输出文件会先行被清空  [[04.Data-Wrangling#^dbaffb]]

---

五. 命令行环境

1. SIGNAL(信号) 与进程 [[05.Command-line Environment#^da1166]]
2. shell `$!` 特殊参数，最近后台运行进程的 pid [[05.Command-line Environment#^f48526]]
3. `jobs`, `fg`, `bg`, `Ctrl-Z`, `&`, `nohup` 等使用 [[05.Command-line Environment#^f060f4]]
4. `&` 后缀可以让命令直接在后台运行, 使得可以直接在 shell 中继续其他操作，不过它此时还是会使用 shell 的标准输出 [[05.Command-line Environment#^0f535a]]
5. `^Z` + `bg` == `&`, 使当前进程后台允许
6. `disown` 切断 后台job 与 会话的关联; `nohup` 是进程忽略关闭shell自动发送的 SIGHUP 信号.
7. tmux 我认为常用的快捷键操作 [[05.Command-line Environment#^cddd3c]]
8. zsh 环境变量读取加载过程 [[05.Command-line Environment#^8a52a5]]
9. 管理 dotfile 相关资源 [[05.Command-line Environment#^0c7add]]
10. 配置文件的可移植性 编写 条件判断脚本 [[05.Command-line Environment#^06d9e6]]
11. ssh 远程执行命令 [[05.Command-line Environment#^afa27f]]
12. 为 ssh 密钥设置密码 ssh-agent 以后再了解 [[05.Command-line Environment#^fbafb6]]
13. ssh-copy-id 简单的复制密钥到服务器的方法 [[05.Command-line Environment#^fc5594]]
14. rsync 是 对 scp 进行了改进 [[05.Command-line Environment#^04abf0]]
15. ssh portforwarding 动态转发 本地转发 远程转发 区分实践 [[05.Command-line Environment#^4b532d]] [[ssh-portforwarding]]
16. ssh x11forwarding 图形转发 [[05.Command-line Environment#^3d7dd6]]
17. ssh mosh roaming [[05.Command-line Environment#^7370b4]]
18. ssh-agent 我的配置实践 [[ssh-agent#^3e75f9]]
19. 在后台进行端口转发 [[05.Command-line Environment#^222544]]

---

六. 版本控制 GIT

1. Git 快照表示的完整备份的解释 [[06.Version Control (Git)#^927cc5]]
2. Git 的数据模型 快照: 文件-Blob 数据对象 目录-tree树🌲 [[06.Version Control (Git)#^f3416c]]
3. Git 快照使用 `sha-1` 进行标记 [[06.Version Control (Git)#^65aaa5]]
4. Git 引用是指向 `sha-1` 提交的指针，可以被更新指向新的提交 [[06.Version Control (Git)#^8a5362]]
5. git blame && git show 查看某文件的某一行最后一次提交的提交信息是什么 [[06.Version Control (Git)#^fbbffc]]
6. git stash && git stash pop 应用 [[06.Version Control (Git)#^37f793]]

---

大杂烩

1. 守护进程 systemd 文件编写 [[10.Potpourri#^4f7d3b]]
2. FUSE 用户空间文件系统 例如 sshfs [[10.Potpourri#^41af63]]
3. 特殊参数 `--` 让某个程序 _停止处理_ `--` 后面出现的标志参数以及选项（以 `-` 开头的内容） [[10.Potpourri#^e23520]]
4. 使用 `-` 代替输入或者输出文件名意味着工具将从标准输入（standard input）获取所需内容，或者向标准输出（standard output）输出结果。 [[10.Potpourri#^8d6976]]
5. [Vagrant](https://www.vagrantup.com/) 是一个构建和配置虚拟开发环境的工具。它支持用户在配置文件中写入比如操作系统、系统服务、需要安装的软件包等描述，然后使用 `vagrant up` 命令在各种环境（VirtualBox，KVM，Hyper-V等）中启动一个虚拟机。[[10.Potpourri#^fedd3e]]

---

Q&A

1. `source script.sh` 和 `./script.sh` 有什么区别? [[11.Q&A#^71b1df]] [[02.Shell_Tools_and_Scripting#^abcf04]]
2. FHS [[11.Q&A#^8865b8]]
3. 代码性能分析工具 [[11.Q&A#^15f1e6]]
4. Docker 与 虚拟机的区别 [[11.Q&A#^89fef5]] [[difference-between-KVM-Docker]]
5. 2FA 双因子认证 [[11.Q&A#^5a1229]]

---

2019

1. libvirt [[libvirt]]
2. virt-manager (libvirt 的前端gui) 使用实践 [[virt-manger qemu libvirt]]
3. kvm 和 docker 的区别 [[difference-between-KVM-Docker]] [[11.Q&A#^89fef5]]
4. kvm 与 仿真虚拟的区别 kvm 是将客户机的程序指令在真实主机的 cpu 上执行, 因此虚拟机的cpu指令架构类型需要与主机相同 否则只能通过仿真 cpu 硬件 [[virt-manger qemu libvirt#^d90d82]]
5. shell for 循环按次数 相关命令 seq 1 5 [[2019-other#^9a3e9e]]
6. `ps` 与 `kill` 信号 [[2019-other#^dc91f7]]
7. `stty` 检查或更改产生信号的字符 [[2019-other#^fd9ba1]]
8. git add `patch mode` 和 `a..b` 提交区间 [[2019-other#^0bc161]]
9. git 中 名称相关的特殊用法 `NAME~3` , `NAME^3` [[2019-other#^ebd0d0]]
10. git 合并一些提交 `amend` 和 `rebase` 变基操作 [[2019-other#^925e18]]
11. git 推送修改到远端的指定分支 [[2019-other#^4be489]]
12. git push -u 将指定的本地分支的修改发送到远端，并且设置远端链接为该本地分支的默认推送拉取 [[2019-other#^1e4805]]
13. git 合并分支解决冲突 [[2019-other#^9d4d87]]
14. git 远程拒绝 冲突解决 [[2019-other#^2ba562]]
15. backup [[backup]]
16. cron && anacron [[automation]]
17. journalctl 一些使用 [[2019-other#^5f85fe]]
18. journalctl dmesg tail 的 follow 跟踪输出模式 [[2019-other#^01ed2d]]
19. 显示打开的链接 ss -tlpn [[2019-other#^224e70]]
20. google 搜索运算符 [[2019-other#^aa59be]]
