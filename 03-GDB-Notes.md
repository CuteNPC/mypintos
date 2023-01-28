# GDB Notes

2020.10.22

## GDB 使用简易手册

GDB 是 GNU 套装中的调试器，下面是一个简易的手册，[这里](http://www.gnu.org/software/gdb/documentation/)是官方的全面手册。

### 开始调试

- 要使用GDB调试程序，gcc 编译的时候需要加上 -g 选项，比如 gcc foo.c -g -o foo.o
- 调试名为 foo 的程序：在 shell 中输入 gdb foo，或者在gdb中输入run foo
- 退出 gdb：`q` 或者 `ctrl+D`
- 在 gdb 中输入 `help`可以查看基本的实用指南

### 过程的调试

- 断点操作

  断点是将给定位置的指令替换为 `int $3`, 当 CPU 运行到这条指令时会自动保存寄存器的值并挂起该进程，交给 gdb 来处理。下面是 breakpoint 的操作

  > - 在 C 代码的第 i 行设置一个断点：`b i`
  > - 在文件 foo.c 的第 i 行设置一个断点：`b foo.c:i`
  > - 在函数 bar 入口设置一个断点：`b bar`
  > - 查看所有断点：`info b`
  > - 删除编号为 i 的断点：`delete i`
  > - 清除所有断点：`clear`
  > - 设置当 `a == 1`时在第 `i` 行中断的断点： `b i if a == 1`

  watch 是当某个表达式发生变化时会产生中断的断点。下面是 watch 的操作

  > - 在变量 a 发生变化的时候产生中断：`watch a`
  > - 在表达式 a+b 发生变化时产生中断：`watch a+b`

- 调试步骤操作

  - 运行直到下一断点：`c`
  - 运行一条指令，step into：`si`
  - 运行 k 条指令，step into：`si k`
  - 运行一条指令，step over：`ni`
  - 运行一条函数语句，step into：`s`
  - 运行 k 条函数语句，step into：`s k`
  - 运行一条函数语句，step over：`n`

- 查看数据/变量

  - 数据格式：在指令 xxx 中输出某种格式 yyy 的数据：xxx/yyy
    - 十六进制数：x
    - 八进制数：o
    - 二进制数：t
    - 字符：c
    - 输出指令：i
  - 输出一个表达式 exp：`p exp`
    - 寄存器 `%rsp` 用 `$rsp` 表示
    - 表达式按照 C 语言语法，比如`*(char*)&a`
  - 输出地址A的数据：`x A`
    - 输出 n 个16进制数数据：`x/nx A`
    - 输出 n 条指令：`x/ni A`
  - 反汇编当前代码：`disas`

- 图形界面调试器

  - 启用图形界面：`tui enable`
  - 关闭图形界面：`tui disable`