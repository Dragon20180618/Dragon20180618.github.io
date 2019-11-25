# Fibonacci

```c
#include<stdio.h>
int fibonacci(int n)
{
    int f1=1;
    int f2=1;
    int f3=f1+f2;
    if(n<3){
        return 1;
    }
    n-=3;
    while(n){
        n--;
        f1=f2;
        f2=f3;
        f3=f1+f2;
    }
    return f3;
}
int main()
{
    int n;
    printf("Input the day : ");
    scanf("%d",&n);
    printf("\n\nThe quantity of lovely Cow(s): %d\n",fibonacci(n));
}
```

**每只小牛第两次循环开始繁殖，所以从本回合向前两回合则是该回合应该繁殖的牛数。**

> 特别注明，不考虑雌雄的问题