# 数据结构与算法

## AC自动机

多模式串匹配算法，AC自动机是基于trie树的一种改进算法，它和trie树的关系，就像单模式串中，KMP算法和BF算法的关系一样。

AC自动机的构建分为两个部分，第一部分是构建AC自动机，第二部分是再AC自动机中匹配主串。第一部分又分为两个步骤，一个是构建trie树，另一个是在trie树上构建失败指针

代码实现

```
public void buildFailurePointer(){
    Queue<AcNode> queue = new LinkedList<>();
    root.fail = null;
    queue.add(root);

    while(!queue.isEmpty){
        AcNode p = queue.remove();

        for(int i = 0; i < 26; ++i){
            AcNode pc = p.children[i];
            if(pc == null) continue;

            if(p == root){
                pc.fail = root;
            }else{
                AcNode q = p.fail;
                while(q != null){
                    AcNode qc = q.children[pc.data - 'a'];
                    if(qc != null){
                        pc.fail = qc;
                        break;
                    }
                    q = q.fail;
                }
                if(q == null){
                    pc.fail = root;
                }
                queue.add(pc);
            }
        }
    }

    public void match(char[] text){
        int n = char.length;
        AcNode p = root;

        for(int i = 0; i < n; ++i){
            int idx = text[i] - 'a';

            while(p.children[idx] == null && p != root){
                p = p.fail;
            }

            p = p.children[idx];
            if(p == null) p = root;
            AcNode tmp = p;
            while(tmp != root){
                if(tmp.isEndingChar == true){
                    int pos = i - tmp.length + 1;
                }
                tmp = tmp.fail;
            }
        }
    }
    public class AcNode{
        public char data;
        public AcNode[] children;
        public boolean isEndingChar;

        public int length = -1;
        public AcNode fail ;

        public AcNode(char data){
            this.data = data;
        }
    }
}
```