# The C programming language

> C程序新建步骤：visual studio c++ ==> 文件  ==> 新建  ==> (此时弹出新建窗口)文件 ==> c++ source file ==> 选择d盘，输入文件名(字母数字均可) ==> 确定。
>
> 主要再窗口左上角看，自己新建的文件是否以`.cpp`为后缀。如果是，则新建c文件成功。否则，请重新建立。

一个程序：

* 每一个c程序都必须有一个`main`函数（或称为方法），它是程序的主方法，程序从main方法开始执行。

* 所有在main函数中被使用的方法和变量会被执行，没有被main函数使用的，则不执行。

* C程序文件，以`.c`为后缀。文件在编译之后才可以运行。每一次修改程序后：点击**保存 -> 编译 -> 执行**。

* 一个c程序的例子：

  * ```c
    //文件: c11.c
    #include <stdio.h>
    void main(){
      int r;
      float s;
      printf("please input a number:");
      scanf("%d",&r);
    }
    ```

  * 头文件
  * 函数结构
  * 数据类型
  * I/O
  * 一个包含main函数和其他函数的程序例子，请参考书上p.14页的例2-1，看自己是否能懂每一句代码。

#### 头文件：

上述的`scanf`和`printf`方法，并不内建于c语言之中，而是包含在一个叫standard input/output的库文件当中。我们可以在程序第一行写入`#include <stdio.h>`来调用它。h = header file —— 头文件用于程序的预处理。

#### 函数结构：

```c
类型 函数名 (参数列表){
//---函数体---//
  声明；
  ....
  操作语句;   //--> 每一行表达语句，都需要用封号(;)结尾。
  ....
  return语句; //函数到这里结束，写在return语句后面的语句，都不会被执行。
//---函数体---//
}
```

#### 数据类型： **(p.25)**

1. **整型** 
   1. **int**
   2. short
   3. long
   4. unsigned int
   5. unsigned short
   6. unsigned long
2. **实数类型**: 
   1. float 单精度
   2. **double 双精度**
   3. long double 长双精度

3. **字符型 char** **（p.27)** 
   1. 占一个字节（即8比特）
   2. 每一个字符，其实是被以ascii码的数值，存放在存储单元中的。例如，字符‘a'，实际上是以97被存储下来的。(**其他数值，请参考附录二：ascii码对照表**)
   3. 字符型在输出时，即可以输出整型数值，也可以输出字符本身。

* 学习的核心：
  * 了解每种类型，思考其存在的意义；
  * 了解其取值范围。在编程过程中，很可能出现「你在赋值过程中，赋予了超出变量范围的值，系统会报错」。
  * 了解它们在`scanf，printf`等方法中被调用的方式。

