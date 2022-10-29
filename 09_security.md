---
date created: 2022-10-29 17:24
date updated: 2022-10-29 19:16
---

## 熵

熵等于`log_2(所有可能的个数，即n)`

## 哈希函数

加密 [哈希 函数](https://en.wikipedia.org/wiki/Cryptographic_hash_function) 映射数据 任意大小到固定大小，并具有一些特殊属性。 粗略 哈希函数的规范如下：

```
hash(value: array<byte>) -> vector<byte, N>  (for some fixed N)
```

哈希函数的一个示例是 [SHA1](https://en.wikipedia.org/wiki/SHA-1) ， 在 Git 中使用。 它将任意大小的输入映射到 160 位输出

```sh
$ printf 'hello' | sha1sum
aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d
$ printf 'hello' | sha1sum
aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d
$ printf 'Hello' | sha1sum 
f7ff9e8b7bb2e09b70935a5d785e0cc5d9d0abf0
```

在高层次上，哈希函数可以被认为是一个难以反转的函数 看起来随机（但具有确定性）的函数

- 确定性：相同的输入总是产生相同的输出。
- 不可逆：很难找到输入 `m`这样 `hash(m) = h`为了 一些期望的输出 `h`.
- 目标抗碰撞：给定输入 `m_1`, 很难找到 不同的输入 `m_2`这样 `hash(m_1) = hash(m_2)`.
- 防碰撞：很难找到两个输入 `m_1`和 `m_2`这样 `hash(m_1) = hash(m_2)`（请注意，这是一个严格比强于 目标碰撞阻力）。

## 密钥导出函数

[密钥生成函数](https://en.wikipedia.org/wiki/Key_derivation_function) (Key Derivation Functions) 作为密码散列函数的相关概念，被应用于包括生成固定长度，可以使用在其他密码算法中的密钥等方面。 为了对抗穷举法攻击，密钥生成函数通常较慢。[bcrypt 加盐](../languages/javascript/bcrypt%20加盐.md)

- 存储登录凭证时不可直接存储明文密码。  正确的方法是针对每个用户随机生成一个[盐](https://en.wikipedia.org/wiki/Salt_(cryptography)) `salt = random()`， 并存储盐，以及密钥生成函数对连接了盐的明文密码生成的哈希值`KDF(password + salt)`。  在验证登录请求时，使用输入的密码连接存储的盐重新计算哈希值`KDF(input + salt)`，并与存储的哈希值对比。

## 对称密码学

说到加密，可能你会首先想到隐藏明文信息。对称加密使用以下几个方法来实现这个功能：

```
keygen() -> key  (这是一个随机方法)

encrypt(plaintext: array<byte>, key) -> array<byte>  (输出密文)
decrypt(ciphertext: array<byte>, key) -> array<byte>  (输出明文)
```

加密方法`encrypt()`输出的密文`ciphertext`很难在不知道`key`的情况下得出明文`plaintext`。\
解密方法`decrypt()`有明显的正确性。因为功能要求给定密文及其密钥，解密方法必须输出明文：`decrypt(encrypt(m, k), k) = m`。

[AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) 是现在常用的一种对称加密系统。

### 对称加密的应用

- 加密不信任的云服务上存储的文件。对称加密和密钥生成函数配合起来，就可以使用密码加密文件： 将密码输入密钥生成函数生成密钥 `key = KDF(passphrase)`，然后存储`encrypt(file, key)`。

## 非对称加密

非对称加密的“非对称”代表在其环境中，使用两个具有不同功能的密钥： 一个是私钥(private key)，不向外公布；另一个是公钥(public key)，公布公钥不像公布对称加密的共享密钥那样可能影响加密体系的安全性。\
非对称加密使用以下几个方法来实现加密/解密(encrypt/decrypt)，以及签名/验证(sign/verify)：

```
keygen() -> (public key, private key)  (这是一个随机方法)

encrypt(plaintext: array<byte>, public key) -> array<byte>  (输出密文)
decrypt(ciphertext: array<byte>, private key) -> array<byte>  (输出明文)

sign(message: array<byte>, private key) -> array<byte>  (生成签名)
verify(message: array<byte>, signature: array<byte>, public key) -> bool  (验证签名是否是由和这个公钥相关的私钥生成的)
```

非对称的加密/解密方法和对称的加密/解密方法有类似的特征。\
信息在非对称加密中使用 _公钥_ 加密， 且输出的密文很难在不知道 _私钥_ 的情况下得出明文。\
解密方法`decrypt()`有明显的正确性。 给定密文及私钥，解密方法一定会输出明文： `decrypt(encrypt(m, public key), private key) = m`。

**对称加密和非对称加密可以类比为机械锁。 对称加密就好比一个防盗门：只要是有钥匙的人都可以开门或者锁门。 非对称加密好比一个可以拿下来的挂锁。你可以把打开状态的挂锁（公钥）给任何一个人并保留唯一的钥匙（私钥）。这样他们将给你的信息装进盒子里并用这个挂锁锁上以后，只有你可以用保留的钥匙开锁。** #非对称加密

签名/验证方法具有和书面签名类似的特征。\
在不知道 _私钥_ 的情况下，不管需要签名的信息为何，很难计算出一个可以使 `verify(message, signature, public key)` 返回为真的签名。\
对于使用私钥签名的信息，验证方法验证和私钥相对应的公钥时一定返回为真： `verify(message, sign(message, private key), public key) = true`。

### 非对称加密的应用

- [PGP电子邮件加密](https://en.wikipedia.org/wiki/Pretty_Good_Privacy)：用户可以将所使用的公钥在线发布，比如：PGP密钥服务器或 [Keybase](https://keybase.io/)。任何人都可以向他们发送加密的电子邮件。
- 聊天加密：像 [Signal](https://signal.org/) 和 [Keybase](https://keybase.io/) 使用非对称密钥来建立私密聊天。
- 软件签名：Git 支持用户对提交(commit)和标签(tag)进行GPG签名。任何人都可以使用软件开发者公布的签名公钥验证下载的已签名软件。

**SSH登录安全性由非对称加密保证，产生密钥时，一次产生两个密钥，一个公钥，一个私钥，在git中一般命名为id_rsa.pub, id_rsa。**

那么如何使用生成的一个私钥一个公钥进行验证呢？

- 本地生成一个密钥对，其中公钥放到远程主机，私钥保存在本地

- 当本地主机需要登录远程主机时，本地主机向远程主机发送一个`登录请求`，远程收到消息后，服务器选择一个随机数字发送给客户端。客户端使用用户私钥对这个数字信息签名后返回服务器。 服务器随后使用`.ssh/authorized_keys`文件中存储的用户公钥来验证返回的信息是否由所对应的私钥所签名。这种验证方式可以有效证明试图登录的用户持有所需的私钥。 ^68186e

## 练习

假设一个密码是从四个小写的单词拼接组成，每个单词都是从一个含有10万单词的字典中随机选择，且每个单词选中的概率相同。 一个符合这样构造的例子是 `correcthorsebatterystaple` 。这个密码有多少比特的熵？ 假设另一个密码是用八个随机的大小写字母或数字组成。一个符合这样构造的例子是 `rg8Ql34g` 。这个密码又有多少比特的熵？

```
Entropy = log_2(100000^4) = 66 #correcthorsebatterystaple
Entropy = log_2((26+26+10)^8) = 48 #rg8Ql34g
```

2.密码散列函数

```shell
cat SHA256SUMS | grep debian-10.9.0-amd64-netinst.iso
8660593d10de0ce7577c9de4dab886ff540bc9843659c8879d8eea0ab224c109  debian-10.9.0-amd64-netinst.iso

shasum -a 256 debian-10.9.0-amd64-netinst.iso
8660593d10de0ce7577c9de4dab886ff540bc9843659c8879d8eea0ab224c109  debian-10.9.0-amd64-netinst.iso
```

```sh
diff <(cat SHA256SUMS |grep debian-10.9.0-amd64-netinst.iso) <(shasum -a 256 debian-10.9.0-amd64-netinst.iso)
```

3.对称加密

使用 OpenSSL的AES模式加密一个文件: `openssl aes-256-cbc -salt -in {源文件名} -out {加密文件名}`。 使用`cat`或者`hexdump`对比源文件和加密的文件，再用 `openssl aes-256-cbc -d -in {加密文件名} -out {解密文件名}` 命令解密刚刚加密的文件。最后使用`cmp`命令确认源文件和解密后的文件内容相同。

```sh
openssl aes-256-cbc -salt -in test -out test.enc -pbkdf2
enter aes-256-cbc encryption password:
Verifying - enter aes-256-cbc encryption password:
```

使用 `hexdump`比较两个文件

```sh
diff <(hexdump test) <(hexdump test.enc)
1,2c1,3
< 0000000 7566 6b63 0a73 7366 6174 7472 000a
< 000000d
---
> 0000000 6153 746c 6465 5f5f 2fef b689 5fee 964e
> 0000010 6f0e 3ed9 fbb1 5bd8 f6e0 e743 9d66 8752
> 0000020
```

使用`cat`比较两个文件

```sh
diff <(cat test) <(cat test.enc)
1,2c1
< fucks
< fstart
---
> Salted__�/���_N�o�>���[��C�f�R�
\ No newline at end of file
```

对文件进行解密

```sh
openssl aes-256-cbc -d -in test.enc -out test2 -pbkdf2
```

4.非对称加密

1. 在你自己的电脑上使用更安全的 [ED25519](https://wiki.archlinux.org/index.php/SSH_keys#Ed25519) 算法生成一组 [SSH 密钥对](https://wiki.archlinux.org/index.php/SSH_keys#Ed25519)。为了确保私钥不使用时的安全，一定使用密码加密你的私钥。

   ```
    ssh-keygen -t ed25519 
   ```

2. [配置GPG](https://www.digitalocean.com/community/tutorials/how-to-use-gpg-to-encrypt-and-sign-messages)。 Linux 系统可以直接按照上面的教程操作，MacOS 上的操作过程如下

   ```
    $ brew install gpg
    $ gpg --gen-key
   ```

^dc731c
3. 给Anish发送一封加密的电子邮件（[Anish的公钥](https://keybase.io/anish)）。

```
gpg --encrypt --sign --armor -r me@anishathalye.com name_of_fil
```

4. 使用`git commit -S`命令签名一个Git提交，并使用`git show --show-signature`命令验证这个提交的签名。或者，使用git tag -s命令签名一个Git标签，并使用`git tag -v`命令验证标签的签名。

   ```
    git commit -S -m "sign a commit"
   ```

   可能会出现下面的错误

   ```
    error: gpg failed to sign the data
    fatal: failed to write commit object
   ```

   这个问题网上有一些解决方案可供参考：

   - [Git error - gpg failed to sign data](https://stackoverflow.com/questions/41052538/)
   - [Set up Keybase.io, GPG & Git to sign commits on GitHub](https://github.com/pstadler/keybase-gpg-github)

   如果遇到

   ```
    echo "test" | gpg --clearsign
    gpg: [stdin]: clear-sign failed: Inappropriate ioctl for device
   ```

   则执行

   ```
    export GPG_TTY=$(tty)
   ```

   此外要注意`~/.gitconfig`里面的 name，email 要和生成秘钥时使用的一样，签名算法也是一样的：

   ```
    gpg -K --keyid-format SHORT
    /Users/lingfeng/.gnupg/pubring.kbx
    ----------------------------------
    sec   rsa2048/56EF5DE3 2021-05-15 [SC] [有效至：2023-05-15]
        35A0BAB790EBBFE193422975097FC49956EF5DE3
    uid         [ 绝对 ] hanxiaomax-mac <hanxiaomax@qq.com>
    ssb   rsa2048/55FB9195 2021-05-15 [E] [有效至：2023-05-15]
   ```

   对应的 `.gitconfig`为

   ```
    [user]
        name = hanxiaomax-mac
        email = hanxiaomax@qq.com
        signingKey = 55FB9195
   ```

   所有问题都解决后，正常签名

   ```
    git commit -S -m "sign a commit"
    [main fc8e916] sign a commit
    3 files changed, 3 insertions(+)
    create mode 100644 security/afile
    create mode 100644 security/notsafefile
    create mode 100644 security/secfile
   ```

![](attachments/Pasted%20image%2020221029182018.png)
