# 数据结构与算法

## BM算法

核心思想：尽可能多的向后移动模式串

BM算法分为两部分，坏字符和好后缀

坏字符：从后往前诸位比较模式串与主串的字符，当找到不匹配的字符串时，记录模式串的下表si,并找到坏字符在模式串中，位于下表si前的最近位置xi，如果不存在，则记录为-1.si-xi即为向后滑动的距离。代码实现：
```
private static final int SIZE = 256;

private void generateBC(char[] b, int m ,int[] bc){
    for(int i = 0; i < SIZE; i++){
        bc[i] = -1 ;
    }

    for(int i = 0; i < m; i++){
        int ascii = (int)b[i];
        bc[ascii] = i;
    }
}

public int bm(char[] a, int n, char[] b ,int m){
    int[] bc = new int[SIZE];
    gernerateBC(b, m, bc);

    int i = 0;

    while(i < n -m ){
        int j;

        for(j = m -1; j >= 0 ; j--){
            if(a[i+j] != b[j]) break;
        }

        if(j < 0>){
            return -1;
        }

        i = i + (j - bc[(int)a[i+j]]);
    }

    return -1;
}
```