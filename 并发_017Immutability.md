# 并发编程

## immutability

不变性模式：对象一旦创建之后，状态就不再发生变化

快速实现具备不可变性的类：将一个类的所有属性都设置成final的，并且只允许存在只读方法，那么这个类基本上就具备不可变性了。更严格的做法是这个类本身也是final类型的。实例代码：

```
public final class String {
    private final char value[];

    String replace(char oldChar, char newChar) {
        if(oldChar == newChar){
            return this;
        }

        int len = value.length;

        int i = -1;

        char[] val = value;
        while(++i < len){
            if(val[i] == oldChar){
                break;
            }
        }

        if(i > len) return this;

        char buf[] = new char[len];
        for(int j=0; j<i; j++){
            buf[j] = val[j];
        }

        while(i < len){
            char c = val[i];
            buf[i] = (c == oldChar)?newChar:c;

            i++;
        }

        return new String(buf,true);
    }
}
```