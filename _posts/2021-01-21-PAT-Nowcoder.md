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

<img src="https://i.loli.net/2021/01/21/eztPJj8yNwoDQIv.png" alt="image-20210121152334331"  />

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

<img src="https://i.loli.net/2021/01/21/F8HRbtjJk4aqoIP.png" alt="image-20210121160101970" style="width:705px;" />

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

<img src="https://i.loli.net/2021/01/21/FIGvMHb6ydf3zKa.png" alt="image-20210121160215822" style="width:705px;" />

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

### 1004：福尔摩斯的约会

<img src="https://i.loli.net/2021/01/21/pjgqGLIHJr2fO8E.png" alt="image-20210121160339749" style="width:705px;" />