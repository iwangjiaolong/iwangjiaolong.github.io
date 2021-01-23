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

/*
输入例子:
4
1 2 3
2 3 4
2147483647 0 2147483646
0 -2147483648 -2147483647
*/
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

/*
输入例子:
13 1 2 3 4 5 6 7 8 9 10 20 16 18
*/
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

/*
输入例子:
5 27
*/

~~~



# 1004：福尔摩斯的约会

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

/*
输入例子:
3485djDkxh4hhGE
2984akDfkkkkggEdsb
s&hgsfdk
d&Hyscvnm
*/
~~~



# 1005：德才论

![image-20210121202329659](https://i.loli.net/2021/01/21/CWZXld8HEBT6eFr.png)

~~~c
#include <stdlib.h>
#include <string.h>
#include <stdio.h>

int flag_node(int *p, int high, int low)
{
    if (p[1] < low || p[2] < low)
        return 0;          // 第五类
    else if (p[1] >= high && p[2] >= high)
        return 4;          // 第一类
    else if (p[1] >= high)
        return 3;          // 第二类
    else if (p[2] <= p[1])
        return 2;          // 第三类
    else
        return 1;          // 第四类
}

int comp(const void *a_t, const void *b_t)
{
    int *a = (int*)a_t, *b = (int*)b_t;
    int sum1 = a[1]+a[2], sum2 = b[1]+b[2];

    if (sum1 != sum2)      return sum2 - sum1; // 按总分排序
    else if (a[1] != b[1]) return b[1] - a[1]; // 总分相等时按德分排序
    else                   return a[0] - b[0]; // 德分相等时按学号排序
}

int main()
{
    int low, high, n, cs, tmp[3], cn[4] = {0};
    scanf("%d %d %d", &n, &low, &high);
    int a[4][n][3];

    for (int i = 0; i < n; i++) {
        scanf("%d %d %d", tmp, tmp+1, tmp+2);
        cs = flag_node(tmp, high, low); // 按题目要求分类
        if (cs) memcpy(a[cs-1][cn[cs-1]++], tmp, 3*sizeof(int)); //只记录前四类有用的数据
    }

    printf("%d\n", cn[0]+cn[1]+cn[2]+cn[3]); // 输出记录数据的份数
    for (int i = 3; i >= 0; i--) {
        qsort(a[i], cn[i], 3*sizeof(int), comp); // 对每一类排序
        for (int j = 0; j < cn[i]; j++) // 排序后直接输出
            printf("%d %d %d\n", a[i][j][0], a[i][j][1], a[i][j][2]);
    }

    return 0;
}

/*
输入例子:
14 60 80
10000001 64 90
10000002 90 60
10000011 85 80
10000003 85 80
10000004 80 85
10000005 82 77
10000006 83 76
10000007 90 78
10000008 75 79
10000009 59 90
10000010 88 45
10000012 80 100
10000013 90 99
10000014 66 60
*/
~~~





# 1006：部分A+B

![image-20210122113400180](https://i.loli.net/2021/01/22/IpOVyaF4Klumozb.png)

~~~c
//
// Created by Jiaolong on 2021/1/22.
//

#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int countsame(int a, char b) {
    int m = 0;
    char stringa[16] = {0};
//    itoa(a, stringa, 10);
    snprintf(stringa, 16, "%d", a);
    for (int i = 0; i < strlen(stringa); i++) {
        if (stringa[i] == b) {
            m++;
        }
    }
    return m;
}

int chartonum(int times, char num) {
    char a[16] = {0};
    for (int i = 0; i < times; i++) {
        a[i] = num;
    }
    return atoi(a);
}


int main() {
    int a, b, m, n, Pa, Pb;
    char Da, Db;
    char stringa[16] = {0}, stringb[16] = {0};
    scanf("%d %c %d %c", &a, &Da, &b, &Db);
    m = countsame(a, Da);
    n = countsame(b, Db);
    Pa = chartonum(m, Da);
    Pb = chartonum(n, Db);
    printf("%d", Pa + Pb);
    return 0;
}

/*
输入例子:
3862767 6 13530293 3
*/
~~~

> `itoa();`函数只在window下可使用，oj系统使用Linux进行编译，故会报错。应使用`snpring()`代替
>
> `int snprintf ( char * str, size_t size, const char * format, ... );`
>
> - **str** -- 目标字符串。
> - **size** -- 拷贝字节数(Bytes)。
> - **format** -- 格式化成字符串。
> - **...** -- 可变参数。



# 1007：A除以B

![image-20210122163719671](https://i.loli.net/2021/01/22/XnDzqWgdlBrZ7M2.png)

> 解题思路：手算除法

~~~c
//
// Created by Jiaolong on 2021/1/22.
//

#include <stdio.h>
#include <string.h>
int main(){
    char a[1001];
    int b;
    scanf("%s %d",&a,&b);
    int p,q,len;
    len=strlen(a);
    p=(a[0]-'0')/b;
    q=(a[0]-'0')%b;
    if(len==1||(len>1&&p!=0))
    printf("%d",p);
    for(int i = 1; i < len; i++) {
        p=(q*10+a[i]-'0')/b;
        printf("%d",p);
        q=(q*10+a[i]-'0')%b;
    }
    printf(" %d",q);
}

/*
输入例子:
123456789050987654321 7
*/
~~~



# 1008：锤子剪刀布

![image-20210122164644288](https://i.loli.net/2021/01/22/PbF2CJsV6wXpnaU.png)

~~~c
//
// Created by Jiaolong on 2021/1/22.
//

#include <stdio.h>

int ct1 = 0, jt1 = 0, bt1 = 0, win1 = 0, lose1 = 0, place1 = 0;
int ct2 = 0, jt2 = 0, bt2 = 0, win2 = 0, lose2 = 0, place2 = 0;

void judge(char a, char b) {
    if (a == 'C' && b == 'C') {
        place1++;
        place2++;
    }
    if (a == 'C' && b == 'J') {
        win1++;
        lose2++;
        ct1++;
    }
    if (a == 'C' && b == 'B') {
        lose1++;
        win2++;
        bt2++;
    }
    if (a == 'J' && b == 'C') {
        lose1++;
        win2++;
        ct2++;
    }
    if (a == 'J' && b == 'J') {
        place1++;
        place2++;
    }
    if (a == 'J' && b == 'B') {
        win1++;
        lose2++;
        jt1++;
    }
    if (a == 'B' && b == 'C') {
        win1++;
        lose2++;
        bt1++;
    }
    if (a == 'B' && b == 'J') {
        lose1++;
        win2++;
        jt2++;
    }
    if (a == 'B' && b == 'B') {
        place1++;
        place2++;
    }
}

char maxwin(int c, int j, int b) {
    int max = c;
    char maxc = 'C';
    if (j > max) {
        max = j;
        maxc = 'J';
    }
    if (b > max) {
        max = b;
        maxc = 'B';
    }

    if (c == j && c == max) {
        maxc = 'C';
    }
    if (c == b && c == max) {
        maxc = 'B';
    }
    if (b == j && b == max) {
        maxc = 'B';
    }


    return maxc;
}

int main() {
    int n;
    char a[105] = {0}, b[105] = {0};
    scanf("%d", &n);

    for (int i = 0; i < n; i++) {
        scanf(" %c %c", &a[i], &b[i]);
    }
    for (int j = 0; j < n; j++) {
        judge(a[j], b[j]);
    }

    printf("%d %d %d\n", win1, place1, lose1);
    printf("%d %d %d\n", win2, place2, lose2);
    printf("%c %c", maxwin(ct1, jt1, bt1), maxwin(ct2, jt2, bt2));

}

/*
输入例子:
10
C J
J B
C B
B B
B C
C C
C B
J B
B C
J J
*/
~~~







# 1009：数字黑洞

![image-20210122174605797](https://i.loli.net/2021/01/22/BChjYuJ1qpZxRKe.png)

~~~c
//
// Created by Jiaolong on 2021/1/22.
//

#include <stdio.h>
#include <math.h>

int main() {
    int n;
    scanf("%d", &n);
    int p1[4], p2[4], temp, res, big = 0, small = 0;
    int i, j, m, k, l;
    do {
//    n放在数组里
        for (i = 0; i < 4; i++) {
            p1[3 - i] = n % 10;
            n = n / 10;
        }


        for (j = 0; j < 3; j++) {
            for (k = 0; k < 3 - j; k++) {
                if (p1[k] < p1[k + 1]) {
                    temp = p1[k];
                    p1[k] = p1[k + 1];
                    p1[k + 1] = temp;
                }
            }
        }

        for (m = 0; m < 4; m++) {
            p2[m] = p1[4 - m - 1];
        }

        for (n = 0; n < 4; n++) {
            big += p1[n] * powf(10, 3 - n);
        }

        for (l = 0; l < 4; l++) {
            small += p2[l] * powf(10, 3 - l);
        }


        res = big - small;
        if (small > 100 && small < 1000)
            printf("%d - 0%d = %d\n", big, small, res);
        else if (small > 10 && small < 100)
            printf("%d - 00%d = %d\n", big, small, res);
        else if (small < 10)
            printf("%d - 000%d = %d\n", big, small, res);
        else
            printf("%d - %d = %d\n", big, small, res);
        n = res;
        big = small = 0;
    } while (res != 0 && res != 6174);


    return 0;
}

/*
输入例子:
6767
*/

~~~



# 1010：月饼

![image-20210123103303082](https://i.loli.net/2021/01/23/TusV6Mqkb8PSJAW.png)