---
layout: post
title: PAT-牛客网-乙级真题
categories: PAT
description: PAT-牛客网-乙级真题
keywords: C
topmost: false
---

> https://www.nowcoder.com/pat/6/problems

### 1001：A+B和C

**题目描述：**

> 给定区间[-2的31次方, 2的31次方]内的3个整数A、B和C，请判断A+B是否大于C。

~~~c
//
// Created by Jiaolong on 2021/1/21.
//

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



### 1002：数字分类

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

~~~c
//
// Created by Jiaolong on 2021/1/21.
//

#include <stdio.h>

int main() {
    int a[1000] = {0};
    int n, b, c, i, A1 = 0, A2 = 0, A3 = 0, A4 = 0, A5 = 0, ch = 0;
    float avg = 0.0,a4num = 0.0;
    while (~scanf("%d", &n)) {
        for (i = 0; i < n; ++i) {
            scanf("%d", &a[i]);
        }
        for (int j = 0; j < n; ++j) {
            //A1
            if (a[j] % 5 == 0) {
                if (a[j] % 2 == 0) {
                    A1 += a[j];
                }
            }

            //A2
            if (a[j] % 5 == 1) {
                if (ch == 0) {
                    A2 = a[j];
                    ch++;
                } else {
                    if (ch % 2 == 0) {
                        A2 += a[j];
                    } else {
                        A2 -= a[j];
                    }
                    ch++;
                }

            }

            //A3
            if (a[j] % 5 == 2) {
                A3++;
            }

            //A4
            if (a[j] % 5 == 3) {
                a4num++;
                A4 += a[j];
                avg = (A4 / a4num);
            }

            //A5
            if (a[j] % 5 == 4) {
                if (a[j] > A5) {
                    A5 = a[j];
                }
            }

        }

        if(A1!=0)
            printf("%d ",A1);
        else
            printf("N ");
        if(A2!=0)
            printf("%d ",A2);
        else
            printf("N ");
        if(A3!=0)
            printf("%d ",A3);
        else
            printf("N ");
        if(A4!=0)
            printf("%.1f ",avg);
        else
            printf("N ");
        if(A5!=0)
            printf("%d",A5);
        else
            printf("N");
        return 0;

    }
}
~~~

### 1003：数素数

<img src="https://i.loli.net/2021/01/21/3yVFYMjG6T9W8XI.png" alt="image-20210121144531091" style="zoom:90%;" />

~~~c
//
// Created by Jiaolong on 2021/1/21.
//

#include<stdio.h>
#include<math.h>

int judge(int num) {
    int k = (int) sqrt((double) num);
    for (int i = 2; i <= k; i++) {
        if (num % i == 0) {
            return 0;
        }
    }
    return 1;
}

int main() {
    int arr[10000];
    int sign = 0;
    int a = 0;
    int i = 2;
    while (sign <= 10000) {
        if (judge(i) == 1) {
            arr[sign] = i;
            sign++;
        }
        i++;
    }
    int m, n;
    scanf("%d %d", &m, &n);
    for (int i = m - 1; i <= n - 1; i++) {

        if (i == n - 1) {
            printf("%d", arr[i]);
        } else {
            printf("%d ", arr[i]);
        }

        a++;
        if (a == 10) {
            printf("\n");
            a = 0;
        }
    }
}
~~~

