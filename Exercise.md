### Exercise 1-3

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





