##### 赋值语句在判断语句中：

```c
while(y=3-4){...}
if(y=3-4){...}
```

编译之后会产生一个**warning**: using the result of an assignment as a condition without parentheses [-Wparentheses]

增加括号后不报错：

```c
while((y=3-4)){...}  //等同于：y=-1; while(1){...}    //while一直执行
if((y=3-4)){...}     //if成立，执行
```

##### 赋值语句还可以在输出语句中：

```c
printf{"%d",y=3>4};  //0
printf{"%d",y=3,y+5,y++};  //3  有warning: data argument not used by format string 和 unsequenced modification and access to 'y'   但还是可以输出结果
```

**逗号表达式**：逐个执行，输出最后一个表达式的值。

