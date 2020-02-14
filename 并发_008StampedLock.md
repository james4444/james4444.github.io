# 并发编程

## StampedLock

StampedLock 支持三种模式：
写锁、悲观读锁、乐观读。其中写锁和悲观读锁与ReadWriteLock的语义一致，不同的是，StampedLock加锁成功之后，都会返回一个stamp,解锁的时候，需要传入这个stamp
```
    final StampedLock sl = new StampedLock();

    long stamp = sl.readLock;

    try{

    } finally {
        sl.unReadLock(stamp);
    }

    stamp = sl.writeLock();
    try{

    } finally {
        sl.unWriteLock(stamp);
    }
```

StampedLock支持锁之间的升降级

```
class Point{
    private int x , y ;
    final StampedLock sl = new StampedLock();

    int distanceFromOrigin() {
        long stamp = sl.tryOptimisticRead();

        int curX = x , curY = y;
        
        if(sl.validate(stamp)){
            stamp = sl.readLock();

            try{
                curX = x;
                curY = y;
            } finally {
                sl.unReadlock(stamp);
            }
        }

        return Math.sqart(curX * curX + curY * curY );
    }
}
```