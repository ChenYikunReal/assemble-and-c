# 汇编语言与C语言

![汇编语言](/汇编语言.jpg)

- 汇编语言调用C语言
- C语言调用汇编语言

`gcc hello.s -o hello`

[学习网址](https://gcc.gnu.org/onlinedocs/gcc/Using-Assembly-Language-with-C.html)

## C语言调用汇编语言代码示例

Demo1：
```c
#include <stdio.h>

// 将src复制到dst，为dst加1
int main() {
    int src = 1;
    int dst;
    asm ("mov %1, %0\n\t"
         "add $1, %0"
         : "=r" (dst)
         : "r" (src));
    printf("%d\n", dst);
    return 0;
}
```

Demo2：
```c
#include <stdio.h>

// (xa+xb)*2的计算 答案为16
int main() {
    int xa = 6, xb = 2, result;
    asm volatile (
            "add %%ebx, %%eax\n\t"
            "movl $2,%%ecx\n\t"
            "mul %%ecx\n\t"
            "movl %%eax,%%edx"
            :"=d"(result):"a"(xa),"b"(xb):"%ecx");
    printf("%d\n", result);
    return 0;
}
```
