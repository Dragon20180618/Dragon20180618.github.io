# 求出数组指定范围内，子序列最大和

（考虑负数）

```c
#include<stdio.h>
int Must (int a[],int i,int j)
{
    int sum = 0;
    int must = a[i];
	for(; i <= j; i++)
		{
            sum += a[i];
            if(sum>must)
                must=sum;
            if(sum<0)
                sum=0;
        }
	return must;
}
int main()
{
    int a[5]={-1,2,3,4,-1};
    printf("%d", Must(a,0,4));
    return 0;
}
```

 <h4>sum作为临时储存点。</h4>

<h4>must是当前最大和。</h4>

<h4>点睛之笔是sum置零。</h4>

<h4>该算法时间复杂度为O(n)</h4>