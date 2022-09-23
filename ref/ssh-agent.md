# ssh-agent - 如何配置、转发、协议。

这 `ssh-agent`是一个帮助程序，用于跟踪用户的 [身份密钥](https://www.ssh.com/ssh/identity-key) 及其 [密码](https://www.ssh.com/ssh/passphrase) 。 然后，代理可以使用密钥登录其他服务器，而无需用户再次输入密码或密码。 这实现了一种单点登录 (SSO) 形式。

SSH 代理用于 [SSH 公钥认证](https://www.ssh.com/ssh/public-key-authentication) 。 它使用 [SSH 密钥](https://www.ssh.com/ssh/key) 进行身份验证。 用户可以使用 [ssh-keygen](https://www.ssh.com/ssh/keygen) 将它们安装在服务器上 [ssh-copy-id](https://www.ssh.com/ssh/copy-id) 。

### 内容

[开始 `ssh-agent`](https://www.ssh.com/academy/ssh/agent#starting-ssh-agent) [将 SSH 密钥添加到代理](https://www.ssh.com/academy/ssh/agent#adding-ssh-keys-to-the-agent) [SSH 代理转发](https://www.ssh.com/academy/ssh/agent#ssh-agent-forwarding) [运行 `ssh-agent`](https://www.ssh.com/academy/ssh/agent#running-ssh-agent) [延伸阅读](https://www.ssh.com/academy/ssh/agent#further-reading)

## 运行 `ssh-agent`

在大多数 Linux 系统上， `ssh-agent`在登录时自动配置和运行，使用它不需要额外的操作。 但是， [SSH 密钥](https://www.ssh.com/ssh/key) 仍必须为用户创建

如果 `ssh-agent`登录时不会自动启动，可以用命令手动启动

```shell
eval `ssh-agent`
```

这 `ssh-agent` command 输出命令以在 shell 中设置某些环境变量。 默认输出的命令兼容 `/bin/sh`和 `/bin/bash`. 为 C-shell 输出命令 ( `/bin/csh`或者 `/bin/tcsh`）， 添加 `-c`.

最简单的检查方法是检查 `SSH_AGENT_SOCK`环境变量。 如果已设置，则代理可能正在运行。 可以通过以下方式检查

```shell
echo $SSH_AGENT_SOCK
```

此外，为了允许基于密钥的服务器登录， [公钥身份验证](https://www.ssh.com/ssh/public-key-authentication) 必须在服务器上启用 在 [OpenSSH](https://www.ssh.com/ssh/openssh/) 中，它默认启用。 它是由控制 `PubkeyAuthentication`的选项 [sshd_config](https://www.ssh.com/ssh/sshd_config/) 。

## 将 SSH 密钥添加到代理

默认情况下，代理使用存储在 `.ssh`用户主目录下的目录。 。 [ssh-add](https://www.ssh.com/ssh/add) 命令用于向代理添加身份 以最简单的形式，只需运行 if 不带参数即可添加默认文件 `~/.ssh/id_rsa`, `.ssh/id_dsa`, `~/.ssh/id_ecdsa`, `~/.ssh/id_ed25519`， 和 `~/.ssh/identity`. 否则，将私钥文件的名称作为参数添加。

以下命令将列出代理当前可访问的私钥：

```shell
ssh-add -l
```

## SSH 代理转发

此外， [SSH 协议](https://www.ssh.com/ssh/protocol/) 实现 _代理转发_ ，一种 [SSH 客户端](https://www.ssh.com/ssh/client) 允许 [SSH 服务器](https://www.ssh.com/ssh/server) 使用本地 `ssh-agent`在用户登录的服务器上，就好像它是本地的一样。 当用户在服务器上使用 SSH 客户端时，客户端会尝试联系服务器实现的代理，然后服务器将请求转发给最初联系服务器的客户端，客户端再将请求转发给本地代理。 这边走， `ssh-agent`和代理转发实现可以传递的单点登录。

SSH 提供的单点登录的一个奇妙特性是它独立于组织边界和地理位置而工作。 您可以轻松地在世界另一端、云服务或客户场所的服务器上实施单点登录。 不需要中央协调。

要使用代理转发， `ForwardAgent`选项必须设置为 `yes`在客户端（参见 [ssh_config](https://www.ssh.com/ssh/config/) ）和 `AllowAgentForwarding`选项必须设置为 `yes`在服务器上（参见 [sshd_config](https://www.ssh.com/ssh/sshd_config/) ）。

## run `ssh-agent`

这 `ssh-agent`命令通常在登录时从初始化脚本运行，例如从 `/etc/X11/Xsession.d/90x11-common_ssh-agent`在 Linux Mint LMDE 上。 或者，任何用户都可以将其配置为从例如用户的 `~/.xsession`文件或 `~/.profile`.

代理会输出此设置的环境变量设置。 这 `SSH_AUTH_SOCK`环境变量设置为指向用于与代理通信的 unix 域套接字，并且 `SSH_AGENT_PID`环境变量设置为代理的进程 ID。 要在用户的 shell 环境中设置环境变量，代理通常运行如下：

```shell
eval `ssh-agent`
```

这 `ssh-agent`命令接受以下选项：

**-a 绑定地址**

强制将 Unix 域套接字绑定到给定的文件路径，而不是默认套接字。

**-C**

强制在标准输出上生成 C-shell 命令。 默认情况下会自动检测外壳。

**-d**

启用调试模式。

**-E Fingerprint_hash** 指定用于生成 SSH 密钥指纹的算法。 有效值包括 `md5`和 `sha256`.

**-k**

杀死当前正在运行的代理。

**-s**

强制生成 Bourne shell ( `/bin/sh`) 标准输出上的命令。 默认情况下会自动检测外壳。

**-t 生命**

指定身份在代理中保留的最大秒数。 该值以秒为单位，但可以添加后缀 `m`几分钟， `h`用了几个小时， `d`几天，和 `w`数周。 如果没有此选项，代理将在其运行期间将密钥保存在其内存中。 这可以在运行 [ssh-add](https://www.ssh.com/ssh/add) 命令时被覆盖。

## 延伸阅读

-   [SSH 密钥管理](https://www.ssh.com/iam/ssh-key-management)
    
-   [原始代理协议 Internet-Draft (2001)](https://tools.ietf.org/html/draft-ietf-secsh-agent-00)
    
-   [较新的代理协议 Internet-Draft (2016)](https://tools.ietf.org/html/draft-miller-ssh-agent-00)

# 我的配置过程 (Archlinux)

^3e75f9

1. 在 `$XDG_CONFIG_HOME/X11/xprofile` 中添加 
```shell
eval `ssh-agent`
```
使之能够在桌面环境运行后自动启动
2. 
![[Pasted image 20220406190338.png]]
3. 
![[Pasted image 20220406190400.png]]
这样就不用每次使用有密码保护的密钥时都要输入密码了

每次重启后都需要重复操作，可以通过脚本配置
