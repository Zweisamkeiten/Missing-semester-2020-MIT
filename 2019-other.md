---
date created: 2022-04-08 10:39
date updated: 2022-04-09 10:36
---

# 虚拟机和容器

## 虚拟机

虚拟机是模拟计算机。 您可以配置来宾虚拟 具有某些操作系统和配置的机器，无需使用 影响您的主机环境。

一般来说，虚拟机有很多用途。 它们通常用于运行软件 仅在特定操作系统上运行（例如在 Linux 上使用 Windows VM 运行特定于 Windows 的软件）。 它们通常用于试验 潜在的恶意软件。

## 有用的功能

- **隔离** ：虚拟机管理程序很好地将客人与 主机，因此您可以使用虚拟机来合理地运行错误或不受信任的软件 安全。

- **快照** ：您可以拍摄虚拟机的“快照”，捕获 整个机器状态（磁盘、内存等），对您的机器进行更改， 然后恢复到之前的状态。 这对于测试很有用 除其他外，潜在的破坏性行为。

## 缺点

虚拟机通常比在裸机上运行要慢，因此它们可能 不适合某些应用。

## 设置

- **资源** ：与主机共享； 物理资源分配时要注意这一点。

- **网络** ：许多选项，默认 NAT 应该适用于大多数用途 案例。

- **来宾插件** ：许多虚拟机管理程序可以在来宾中安装软件以 更好地与主机系统集成。 如果可以的话，你应该使用它。

## 资源