4. 常量

   1. 常量 **(p.21)** 是指，在程序运行中，值会保持不变的量。

      1. 整型
      2. 实型
      3. 字符常量
      4. 字符串常量

   2. 我们用**符号常量**来存储我们要使用的常量。

      1. 符号常量跟变量很类似，惟一的区别是，它一经定义(赋值) 则不会被改变。而变量始终可以被赋值(被改变）。
      2. 符号常量的定义：

      ```c
      #define PI 3.1415926
      #define MYNAME "zhang"
      #define SUN 3
      ```

5. 变量
   1. 变量在程序中，相当于一个容器，用来存储相应的值。
      1. 使用变量前，要先声明变量：`int a`;
      2. 然后，对变量进行赋值：`int a = 3;`  赋值过程就是存值的过程。
      3. 变量名要有意义。
   2. 变量在定义时，必须说明其数据类型。可使用的数据类型，如上所述。

#### I/O - 1

`scanf("格式串",&变量1,&变量2,...)`                              注意：scanf 需要用取地址符

`printf("格式串",表达式1/变量1,表达式2/变量2,...) `                printf 却不需要

* `&`是**取地址符**，为表达式提供变量的地址。

* `%`是**占位符**。**(p.38 )**
  * **格式符**和占位符之间可以加修饰符 **（p.39）**
    1. `%.3f`表示输出一个浮点数，精确到小数点后3位
    2. `%4.3f`表示输出一个浮点数，占4个数据宽度（用于右对齐），精确到小数点后3位
    3. `%-4.3f`表示输出一个浮点数，占4个数据宽度（向左对齐），精确到小数点后3位
* **转义符**，用于在字符串语句中提供特殊的含义。**(p.23)**

| 格式符     | 含义           |
| ---------- | -------------- |
| %c         | character 字符 |
| %d         | decimal 十进制 |
| %f         | float          |
| %lf        | double float   |
| **转义符** | **含义**       |
| \n         | New line 换行  |
| \t         | Tab            |
| \\\        | \本身          |

#### I/O - 2

（p.40）`getchar()` `putchar()`也是输入输出语句，只不过，它们只输入输出一个字符。

#### 表达式和操作符

1. 基本的算数运算符：

   `+  -  *  /  %`

   * `/` ：注意，除法有**整数除法**和**实数除法**之分。
   * `%` ：求余  eg：`a = 15%7;`  a得到的值为1。

2. 自增、自减运算符

   `++    --`

   * `a++`   `a--`  
   * `++a`   `--a`

3. 算术表达式 —— 符号优先级

   1. a+b
   2. ++i
   3. (++i) - (j++)
   4. (a * 3) / b

4. 强制转换

   eg: `  (int)(x+y);` ` (float)a;`

   ```c
   void main(){
     float x = 3.2, y = 1.0;
     int a = 10;
     printf("%d, %f", (int)(x+y), (float)a);
   }
   ```

5. 赋值

   `a = a+b;`可以缩写为`a += b;` 

# 作业：

1. 第二章习题第7题。
   * 先自己得出表达式结果，再写程序测试。

2. p41 例 3-3：从键盘输入小写字母，用大写字母输出。
   * 要求：使用putchar()输出结果。
3. 例 3-5：练习敲一遍，读懂代码。
4. 第三章习题。第6题不需要做，读懂例3-4更好。

# 第4+5章

### 关系式：

1. 关系运算符：

   `>  <   ==  !=  <=  >=`

2. 关系表达式：

   `a+b > c-d` --->  关系表达式会输出一个结果：0或1  

   * 0表示错误，1表示正确

3. 逻辑运算符：

   `||或   &&且   !非`

   **优先级**：**或/且** < 关系运算符 < **非**

   或：一边为真，则结果为真 --> 1

   且：两边均为真，则结果为真 --> 1

   非：表达式为真，则结果为假 --> 0

   > 那么，请问：`-1||0`的结果是什么？请写程序测试。

4. 条件表达式：`?:`  (三元操作符)

   `判断条件? 表达式1:表达式2`

   如果判断的结果为真，则输出表达式1的值，否则输出表达式2的值。

### 条件判断：if语句和switch语句

```c
if(条件判断语句){
	执行语句;
}
else
{
  执行语句;
}
```

* **理解和练习：例4-2，4-3， 4-4，4-5**

```c
switch(表达式){         
  case 常量或常量表达式1:   //case之后不需要{},
      执行语句1/空语句;     //这里可以有多条语句
    	执行语句111/空语句; 
    	......
  case 常量或常量表达式2:
      执行语句2/空语句;
  case 常量或常量表达式3:
      执行语句3/空语句;
    ......
    ......
    default:  //default语句模块，可以省略
    	执行语句n/空语句；
}

//break 和 continue  p.78
//switch一旦匹配到合适的case，就会执行case和它之后的所有语句。所以我们需要使用`break`来跳出switch语句模块。
```

* **理解和练习：例4-7(课上讲)，4-8至4-12：有些题是对前面题目的优化，注意理解它们的区别。**

  已完全理解的题目，可以不需要再敲一遍。

### 循环执行：while循环，do-while循环，for循环

```c
while(条件){
	执行语句;
}

do{
  执行语句;
}while(条件)
  
for(初始化;条件判断;自增/自减){
  执行语句;
}

//break: 跳出循环。执行循环体后面的语句。
//continue：结束本次循环，进入下一次循环
```

# 第6章 数组

**数组**是由相同类型的元素所构成的集合，由一块连续的内存来存储其值。

* 数组一旦定义，长度就固定不变。

```c
int a[20];
char str[5];

//引用：数组的下标从0开始，到其长度-1
a[0],a[10],a[19]     //没有a[20]
  
//赋值：
a[0] = 1;
a[10] = 3;
a[3] = a[0]+a[10];    
//-->下标可以是一个整型数值(如上所示)、或一个整型表达式、或一个整型变量
int i = 3; 
a[i];  //整型变量
a[i+3];//整型表达式

//数组初始化1：声明时初始化
int a[5] = {1,3,7,8,9};  //这种情况时，可以省略数组长度：int a[] = {1,3,7,8,9}; 

//数组初始化2：声明后初始化 -->注意：数组声明之后，只能用for循环做初始化，不能用集合赋值
int a[5], i;
for(i=0;i<10;i++){
  a[i] = i;
}
//结果：数组a里的值为：{0,1,2,3,4,5,6,7,8,9}
```

1. 数组初始化时，**如果赋值个数 < 数组长度**，则部分赋值。剩余部分，根据数组类型，以默认值进行赋值——int的默认值为0，char的默认值为'\\0' (字符串的结束标志)。

2. **如果赋值个数 > 数组长度**，会报错。

### 二维数组

```c
//声明
int a[2][4];  //声明了一个2行4列的二维数组a，数据类型为int

//初始化1:声明时初始化
int a[][] = {{1,2,3,4},{2,2,3,4}};

//初始化2: 两个for循环嵌套赋值
for(int i=0;i<=2;i++){
  for(int j=0;j<=4;i++){
  	a[i][j] = 1;   //把数组的每一个元素都赋值为1
	}
}

//初始化3：特殊操作1
int a[2][4] = {1,2,3,4,2,2,3,4};  //系统会自动按行进行赋值
int a[ ][4] = {1,2,3,4,2,2,3,4};  //有列下标时，行下标可省(了解即可，不建议学习这种懒惰的行为)
//初始化3：特殊操作2，部分赋值
int a[2][4] = {{1}{2}};           //为每行的第一个元素赋值，即a[0][0]=1，a[1][0]=2；
```

### 字符数组



# 课堂练习tips:

Ctrl + c/v  复制粘贴

按住shift可以多选

tab相当于4个空格的长度，用于对齐格式非常方便

# 课程安排

| 学时   | 作业        |
| ------ | ----------- |
| 3，4   | 第四章      |
| 5，6   | 第五章      |
| 7，8   | 第六章 数组 |
| 9，10  | 第七章 函数 |
| 11，12 | 练习        |
| 13，14 | 练习/测验一 |
| 15，16 | 测验二      |

