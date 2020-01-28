# 数据结构与算法

## KMP

KMP 是根据三位作者的名字来命名的

KMP算法的核心思想是，利用好前缀和坏字符，从前向后比较，尽可能的多移动模式串。我们只需要拿好前缀本身，在他的后缀子串中，查找最长的那个可以跟好前缀的前缀子串匹配的。类似BM算法中的bc,suffix,prefix数组，KMP也可以提前构建一个数组，用来存储模式串中每个前缀的最长可匹配前缀字串的结尾下标。我们把这个数组定位为 **next数组** ，很多书中还给这个数组起了一个名字，叫做**失效函数** 。

数组的下标是每个前缀子串的结尾下表，数组的值是这个前缀子串的最长可以匹配的前缀子串的结尾字符的下标。

代码实现：
```
public static int KMP(char[] a, int n, char[] b, int n){
    int[] next = getNext(b, m);
    int j = 0;
    for(int i = 0; i < n; ++i){
        while(j >0 && a[i] != b[j]){
            j = next[j - 1] + 1;
        }
        if(j == m){
            return i -m + 1;
        }
    }

    retrun -1;
}

private static int[] getNext(char[] b, int m){
    int[] next = new int[m];

    next[0] = -1;
    int k = -1;

    for(int i = 1; i < m; ++i){
        while(k != -1 && b[k +1] != b[j]){
            k = next[k];
        }

        if(b[k +1] == b[i]){
            ++k;
        }
        next[i] = k;
    }
    return next;
}
```