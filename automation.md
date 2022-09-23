---
date created: 2022-04-08 16:05
---

# Automation

在大多数 UNIX 系统上，cron 守护进程， `crond`将默认运行，但您可以随时使用 `ps aux | grep crond`.

cron 的配置文件可以显示运行 `crontab -l`编辑运行 `crontab -e`cron 使用的时间格式是五个空格分隔的字段以及用户和命令

- **minute** - 命令将在每小时的哪一分钟运行， 介于“0”和“59”之间
- **hour** - 这控制命令将运行的时间，并在 24 小时制，值必须介于 0 和 23 之间（0 是午夜）
- **dom** - 这是您希望运行命令的每月的日，例如 在每个月的 19 号运行一个命令，dom 将是 19。
- **month** - 这是指定命令运行的月份，可以指定 数字（0-12），或作为月份的名称（例如五月）
- **dow** - 这是您希望运行命令的星期几，它可以 也可以是数字 (0-7) 或作为一天的名称（例如太阳）。
- **user** - 这是运行命令的用户。
- **command** - 这是您要运行的命令。 该字段可能包含 多个单词或空格。

请注意，使用星号 `*`表示全部，使用星号后跟斜杠，数字表示每第 n 个值。 所以 `*/5`意思是每五个。 一些例子是

```shell
*/5   *    *   *   *       # Every five minutes
  0   *    *   *   *       # Every hour at o'clock
  0   9    *   *   *       # Every day at 9:00 am
  0   9-17 *   *   *       # Every hour between 9:00am and 5:00pm
  0   0    *   *   5       # Every Friday at 12:00 am
  0   0    1   */2 *       # Every other month, the first day, 12:00am
```
## Shell 环境和日志记录

使用 cron 时的一个常见缺陷是它不会加载与普通 shell 相同的环境脚本，例如 `.bashrc`, `.zshrc`, &c 并且默认情况下它不会在任何地方记录输出。 结合最大频率为一分钟，最初调试 cronscript 会变得非常痛苦。

要处理环境，请确保在所有脚本中使用绝对路径并修改环境变量，例如 `PATH`所以脚本可以成功运行。 为了简化日志记录，一个好的建议是以这样的格式编写你的 crontab

```shell
* * * * *   user  /path/to/cronscripts/every_minute.sh >> /tmp/cron_every_minute.log 2>&1
```

并将脚本写入单独的文件中。 请记住 `>>`附加到文件中 `2>&1`重定向 `stderr`到 `stdout`（尽管您可能希望将它们分开）。

## Anacron
使用 cron 的一个警告是，如果计算机在 cron 脚本应该运行时关闭或处于睡眠状态，则它不会被执行。 对于频繁的任务，这可能很好，但如果任务运行频率较低，您可能希望确保它被执行。 [anacron](https://linux.die.net/man/8/anacron) 的工作原理类似于 `cron`除了频率以天为单位指定。 与 cron 不同，它不假定机器连续运行。 因此，它可以在不是一天 24 小时运行的机器上使用，将常规作业控制为每日、每周和每月作业