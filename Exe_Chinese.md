C的类型：

整数型：

int, short, long, unsigned, unsigned short, unsigned long

16,16, 16, 16, 32, 32

实数型：

Float32, double64, long double128





### Chapter 1 一百以内素数

```c
#include <stdio.h>
int main(){
    for (int i = 1; i<=100; i++){
        int j = 1;
        int c = 0;
        for(j = 2; j<i; j++){
            if(i%j == 0){
                c++;
            }
        }
        if(c==0){
            printf("%d,",i);
        }
    }
}
//1,2,3,5,7,11,13,17,19,23,29,31,37,41,43,47,53,59,61,67,71,73,79,83,89,97,
```

素数的方法是：`m取值：[2, sqrt(n)]`, 如果有`n%m == 0`, 则不是素数，否则就是素数。

### Chapter 2: 求算术表达式结果

```c
#include <stdio.h>
int main(){
    int a = 2, b = 3;
    float x = 5.5, y = 4.4;
    printf("%.1f\n", x+a%3*(int)(x+y)%2/4);
    printf("%.1f\n", (float)(a+b)/2+(int)x%(int)y);
}
//5.5 = 5.5+1*9%2/4 = 5.5+0
//3.5 = 2.5+5%4 = 3.5
```

### Chapter 3-4: 计算三角形面积

```c
#include <stdio.h>
#include <math.h>
int main(){
    int a,b,c;
    printf("please input 3 numbers of the SANJiaoXing:\n");
    scanf("%d,%d,%d",&a,&b,&c);
    double area, s;
    s = (a+b+c)/2;
    area = sqrt(s*(s-a)*(s-b)*(s-c));
    printf("the result is %lf.\n", area);
}
//3,4,5 --> 6.000000
```

本例：abcs area 均可设置为float，最终输出结果，也%f。结果会输出小数点会两位。



```c
#include <stdio.h>
// #include <math.h>
int main(){
    int x=7;
    x=x++;
    printf("%d\n", x);//7  因为x自加，并返回原值，赋值给自己。所以x=7。
    
    x-=x+x;
    printf("%d\n", x);//先算了x+x,所以输出是-7
  
    x+=x-=x;
		printf("%d\n", x);//0
  
  	x+=x-=x+x;
    printf("%d\n", x);//-2x=-14,如果把最后一个x换成1,3,结果是-2,-6
    //
}
```

暂时的理解是：

1. 右向左结合。`x+x`先计算，=14。
2. `x-=14`, 即`x=x-14`，`x`变成-7。
3. 剩下的式子是`x=x+(x)`，x=-7+-7 = -14。

### Chapter 4-7: switch

```c
#include <stdio.h>
// #include <math.h>
int main(){
    float a,b;
    char c;
    printf("input:\n");
    scanf("%f,%c,%f",&a,&c,&b);
    switch(c){
        case '+':
            printf("%f",a+b);
            break;
        case '-':
            printf("%f",a-b);
            break;
        case '*':
            printf("%f",a*b);
            break;
        case '/':
            printf("%f",a/b);
            break;
        default:
            printf("your input is wrong.");
    }
}
//3,*,6 --> 18.000000
```

本题遇到的问题：

1. mac端输入，不能用空格做分隔符，必须是逗号。

2. exercise1.6 也是，mac的输入端处理，跟windows诸多不同。比如回车，空格，EOF。mac的float后6位小数点。double也是6位小数。double是%LF。
3. switch注意：
   1. switch的条件句，是一个运算，求出结果
   2. case是数值或者char，跟上面的结果匹配。注意case后面不加花括号，记得break。
4. 本题：abc，ab是float，c是char。直接输出即可，不需要变量来接受计算结果。

### chapter 4-12

