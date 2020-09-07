### Exercise 1-3: 华氏温度—>摄氏温度

```c
#include <stdio.h>
int main(){
    float hua, she;
    int low = 0,
        up = 300,
        step = 20;
    hua = low;
    printf("Hua to She Table\n");
    while(hua <= up){
        she = (5.0/9.0) * (hua - 32.0);
        printf("%3.0f\t%6.1f\n",hua,she);
        hua += step;
    } 
}
```

Output: 

```bash
Hua to She Table
  0      -17.8
 20       -6.7
 40        4.4
 60       15.6
 80       26.7
100       37.8
120       48.9
140       60.0
160       71.1
180       82.2
200       93.3
220      104.4
240      115.6
260      126.7
280      137.8
300      148.9
```

Notes: 

1. `main`函数名，前面是int。
2. 如果是整数除法，要先（hua-32)✖️5再➗9。因为如果直接(5/9)(F-32)，整数除法5/9=0，结果全是0；而如果是float，就可以(5/9)(F-32)，但要注意：
   * 是(5.0/9.0)
   * 是(F-32.0)，虽然这里会自动转换，但写成32.0便于阅读代码
   * printf("%3.0f....") 这里不再是d，而是f
     * %表其他参数（第二个参数，第三个参数……）
     * d表示decimal；
     * f表示float；
     * 3表示数字宽；
     * .0表示小数点后保留几位。

### Exercise 1-6: Test the value of `getchar()!=EOF`, 0 or 1?

```c
#include <stdio.h>
int main(){
    printf("getchar() != EOF --> %d\n", getchar() != EOF);
}
```

Output:

```bash
s
getchar() != EOF --> 1
//Ctrl+D -- Mac的EOF
getchar() != EOF --> 0
```

Notes: 

1. `getchar()`只要用一次，就会引起一次terminal输入；
2. `putchar()`可以像printf那么用，直接输出一个字符。本题输出的是0或1，所以可以用putchar而不是printf。

犯的错误：

```c
#include <stdio.h>
int main(){
    int c;
    while(c = getchar()!=EOF){//把赋值当做条件 --> 编译warning
        putchar(c);
    }
}
```

### Exercise 1-7: print the value of EOF

```c
#include <stdio.h>
int main(){
    printf("%d\n",EOF);  //-1
}
```

### Exercise 1-8: 

```c
#include <stdio.h>
int main(){
    int c, space, tab, nl;
    space = tab = nl = 0;
    while(getchar()!=EOF){
        if(c=='\t'){
            ++tab;
        }
        if(c=='\n'){
            ++nl;
        }
        if(c==' '){
            ++space;
        }
    }
    printf("There are %d spaces, %d tabs and %d newlines.\n", space, tab, nl);
}
```

结果全是0.

### Exercise 1.6

```c
#include <stdio.h>
// #include <math.h>
int main(){
    int c,i,nwhite,nother;
    int ndigit[10];

    nwhite = nother = 0;
    for(i=0;i<10;i++){
        ndigit[i]=0;
    }

    while((c=getchar())!=EOF){
        if(c>='0'&&c<='9'){
            ndigit[c-'0']++;
            printf("%d",c-'0');
        }
        else if(c==' '||c=='\n'||c=='\t'){
            nwhite++;
        }
        else{
            nother++;
        }
    }
    printf("digits=");
    for(i=0;i<10;i++){
        printf(" %d",ndigit[i]);
    }
    printf(", white space = %d, other = %d\n", nwhite, nother);
}
//输入本程序全文，得：
//digits= 10 3 0 0 0 0 0 0 0 1, white space = 207, other = 363
```



