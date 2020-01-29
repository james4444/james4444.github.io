# 数据结构与算法

## trie树

对要处理的字符串的要求：

1. 字符串包含的字符集不能太大

2. 要求字符串的前缀重合比较多


trie树的缺点：

1. 需要手动去实现

2. 用到了指针，对缓存不够友好，性能上会打个折扣

trie树的适用场景：

查找前缀匹配的字符串和自动补全

trie树的实现

```
public class Trie{

    private TreeNode = new TreeNode('/');
    public class TreeNode{
        public char data;
        public TreeNode[] children = new TreeNode[26];
        public boolean isEndingChar = false;

        public TreeNode(char data){
            this.data = data;
        }
    }

    public void insert(char[] text){
        TreeNode p = root;

        for(int i = 0; i < text.length; i++){
            int index = text[i] - 'a';

            if(p.children[index] == null){
                p.children[index] = new TreeNode(text[i]);
            }

            p = p.children[index];
        }

        p.isEndingChar = true;
    }

    public boolean find(char[] text){
        TreeNode p = root;

        for(int i = 0; i < text.length; i++){
            int index = text[i] - 'a';

            if(p.children[index] == null) return false;

            p = p.children[index];
        }

        return p.isEndingChar;
    }
}
```

