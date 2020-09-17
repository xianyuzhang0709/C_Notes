# Modulo%

```c
x % y
```

- If y completely divides x, the result of the expression is 0.
- If y is not completely divisible by x, then the result will be the remainder in the range [1, x-1].
- If x is 0, then [division by zero](https://www.geeksforgeeks.org/handling-the-divide-by-zero-exception-in-c/) is a [compile-time error](https://www.geeksforgeeks.org/difference-between-compile-time-errors-and-runtime-errors/).

1. The % operator cannot be applied to [floating-point numbers](https://www.geeksforgeeks.org/introduction-of-floating-point-representation/). xy必须是整数

2. The sign of the result for modulo operator is machine-dependent for negative operands, as the action takes as a result of underflow or overflow. 下溢还是上溢

```c
#include <stdio.h> 
int main(void) 
{ int x, y; 
	int result; 
	x = -3; 
	y = 4; 
	result = x % y; 
	printf("%d", result);           //-3

	x = 4; 
	y = -2; 
	result = x % y; 
	printf("\n%d", result);         //0

	x = -3; 
	y = -4; 
	result = x % y; 
	printf("\n%d", result);         //-3
	return 0; 
} 
```

**Note:** Some compilers may show the result of the expression as 1 and other may show -1. It depends on the [compiler](https://www.geeksforgeeks.org/introduction-of-compiler-design/).

结果的符号总是跟x相同。

