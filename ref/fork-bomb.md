---
date created: 2022-04-08 10:54
---

Read what a [fork-bomb](https://en.wikipedia.org/wiki/Fork_bomb) (`:(){ :|:& };:`) is and run it on the VM to see that the resource isolation (CPU, Memory, &c) works.

在 [计算](https://en.wikipedia.org/wiki/Computing "计算") 中， **分叉炸弹** （也称为 **兔子病毒** 或 **wabbit** )(<https://en.wikipedia.org/wiki/Fork_bomb#cite_note-wabbit-1>) ）是一种 [拒绝服务攻击](https://en.wikipedia.org/wiki/Denial-of-service_attack "拒绝服务攻击") ，其中一个 [进程](https://en.wikipedia.org/wiki/Process_(computing) "过程（计算）") 而减慢或崩溃系统 [资源匮乏](https://en.wikipedia.org/wiki/Resource_starvation "资源匮乏") 。

A classic example of a fork bomb is the [Unix shell](https://en.wikipedia.org/wiki/Unix_shell "Unix shell") one `:(){ :|:& };:`, which can be more easily understood as:

```shell
fork() {
    fork | fork &
}
fork
```

In it, a function is defined (`fork()`) as calling itself (`fork`), then [piping](https://en.wikipedia.org/wiki/Pipeline_(Unix) "Pipeline (Unix)") (`|`) its result to a background [job](https://en.wikipedia.org/wiki/Job_(Unix) "Job (Unix)") of itself (`&`).
