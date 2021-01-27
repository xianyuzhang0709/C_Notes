### Exercise 3.03

For each of the following pairs of `scanf` format strings, indicate whether or not the two strings are equivalent. If they're not, show how they can be distinguished.

```
(a) "%d"       versus " %d"
(b) "%d-%d-%d" versus "%d -%d -%d"
(c) "%f"       versus "%f "
(d) "%f,%f"    versus "%f, %f"
```

### Solution

(a) - equivalent. 二者等价。

* "%d" - 开始时读取并跳过/忽略0或多个空白字符，然后读取一个int整数（如果遇到的是不可能的符号，则直接结束，把该字符放回原处），结束。
* " %d" - 会读取并跳过0或多个空白字符，直到读取到一个非空白字符并将其放回原处，然后读取一个int整数（如果遇到的是不可能的符号，则直接结束，把该字符放回原处），结束。

(b) - equivalent. 二者等价。

* 对于format string（格式串）中的空白字符，scanf函数所采取的措施都是：在此处开始读取0或多个空白字符并忽略掉（丢掉不理），直到遇到一个非空白字符的符号，然后将其放回。接着读取下一个'-'，匹配成功，则继续读取下一个int整数。

(c) - different. 不等价。

* (c) is not equivalent because the trailing space will require the user to input a non-whitespace character at the end of the input signifying the end of the whitespace sequence matched by the space. (表示由空格匹配的空白序列的结尾。)
* scanf的格式串如果以空白字符结束，那么它会在用户在输入结束后（回车之后）一直挂起，直到等待用户输入一个非空白字符，才能确认格式串中的' '匹配结束，并将用户输出的非空白字符放回原处，留给下一次输入函数读取。

(d) - equivalent. 二者等价。

* white-space characters in format string match **ANY** number of white-space characters in the input string (including none).

### - Review Notes -

> **C**标准中**空白字符**有：空格（' '）、换页（'\f'）、换行（'\n'）、回车（'\r'）、水平制表符（'\t'）、垂直制表符（'\v'）六个。

> 总结C语言中的scanf读取方式：
>
> * 格式串中包含 **转换说明（conversion specification）**和 **普通字符（ordinary characters）**
>
> 针对带%的conversion specification：
>
> 1. 在每一次匹配格式之前，scanf会 **跳过/忽略/读取后扔掉** 所有的空白字符，直到读取到非空白字符
>    1. 如果读取的是合理的字符，则匹配和存入。
>    2. 如果读取的是不可能的字符，则退出，把读取的字符放回，同剩下的字符一起留给后面的输入函数读取。
>
> 针对%之间的普通字符：
>
> 1. 空白字符，一个代表可以在此处匹配0或多个空白字符。
>    * scanf会 **读取&扔掉** 这些空白字符，直到读取到非空白字符，并放回原处。交给下面的步骤处理。
> 2. 非空白字符，则严格按照一对一匹配的方式进行匹配。
>    * 匹配成功，则进入下面的步骤。
>    * 匹配失败，则退出，将读取的字符放回，同剩下的字符一起留给后面的输入函数读取。

### Exercise 3.04

Suppose that we call `scanf` as follows:

```
scanf("%d%f%d", &i, &x, &j);
```

If the user enters

```
10.3 5 6
```

what will be the values of `i`, `x` and `j` after the call? (Assume that `i` and `j` are `int` variables and `x` is a `float` variable.)

### Solution

```
i = 10
x = 0.3
j = 5
```

The decimal point will end the input for `i` and begin `x`, and the next input, 5, will be assigned to `j`.

> `10.3 5 6`
>
> 为%d读取：`1` `0` `.` —— `.` 不可能是int类型数字中存在的字符，所以把`.`放回，把10存入i。
>
> `.3 5 6`
>
> 为%f读取：`.` `3` ` ` —— 空格不可能是float或double类型中存在的字符，所以把空格放回，把0.3存入x。
>
> `_5 6` （为了方便显示，这里用_代替空格）
>
> 为%d读取：` ` —— 空格读取并丢掉。`5` ` ` —— 空格不可能是int类型中存在的字符，把空格放回，把5存入j。结束。
>
> `_6`