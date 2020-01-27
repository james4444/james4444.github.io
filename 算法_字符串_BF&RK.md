# 数据结构预算法

## 字符串匹配

### BF
BF算法是最简单粗暴的字符串匹配算法，它的实现思路是，拿模式串与主串中所有字串进行对比，看是否有能匹配的字符串。时间复杂度为O(n*m).思想逻辑比较简单，自己实现了一下
```
public static int bf(String n , String m){
        int index = -1 ;

        char[] nArray = n.toCharArray();
        char[] mArray = m.toCharArray();

        for(int i = 0; i < n.length() - m.length() ; i++){
            boolean flag = true;

            for(int j = 0; j < m.length(); j++){
                if(nArray[i + j] != mArray[j]){
                    flag = false;
                    break;
                }
            }

            if(flag) {
                index = i;
                break;
            }
        }

        return index;
    }
```

## RK
RK算法是对BF算法的升级改造，对主串中的每个字串分别求哈希值，然后拿字串的哈希值与模式串进行比较，减少了比较的时间。理想情况下，RK算法的时间复杂度为O(n),当存在哈希冲突的时候，时间复杂度会退化。极端情况下，时间复杂度退化到O(n*m)
