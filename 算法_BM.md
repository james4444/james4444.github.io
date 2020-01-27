# 数据结构与算法

## BM算法

核心思想：尽可能多的向后移动模式串

BM算法分为两部分，坏字符和好后缀

坏字符：从后往前诸位比较模式串与主串的字符，当找到不匹配的字符串时，记录模式串的下表si,并找到坏字符在模式串中，位于下标si前的最近位置xi，如果不存在，则记录为-1.si-xi即为向后滑动的距离。如果每次暴力查找xi,会比较消耗性能，所以我们通过散列表，提前进行预处理，将每个字符对应的下表散列存储。散列存储带来的一个问题是，如果字符串存在两个相同的字符，我们只能存储一个值，为了不遗漏导致结果错误，我们存储了最后一个下标，带来的一个问题是有可能会向前移动，所以坏字符是不能单独工作的，需要依赖好后缀一起实现


好后缀：核心内容
* 在模式串中，查找跟好后缀匹配的另一个字串
* 在好后缀的后缀字串中，查找最长的，能跟模式串的前缀字串匹配的后缀字串

代码实现：
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

private void generateGS(char[] b, int m, int[] suffix, blean[] prefix){
    for(int i = 0; i < m; i++){
        suffix[i] = -1;
        prefix[i] = false;
    }

    for(int i = 0; i < m-1; ++i){
        int j = i;
        int k = 0;

        while(j >= 0 && b[j] == b[m-1-k]){
            --j;
            ++k;
            suffix[k] = j + 1;
        }

        if(j == -1 ) prefix[k] = true;
    }
}

public int bm(char[] a, int n, char[] b ,int m){
    int[] bc = new int[SIZE];
    gernerateBC(b, m, bc);

    int[] suffix = new int[m];
    boolean prefix = new boolean[m];

    generateGS(b, m, suffix, prefix);

    int i = 0;

    while(i < n -m ){
        int j;

        for(j = m -1; j >= 0 ; j--){
            if(a[i+j] != b[j]) break;
        }

        if(j < 0){
            return -1;
        }

        int x =  i + (j - bc[(int)a[i+j]]);
        int y = 0;

        if(j < m -1){
            y = moveBYGS(j, m, suffix, prefix);
        }

        i = i + Max(x,y);
    }

    return -1;
}

private int moveBYGS(int j, int m, char[] suffix, boolean[] prefix){
    int k = m - 1 - j;

    if(suffix[k] != -1) return j - suffix[k] + 1;

    for(int r = j + 2; r < = m-1 ; ++r){
        if(prefix[m-r] == ture) {
            retrun r;
        }
    }
    retrun m;
}
```