- 管理程序
  - [VirtualBox](https://www.virtualbox.org/) （开源）
  - [Virt-manager](https://virt-manager.org/) （开源，管理 KVM 虚拟机和 LXC 容器）
  - [VMWare](https://www.vmware.com/) （商业，可从 IS&T [获得 麻省理工学院学生](https://ist.mit.edu/vmware-fusion) ）

如果您已经熟悉流行的虚拟机管理程序/VM，您可能想了解更多关于如何从命令行友好的方式执行此操作的信息。 一种选择是 [libvirt](https://wiki.libvirt.org/page/UbuntuKVMWalkthrough) 工具包，它允许您管理多个不同的虚拟化提供程序/管理程序。

libvirt 的主要目标是提供单一方式来管理多个不同的虚拟化提供程序/管理程序，例如 [KVM/QEMU](https://wiki.archlinux.org/title/QEMU "QEMU") 、 [Xen](https://wiki.archlinux.org/title/Xen "辛") 、 [LXC](https://wiki.archlinux.org/title/LXC "LXC") 、 [OpenVZ](https://openvz.org) 或 [VirtualBox](https://wiki.archlinux.org/title/VirtualBox "虚拟盒子") [管理程序](https://wiki.archlinux.org/title/Category:Hypervisors "类别：管理程序") （ [等等](https://libvirt.org/drivers.html) ）[[libvirt#^6cdbc5)

## 容器

- Amazon Firecracker
- Docker
- rkt
- lxc

容器 _大多_ 只是各种 Linux 安全性的组合 功能，如虚拟文件系统、虚拟网络接口、chroot、 虚拟内存技巧等，它们共同呈现 的虚拟化。

不像虚拟机那样安全或隔离，但非常接近并且越来越 更好的。 通常性能更高，启动速度更快，但不是 总是。

性能提升来自这样一个事实，即与运行整个操作系统副本的 VM 不同，容器与主机共享 linux 内核。 但是请注意，如果您在 Windows/macOS 上运行 linux 容器，则 Linux VM 需要作为两者之间的中间层处于活动状态。

当您想在 标准化设置：

- 构建系统
- 开发环境
- 预打包的服务器
- 运行不受信任的程序
  - 评分学生提交
  - （部分）云计算
- 持续集成 CI Continuous integration
  - Travis CI
  - GitHub Actions

此外，像 Docker 这样的容器软件也被广泛用作 [依赖地狱](https://en.wikipedia.org/wiki/Dependency_hell) 。 如果一台机器需要运行许多具有冲突依赖关系的服务，则可以使用容器将它们隔离。

通常，您编写一个文件来定义如何构建您的容器。 你从一些最小的 _基础镜像_ （比如 Alpine Linux），然后 要运行以设置所需环境的命令列表（安装 包，复制文件，构建东西，编写配置文件等）。 一般， 还有一种方法可以指定应该是的任何外部端口 可用，以及一个 _入口点_ 指示应该运行什么命令 容器启动时（如评分脚本）。

类似 [GitHub](https://github.com/) ，也有一些容器存储库网站（如 [DockerHub](https://hub.docker.com/) ），其中许多软件服务都具有可以轻松部署的预构建映像。

# Shell script

多次运行命令：

```shell
for i in $(seq 1 5); do echo hello; done
```

^9a3e9e

有很多东西要解压：

- `for x in list; do BODY; done`
  - `;`终止命令 - 相当于换行符
  - 分裂 `list`，将每个分配给 `x`, 并运行身体
  - 分裂是“空白分裂”，我们将回到
  - 外壳中没有花括号，所以 `do`+ `done`
- `$(seq 1 5)`
  - 运行程序 `seq`有论据 `1`和 `5`
  - 全部替换 `$()`与该程序的输出
  - 相当于

    ```shell
    for i in 1 2 3 4 5
    ```

### 参数拆分

Bash 按空格分割参数； 并不总是想要的！

- 需要使用引号来处理参数中的空格 `for f in "My Documents"`会正常工作

![](./attachments/Pasted%20image%2020220408111706.png)

- 其他地方也有同样的问题——你看到哪里了吗？ `test -d $f`： 如果 `$f`包含空格， `test`会出错！

![](./attachments/Pasted%20image%2020220408112035.png)

- `echo`碰巧没问题，因为 split + join by space 但是如果文件名包含换行符怎么办？！ 变成空间！
- 引用您不想拆分的所有变量的使用
- 但是我们如何修复上面的脚本呢？ 做什么 `for f in "$(ls)"`你觉得呢？

通配符就是答案！

- bash 知道如何使用模式查找文件：
  - `*`任何字符串
  - `?`任何单个字符
  - `{a,b,c}`这些字符中的任何一个
- `for f in *`: 该目录下的所有文件
- 通配时，每个匹配的文件都成为自己的参数
  - _使用_ 时仍需确保引用 ： `test -d "$f"`

![](./attachments/Pasted%20image%2020220408112419.png)

- 可以制作高级图案：
  - `for f in a*`: 所有文件以 `a`在当前目录中
  - `for f in foo/*.txt`： 全部 `.txt`文件在 `foo`
  - `for f in foo/*/p??.txt` 子目录中所有以 p 开头的三字母文本文件 `foo`

- `if [ $foo = "bar" ]; then` – see the issue?

- what if `$foo` is empty? arguments to `[` are `=` and `bar`…

if `[` 实际上程序就是 `[`, 参数是 `$foo`, `=`, `bar`, 如果 $foo 为空, 就会使程序命令执行错误
解决方法1:
`[ x$foo = "xbar" ]` , 人为给其加上一个x使其不为空，但这并不是一个好办法
解决方法2:
使用  `[[`, 它是 bash built-in 比较器， 特殊的解析，因此它还允许使用`&&`代替`-a` ,  `||`代替`-o` 等等 ^61c85f

## Job and process control

^dc91f7

- `ps`是你的朋友：列出正在运行的进程
  - `ps -A`：来自所有用户的打印进程（也 `ps ax`)
  - `ps`有 _很多_ 论点：见 `man ps`
- `pgrep`：通过搜索查找进程（== 如 `ps -A | grep`)
  - `pgrep -af`: 搜索并显示参数
- `kill`发送 _信号_ 通过 ID 向进程 `pkill`通过搜索 + `-f`)
  - 信号告诉进程“做某事”
  - 最常见的： `SIGKILL`( `-9`或者 `-KILL`退出 _现在_ 相当于 `^U`
  - 还 `SIGTERM`( `-15`或者 `-TERM`): 告诉它优雅地退出

![](./attachments/Pasted%20image%2020220408114643.png)
`stty -a | grep -Ewoe '(intr|quit|susp|kill|start|stop) = [^;]+'`
`man stty | grep -C1 signal`
获得产生信号的按键(其实即字符) ^fd9ba1

# Version Control

- add only some change in a file with `git add -p` , 一个文件的部分添加进暂存区, 进入 `patch mode`

![](./attachments/Pasted%20image%2020220408135425.png)
`y` 接受该部分 patch,
相当与 `git add -i` 后进入 `patch mode`, `-i` 表示 add contents interactively to index , 可交互式添加内容到暂存区.

- remove a file and stage its removal with `git rm`. 删除一个文件并停止追踪。
- empty the set of staged changes `git reset`
  - remove some staged changes: `git reset HEAD -- FILE` or `git reset -p` patch mode.
- check staged change with `git diff --staged` 暂存区与HEAD比较差异
- see remaining changes with `git diff`
- `git commit`, `git commit -a`

### A commit you say…

okay, we have a commit, now what?

- we can look at recent changes: `git log` (or `git log --oneline`)
- we can look at the full changes: `git log -p`
- we can show a particular commit: `git show master`
  - or with `-p` for full diff/patch
- we can go back to the state at a commit using `git checkout NAME`
  - if `NAME` is a commit hash, git says we’re “detached”. this just means there’s no `NAME` that refers to this commit, so if we make commits, no-one will know about them.
- we can revert a change with `git revert NAME`
  - applies the diff in the commit at `NAME` in reverse.
- we can compare an older version to this one using `git diff NAME..`
  - `a..b` is a commit _range_. if either is left out, it means `HEAD`.
- we can show all the commits between using `git log NAME..`
  - `-p` works here too
- we can change `master` to point to a particular commit (effectively undoing everything since) with `git reset NAME`:
  - huh, why? wasn’t `reset` to change staged changes? reset has a “second” form (see `git help reset`) which sets `HEAD` to the commit pointed to by the given name.
  - notice that this didn’t change any files – `git diff` now effectively shows `git diff NAME..`.

主要两个，一个是patch mode 和 `a..b`获得一个提交区间，如果其中一边没有被提供，则指定为 `HEAD` ^0bc161

### 名字里有什么？

显然，名称在 git 中很重要。 他们是关键 了解 _的很多_ 事情。 到目前为止，我们已经讨论过 提交哈希、master 和 `HEAD`. 但还有更多！ ^ebd0d0

- 你可以用 `git branch b`
  - 创建一个新分支， `b`，它指向提交 `HEAD`
  - 不过你仍然是“on” master，所以如果你做出新的提交， master 将指向那个新的提交， `b`将不会。
  - 切换到一个分支 `git checkout b`
    - 您所做的任何提交现在都将更新 `b`
    - 切换回master `git checkout master`
      - 你所有的变化 `b` 被隐藏起来
    - 一种非常方便的方法，可以轻松测试更改
- 标签是永远不会改变的其他名称，并且有自己的 信息。 通常用于标记发布+变更日志。
- `NAME^`意思是“之前的提交 `NAME`
  - 可以递归应用： `NAME^^^`
  - 你 _很可能_ 是说 `~`当你使用 `~`
    - `~`是“时间相关的”，而 `^`由 父节点相关的
    - `~~`  与 `^^` 是相同的
    - 和 `~`你也可以写 `X~3`对于“3 次提交早于 `X`
    - 你不想要 `^3`
  - `git diff HEAD^`
- `-`意思是“上一个的名字”
- 大多数命令都在 `HEAD`除非你给出另一个参数

### Clean up your mess

我们的提交历史可能是混乱的, 为了对未来有帮助，或者帮助其他对我们的修改感兴趣的人, 我们需要清理这些提交历史.

- `git commit --amend` 把当前工作区中的修改添加进上一次的提交中
  - 其实这会修改上一次提交，使上一次提交的 hash 发生变化
- `git rebase -i HEAD~13` 变基. 对于过去的13次提交，我们可以选择 ^925e18
  - 默认 `pick`; 什么都不做
  - `r`: change commit message 修改提交信息
  - `e`: 修改提交 (添加或删除文件)
  - `s`: 将提交与前一次的提交合并并修该提交信息
  - `f`: "fixup" 合并前一次的提交，但丢弃提交信息
  - 变基的真正作用就是将 `HEAD` 倒回起始点，然后重新按顺序重新提交
- `git reset --hard NAME`: reset the state of all files to that of `NAME`. Undoing changes.

### Playing with others

`git clone ADDRESS`(instead of `git init`).
fetch names and the commits point to from a remote with `git fetch REMOTE`.

- `git push origin master:master` 第二个master指远端的分支 ^4be489
- `git push origin master:HEAD^`
- Send changes from a specific local branch to its remote counterpart, and set the remote one as the default push/pull target of the local one: `git push -u remote_name local_branch` 将指定的本地分支的修改发送到远端，并且设置远端链接为该本地分支的默认推送拉取。 ^1e4805

### Working with other

^9d4d87

`git merge NAME`. `merge`将要：

- 寻找最新的点 `HEAD`和 `NAME` 有一个共同的祖先提交即，他们分歧的地方）
- （尝试）将所有这些更改应用于当前 `HEAD`
- 生成一个包含所有这些更改的提交，并列出两者 `HEAD`和 `NAME` 作为这个提交个父提交
- 把`HEAD` 设置到这个新的提交的哈希

一旦你的大特性完成了，你可以将它的分支合并到 master 和 git 将确保您不会丢失任何更改 分支！

如果您过去使用过 git，您可能会认出 `merge`由不同的 姓名： `pull`. 当你这样做时 `git pull REMOTE BRANCH`， 那是由他们组成：

- `git fetch REMOTE`
- `git merge REMOTE/BRANCH`
- 在哪里，比如 `push`, `REMOTE`和 `BRANCH`经常被省略和使用 “跟踪”远程分支（记住 `-u`?)

这通常效果 _很好_ 。 只要对分支的更改是 合并是不相交的。 如果不是，您会遇到 _合并冲突_ 。

- 合并冲突只是 git 告诉你它不知道最终的差异应该是什么样的
- git 暂停并要求您完成“合并提交”的暂存
- 在编辑器中打开有冲突的文件并寻找很多角度 括号 ( `<<<<<<<`）。 上面的东西 `=======`是在 这 `HEAD`自共享祖先提交以来。 下面的东西是 中所做的更改 `NAME`自共享提交以来。
- `git mergetool`非常方便——打开一个差异编辑器
- 一旦你 _解决_ 通过找出文件的内容 现在应该看起来像，将这些更改与 `git add`.
- 当所有冲突都解决后，完成 `git commit`
  - 你可以放弃 `git merge --abort`

你刚刚解决了你的第一个 git 合并冲突！ \o/ 现在您可以发布完成的更改 `git push`

### When worlds collide 当发生碰撞

^2ba562

当 push 时，git 会检查我们的修改会不会使先前的修改丢失。它会检查远端的HEAD节点是否是这次推送提交的祖先节点, 如果是的话就成功更新(fast-forwarding), 如果不是，它会拒绝更新远端.

当被拒绝时有几种解决方法:

- 先merge远端修改`git pull` (i.e, `fetch` + `merge`)
- 强制推送 `--force`, 它会使得其他人的修改丢失
  - `--force-with-lease` 只会在我们上一次 fetch 到 这次 push 的时间间隔内，远端没有发生过改变的情况下强制推送
  - 如果在本地进行过变基，就必须强制推送。因为父节点已经发生变化了。
- 尝试在远程更改的“之上”重新应用您的更改
  - 这是一个 `rebase`！
    - 倒回自共享祖先以来的所有本地提交
    - 快进 `HEAD`以远程名称提交
    - 按顺序应用本地提交
      - 可能有您必须手动解决的冲突
      - `git rebase --continue`或者 `--abort`
  - `git pull --rebase`将为您启动此过程

# Machine Introspection 机器自省

## What happened?

传统上，日志都存储在 `/var/log`，而且许多仍然是。 通常每个程序都有一个文件或文件夹。 采用 `grep`或者 `less`到 找到你的出路。

还有一个内核日志，您可以使用 `dmesg`命令。 这曾经以纯文本文件的形式提供，但现在你经常 必须通过 `dmesg`去解决它。

最后是“系统日志”，它越来越多地显示所有 你的日志消息去。 在 _大多数_ （尽管不是全部）Linux 系统上，该日志 由管理 `systemd`，“系统守护进程”，它控制所有 在后台运行的服务（此时还有更多）。 可以通过有点不方便的方式访问该日志 `journalctl` 如果您是 root 用户，或者是 `admin`或者 `wheel`组。

为了 `journalctl`，您应该特别注意这些标志： ^5f85fe

- `-u UNIT`：仅显示与给定 systemd 服务相关的消息
- `--full`：不要截断长行（最愚蠢的功能）
- `-b`: 仅显示最新启动的消息（另请参阅 `-b -2`)
- `-n100`: 只显示最后 100 个条目

## Wht is happining?

首先，有 `top`, 和改进的版本 `htop`, 这显示你 系统上当前正在运行的进程的各种统计信息。 CPU使用，内存使用，进程树等。有很多快捷方式， 但 `t`对于启用树视图特别有用。 你也可以 查看进程树 `pstree`(+ `-p`包括 PID）。 如果你想 要知道这些程序在做什么，您通常会想跟踪他们的 日志文件。 `journalctl -f` (follow journal) , `dmesg -w` (follow, wait for new messages)， 和 `tail -f` (same as follow). ^01ed2d

了解总体使用的资源。 [`dstat`](http://dag.wiee.rs/home-made/dstat/)是 非常好。 它为您提供了许多实时资源指标 不同的子系统，例如 I/O、网络、CPU 利用率、上下文 开关等。 `man dstat`是开始的地方。

如果您的磁盘空间不足，则有两个主要实用程序 你会想知道： `df`和 `du`. 前者向您展示了 系统上所有分区的状态（尝试使用 `-h`）， 然而 后者测量你给它的所有文件夹的大小，包括 它们的内容（另见 `-h`和 `-s`）。

要弄清楚您打开了哪些网络连接， `ss`是方法。 `ss -t`将显示所有打开的 TCP 连接。 `ss -tl`将显示所有 监听系统上的（即服务器）端口。 `-p`还将包括 哪个进程正在使用该连接，以及 `-n`会给你生的 端口号。 ^224e70

## 系统配置

有 _很多_ 方法可以配置您的系统，但我们会解决的 两个非常常见的：网络和服务。 您的大多数应用程序 系统会告诉你如何在他们的手册页中配置它们，通常它 将涉及编辑文件 `/etc`; 系统配置 目录。

如果要配置网络， `ip`命令让你做 那。 它的论点采取了一种有点奇怪的形式，但是 `ip help command` 会让你走得很远。 `ip addr`向您显示有关您的信息 网络接口及其配置方式（IP 地址等）， 和 `ip route`向您展示网络流量如何路由到不同的 网络主机。 网络问题通常可以纯粹通过 `ip`工具。 还有 `iw`用于管理无线网络接口。 `ping`是一个方便的工具，用于检查事物被破坏的程度。 尝试 ping 主机名 (google.com)、外部 IP 地址 (1.1.1.1) 和 内部 IP 地址（192.168.1.1 或默认 gw）。 您可能还想 摆弄 `/etc/resolv.conf`检查您的 DNS 设置（主机名如何 被解析为 IP 地址）。

要配置服务，您几乎必须与 `systemd`这些天，无论好坏。 您系统上的大多数服务将 有一个定义 systemd _单元_ 。 这些文件 定义启动该服务时要运行的命令，如何停止 它，在哪里记录东西等等。它们通常不会太难读，并且 你可以在其中找到大部分 `/usr/lib/systemd/system/`. 你也可以 定义你自己的 `/etc/systemd/system`.

一旦您想到了 systemd 服务，您就可以使用 `systemctl`命令 与它互动。 `systemctl enable UNIT`将服务设置为 开机启动（ `disable`再次删除它），和 `start`, `stop`， 和 `restart`会做你所期望的。 如果出现问题，systemd 将 让你知道，你可以使用 `journalctl -u UNIT`看到 应用程序的日志。 你也可以使用 `systemctl status`看看怎么样 你的系统服务在做什么。 如果你的启动感觉很慢，可能是 由于一些缓慢的服务，您可以使用 `systemd-analyze`（尝试 它与 `blame`) 找出哪些。

# Web
## 搜索运算符

^aa59be

像 Google 或 DuckDuckGo 这样的网络搜索引擎提供了搜索运算符来实现更精细的网络搜索：

-   `"bar foo"`强制 bar foo 完全匹配
-   `foo site:bar.com`在 bar.com 中搜索 foo
-   `foo -bar` 从搜索中排除包含 bar 的术语
-   `foobar filetype:pdf`搜索该扩展名的文件
-   `(foo|bar)`搜索具有 foo OR bar 的匹配项

更多通过列表可用于 [Google](https://ahrefs.com/blog/google-advanced-search-operators/) 和 [DuckDuckGo](https://duck.co/help/results/syntax)