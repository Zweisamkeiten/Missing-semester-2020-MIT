# Bash Arithmetic
## Let
---
```shell
let <arithmetic expression>
```
```shell
1.  #!/bin/bash
2.  # Basic arithmetic using let

4.  let a=5+4
5.  echo $a # 9

7.  let "a = 5 + 4"
8.  echo $a # 9

10.  let a++
11.  echo $a # 10

13.  let "a = 4 * 5"
14.  echo $a # 20

16.  let "a = $1 + 30"
17.  echo $a # 30 + first command line argument
```
## Expr
---
```shell
expr item1 operator item2
```
```shell
#!/bin/bash
# Basic arithmetic using expr
expr 5 + 4
expr "5 + 4"
expr 5+4
expr 5 \* $1
expr 11 % 2
a=$( expr 10 - 3 )
echo $a # 7
```
## Double Parentheses
---
我们可以轻松地将命令的输出保存到变量中。 事实证明，如果我们稍微调整一下语法，这个机制也能够为我们做基本的算术。 我们通过使用这样的双括号来做到这一点：
```shell
$(( expression ))
```
```shell
1.  #!/bin/bash
2.  # Basic arithmetic using double parentheses

4.  a=$(( 4 + 5 ))
5.  echo $a # 9

7.  a=$((3+5))
8.  echo $a # 8

10.  b=$(( a + 3 ))
11.  echo $b # 11

13.  b=$(( $a + 4 ))
14.  echo $b # 12

16.  (( b++ ))
17.  echo $b # 13

19.  (( b += 3 ))
20.  echo $b # 16

22.  a=$(( 4 * 5 ))
23.  echo $a # 20
```
## Length of a Variable
这不是真正的算术，但它可能非常有用。 如果您想找出变量的长度（有多少个字符），您可以执行以下操作： 
```shell
${#variable}
```
```shell
#!/bin/bash
# Show the length of a variable.
a='Hello World'
echo ${#a} # 11
b=4953
echo ${#b} # 4
```
