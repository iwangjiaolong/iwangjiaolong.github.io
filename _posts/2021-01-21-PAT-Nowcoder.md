---
layout: post
title: PAT-牛客网-乙级真题
categories: PAT
description: PAT-牛客网-乙级真题
keywords: C
topmost: false
---

> **链接：**[PAT乙级(Basic Level)真题](https://www.nowcoder.com/pat/6/problems)

# 1001：A+B和C

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



# 1002：数字分类

<img src="https://i.loli.net/2021/01/21/F8HRbtjJk4aqoIP.png" alt="image-20210121160101970" style="zoom:;" />

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

# 1003：数素数

<img src="https://i.loli.net/2021/01/21/FIGvMHb6ydf3zKa.png" alt="image-20210121160215822" style="zoom:;" />

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

<img src="https://i.loli.net/2021/01/21/pjgqGLIHJr2fO8E.png" alt="image-20210121160339749" style="zoom:;" />

~~~c
//
// Created by Jiaolong on 2021/1/21.
//

#include<stdio.h>
#include<string.h>

int main() {
    char arr1[60], arr2[60], arr3[60], arr4[60];
    int k1, k2, k3, k4, i, j, flag = 0, num;
    scanf("%s %s %s %s", arr1, arr2, arr3, arr4);
    k1 = strlen(arr1);
    k2 = strlen(arr2);
    k3 = strlen(arr3);
    k4 = strlen(arr4);

    for (int i = 0; i < (k1 < k2 ? k1 : k2); i++) {
        if (arr1[i] == arr2[i]) {
            if (flag == 0 && arr1[i] >= 'A' && arr1[i] <= 'G') {
                switch (arr1[i]) {
                    case 'A':
                        printf("MON ");
                        break;
                    case 'B':
                        printf("TUE ");
                        break;
                    case 'C':
                        printf("WED ");
                        break;
                    case 'D':
                        printf("THU ");
                        break;
                    case 'E':
                        printf("FRI ");
                        break;
                    case 'F':
                        printf("SAT ");
                        break;
                    case 'G':
                        printf("SUN ");
                        break;
                }
                flag++;
                continue;
            }

            if (flag == 1) {
                if (arr1[i] >= '0' && arr1[i] <= '9') {
                    printf("0%c:", arr1[i]);
                }
                if (arr1[i] >= 'A' && arr1[i] <= 'N') {
                    num = arr1[i] - 65 + 10;
                    printf("%d:", num);
                }
                flag++;
            }
        }
    }

    for (int j = 0; j < (k3 < k4 ? k3 : k4); j++) {
        if (arr3[j] == arr4[j]) {
            if ((arr3[j] >= 'a' && arr3[j] <= 'z') || (arr3[j] >= 'A' && arr3[j] <= 'Z')) {
                if (j < 10) {
                    printf("0%d", j);
                } else {
                    printf("%d", j);
                }
                break;
            }
        }
    }


    return 0;
}
~~~

# 1005：德才论

![image-20210121202329659](https://i.loli.net/2021/01/21/CWZXld8HEBT6eFr.png)