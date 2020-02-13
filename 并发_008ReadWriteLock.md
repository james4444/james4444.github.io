# 并发编程

## ReadWriteLock

* 理论上利用sychronized和Semaphore能够解决所有的并发问题，存在其他并发包的原因为分场景解决性能问题。

* ReadWriteLock适用场景，读多写少的场景，如缓存。sychronized对读和写，都是互斥的。ReadWriteLock允许多线程同时读，对写入是互斥的。

* 遵循原则：
1. 允许多个线程同时读取共享变量
2. 只允许一个线程写共享变量
3. 如果一个线程正在写共享变量，是不允许读线程读共享变量的

代码示例：按需加载缓存
```
class Cache<K,V>{
    final Map<K,V> m = new HashMap<>();

    final ReadWriteLock rwl = new ReentrantReadWriteLock();

    final Lock r = rwl.readLock();
    final Lock w = rwl.writeLock();

    V get(K key){
        V v = null;

        r.lock();
        try{
            v = map.get(key);
        } finally {
            r.unlock();
        }

        if(null != v){
            return v;
        }

        w.lock();

        try{
            v = map.get(key);
            if(v == null){
                // 查询数据库
                map.put(key,v);
            }
        } finally {
            w.unlock();
        }

        return v;
    }
}
```

在读锁内，不能将锁升级为写锁，否则写锁会永久等待。在写锁内，可以把写锁降级为读锁