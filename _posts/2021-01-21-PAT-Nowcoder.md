---
layout: post
title: PAT-牛客网-乙级真题
categories: PAT
description: PAT-牛客网-乙级真题
keywords: C
topmost: false
---

> https://www.nowcoder.com/pat/6/problems

### [1001：A+B和C](https://www.nowcoder.com/pat/6/problem/4077)

**题目描述：**

> 给定区间[-2的31次方, 2的31次方]内的3个整数A、B和C，请判断A+B是否大于C。

~~~c
#include <stdio.h>

int main() {
    long long a, b, c,i,j;
    while(~scanf("%lld",&i)){
        for(j=1;j<=i;j++){
            scanf("%lld %lld %lld",&a,&b,&c);
            printf("Case #%lld: %s\n",j, (a+b>c)? "true":"false");
        }
    }
}

~~~

> 因long类型只能表示到2^31-1，故要使用long long 类型表示



### [1002：数字分类](https://www.nowcoder.com/pat/6/problem/4078)

**题目描述：**

> 给定一系列正整数，请按要求对数字进行分类，并输出以下5个数字：
>
> 
>
>  A1 = 能被5整除的数字中所有偶数的和；
>
>  A2 = 将被5除后余1的数字按给出顺序进行交错求和，即计算n1-n2+n3-n4...；
>
>  A3 = 被5除后余2的数字的个数；
>
>  A4 = 被5除后余3的数字的平均数，精确到小数点后1位；
>
>  A5 = 被5除后余4的数字中最大数字。

~~~C
#include <stdio.h>
int main(){
    int a[1000]={0};
    int n,b,c,i,A1=0,A2=0,A3=0,A4=0,A5=0;
    while (~scanf("%d"),&n){
        for(i=0;i<=a;i++){
            scanf("%d",&a[i]);
        }
        for (int j = 0; j <= n; j++) {
            //A1
            if(a[j]%5==0){
                if(a[j]%2==0){
                    A1+=a[j];
                }
            }
        }
    }
}
~~~

