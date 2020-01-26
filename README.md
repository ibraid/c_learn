# c-learn

linux c 一站式编程学习

## 第七章笔记

SICP 指出, 在学习一门编程语言要特别注意一下三个方面:

1. 这门语言提供了哪些 Primitive, 比如基本类型, 比如基本运算符, 表达式和语句.
2. 这门语言提供了哪些组合规则, 比如基本类型如何组成复合类型, 比如简单的表达式和语句如何组成复杂的表达式和语句.
3. 这门语言提供了哪些抽象机制, 包括数据抽象和过程抽象 (Procedure Abstraction).

## gdb 基本命令 1

| 命令                | 描述                                               |
| ------------------- | -------------------------------------------------- |
| backtrack (或者 bt) | 查看各级函数调用及参数                             |
| finish              | 连续运行到当前函数返回为止, 然后停下来等待命令     |
| frame (或 f) 帧编号 | 选择栈帧                                           |
| info （或 i) locals | 查看栈局部变量的值                                 |
| list (或 l)         | 列出源代码, 接着上次的位置往下列, 每次列 10 行     |
| list 行号           | 列出从第几行开始的源代码                           |
| list 函数名         | 列出某个函数的源代码                               |
| next (或 n)         | 执行下一行语句                                     |
| print (或 p)        | 打印表达式, 通过表达式可以修改变量的值或者调用函数 |
| quit (或 q)         | 推出 gdb 调试环境                                  |
| set var             | 修改变量的值                                       |
| start               | 开始执行程序, 停在 main 函数的第一行前面等待命令   |
| step （或 s)        | 执行下一行语句, 如果有函数调用则进入到函数中       |

## gdb 基本命令 2

| 命令                       | 描述                                     |
| -------------------------- | ---------------------------------------- |
| break (或 b) 行号          | 在某一行设置断点                         |
| break 函数名               | 在某个函数开头设置断点                   |
| break ... if ...           | 设置条件断点                             |
| continue (或 c)            | 从当前位置开始连续运行程序               |
| delete breakpoints 断点号  | 删除断点                                 |
| display 变量名             | 跟踪查看某个变量, 每次停下来都显示它的值 |
| disable breakpoints 断点号 | 禁用断点                                 |
| enable 断点号              | 启用断点                                 |
| info (或 i) breakpoints    | 查看当前设置了哪些断点                   |
| run (或 r)                 | 从头开始连续运行程序                     |
| undisplay 跟踪显示号       | 取消跟踪显示                             |

## gdb 基本命令 3

| 命令                    | 描述                                           |
| ----------------------- | ---------------------------------------------- |
| watch                   | 设置观察点                                     |
| info (或 i) watchpoints | 查看当前设置了哪些观察点                       |
| x part1                 | 从某个位置开始打印储存单元的内容,              |
| x part2                 | 全部当作字节来看, 而不区分哪个字节属于哪个变量 |

## 整数的加减运算

### 2's complement 表示法

2's Complement 表示法规定：正数不变,负数先取反码再加 1.
如果 8 个 bit 采用 2's Complement 表示法,负数的取值范围是从 10000000 到 11111111（-128~-1）
,正数是从 00000000 到 01111111（0~127）,也可以根据最高位判断一个数是正是负,
并且 0 的表示是唯一的,目前绝大多数计算机都采用这种表示法.

### 判断溢出

在相加过程中最高位产生的进位和次高位产生的进位如果相同则没有溢出,
如果不同则表示有溢出.逻辑电路的实现可以把这两个进位连接到一个异或门,
把异或门的输出连接到溢出标志位.[链接](https://www.cnblogs.com/Jamesjiang/p/8947252.html)

## 浮点数

模型由三部分组成：符号位,指数部分(表示 2 的多少次方)和尾数部分(小数点前面是 0,尾数部分只表示小数点后的数字)

### 指数部分的正负号

使用偏移的指数(Biased Exponent).规定一个偏移值,比如 16,实际的指数要加上这个偏移值再填写到指数部分,
这样比 16 大的就表示正指数,比 16 小的就表示负指数

### 正规化(Normalize)

规定尾数部分的最高位必须是 1,也就是说尾数必须以 0.1 开头,对指数做相应的调整,这称为正规化(Normalize).
由于尾数部分的最高位必须是 1,这个 1 就不必保存了,可以节省出一位来用于提高精度,我们说最高位的 1 是隐含的(Implied)

## 汇编

### 寻址方式

内存寻址在指令中可以表示成如下的通用格式:
`ADDRESS_OR_OFFSET(%BASE_OR_OFFSET,%INDEX,MULTIPLIER)`
它所表示的地址可以这样计算出来:
`FINAL ADDRESS = ADDRESS_OR_OFFSET + BASE_OR_OFFSET + MULTIPLIER \* INDEX`

