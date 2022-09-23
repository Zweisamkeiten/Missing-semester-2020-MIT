## env
**env**是 [shell](https://en.wikipedia.org/wiki/Unix_shell "Unix 外壳") [命令](https://en.wikipedia.org/wiki/Command_(computing) "命令（计算）") 。 [Unix](https://en.wikipedia.org/wiki/Unix "Unix") 和 [类 Unix](https://en.wikipedia.org/wiki/Unix-like "类 Unix") [操作系统](https://en.wikipedia.org/wiki/Operating_system "操作系统") 的 它用于打印 [环境变量](https://en.wikipedia.org/wiki/Environment_variable "环境变量") 或在更改的环境中运行另一个实用程序，而无需修改当前存在的环境。 使用 `env`，可以添加或删除变量，并且可以通过为它们分配新值来更改现有变量。

在实践中， `env`还有另一个常见的用途。 经常使用它 [shell 脚本](https://en.wikipedia.org/wiki/Shell_script "外壳脚本") 来启动正确的 [解释器](https://en.wikipedia.org/wiki/Interpreter_(computing) "口译员（计算）") 。 在这种用法中，环境通常不会改变。

### Example
---
To print out the set of current environment variables:
```shell
env
```
To create a new environment without any existing environment variables for a new shell:
```shell
env -i /bin/sh
```
env 也可以在脚本的 [hashbang](https://en.wikipedia.org/wiki/Hashbang "哈希邦") 行中使用，以允许 [解释器](https://en.wikipedia.org/wiki/Interpreter_(programming) "口译员（编程）") 通过 PATH 查找 例如，这是一个 [Python](https://en.wikipedia.org/wiki/Python_(programming_language) "Python（编程语言）") 脚本的代码：

```python
#!/usr/bin/env python3
print("Hello, World!")
```
在这个例子中， `/usr/bin/env`是完整 [路径](https://en.wikipedia.org/wiki/Path_(computing) "路径（计算）") 的 `env`命令。 环境没有改变。

请注意，可以在不使用的情况下指定解释器 `env`，通过给出完整路径 `python` 解释器。 这种方法的一个问题是，在不同的计算机系统上，确切的路径可能不同。 通过改为使用 `env`在示例中，解释器在脚本运行时被搜索并定位（更准确地说， `env`进行系统调用 `execvp`，它负责定位解释器并启动它）。 这使脚本更具 [可移植性](https://en.wikipedia.org/wiki/Porting "移植") ，但也增加了选择错误解释器的风险，因为它在可执行搜索路径上的每个目录中搜索匹配项。 它也面临着同样的问题，即通往 `env`二进制文件在每台机器上也可能不同。