```c
#include <stdio.h>
// #include <math.h>
int main(){
    int s;
    printf("please input your score:\n");
    scanf("%d",&s);
    switch(s/10){         //1.注意这里的技巧，score除以10，得出数值，可以用switch
        case 10:
        case 9:
            printf("A");
        case 8:
            printf("B");
        case 7:
            printf("C");
        case 6:
            printf("D");
      case 5:              //2.这部分可以用default代替。
        case 4:
        case 3:
        case 2:
        case 1:
        case 0:
            printf("E");
    }
}
```

### Chapter5-3: 计算圆周率

```c
#include <stdio.h>
#include <math.h>
int main(){
    float ans = 1.0;
    int n = 3, f = 0;
    while(fabs(1.0/n)>=1e-6){
        if(f == 1){
            ans += 1.0/n;
            n += 2;
            f = 0;
        }else{
            ans -= 1.0/n;
            n += 2;
            f = 1;
        }
    }
    printf("Pi = %f",ans * 4); 
}
```

出现过很多细节错误。

1. 比如while条件里要写，满足sm条件时运行，我却写了结束循环的条件。
2. 第一个数从3开始，符号为负。测试多次才慢慢靠近正确答案。不是一开始就对。
3. 本程序可以从1开始。`n=1,f=1`即可。
4. abs在c中，是fabs()。
5. 程序不够简洁，借鉴一下书上的做法：

```c
#include <stdio.h>
#include <math.h>
int main(){
    float ans = 0, t = 1.0;
    int n = 1, f = 1;
    while(fabs(t)>=1e-6){
        ans += t;
        n += 2;
        f = -f;
        t = f * 1.0/n;
    }
    printf("Pi = %f\n",ans * 4); 
}
//引入t作为最后一项的值。判断t，累加t，然后改变f正负，改变t为带符号的最后项。循环。
```

### Chapter 5-6 水仙花数

```c
#include <stdio.h>
#include <math.h>
int main(){
    int n = 100;
    do{
        int bit1 = n%10;
        int bit10 = n/10%10;
        int bit100 = n/100;
        if(pow(bit1,3)+pow(bit10,3)+pow(bit100,3)==n){
            printf("%d, ", n);
        }
        n++;
    }while(n<=999);
}
```

### Chapter 5-10: 三角形

```c
#include <stdio.h>
#include <math.h>
int main(){
    int l;
    printf("input a number");
    scanf("%d",&l);
    int i,j;
    for(i=1;i<=l;i++){
        for(j=1;j<=i;j++){
            printf("%d",j);
        }
      	//此时j=？     答案是  n+1。
        for(;j>2;j--){        
            printf("%d",j-2);  //所以这里要-2，j的循环要-3
        }
        printf("\n");
    }
}
//输出：
1
121
12321
1234321
123454321
12345654321
1234567654321
```

### chapter 5-13: 小球100米下落10次

```c
#include <stdio.h>
int main(){
    float sum = 100, t = 50;
    for(int i=1; i<10;i++){
        sum += 2*t;
        t = t/2;
    }
    printf("%f, %f\n",sum, t);
}
//299.609375, 0.097656
```

### Chapter 5.2 角谷定理

```c
#include <stdio.h>
// #include <math.h>
int main(){
    int n;
    printf("input:");
    scanf("%d\n",&n);
    while(n!=1){
        if(n%2==0){
            n /= 2;
            printf("%d, ",n);
        }else{
            n = n * 3 + 1;
            printf("%d, ",n);
        }
    }
    printf("--> %d.",n);   
}
//28, 14, 7, 22, 11, 34, 17, 52, 26, 13, 40, 20, 10, 5, 16, 8, 4, 2, 1, --> 1.
//terminal输入时，需要EOF，才能结束输入。好坑啊日！！！
```









































### Exercise 1

```c
#include <stdio.h>
int main(){
    double v;
    printf("%d",scanf("%lf", &v));
}
//scanf("%lf", &v)的值为1，只要有数字传入。
//3或5 --> 1
//s --> 0
```

