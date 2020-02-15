# 并发编程

## CountDownLatch 和 CyclicBarrier

CountDownLatch使用场景：当一个线程需要另外一个线程或多个线程执行完之后，再开始执行。使用的时候需要先初始化计数器，调用await方法，阻塞线程。调用countDown方法，计数器减一，计数器减到0时，线程被唤醒。示例代码
```
private static CountDownLatch latch = new CountDownLatch(1);

public static void main(String[] args) throws InterruptedException {
    System.out.println("主线程开始执行");
    Thread thread = new Thread(new Worker());
    thread.start();
    System.out.println("主线程等待");

    latch.await();
    System.out.println("主线程继续");
}

public static class Worker implements Runable {
    @Override
    public void run() {
        System.out.println("子线程任务正在执行");

        try {
            Thread.sleep(2000);
        } catch (InterruptedException e){

        } finally {
            latch.countDown();
        }
    }
}
```

cyclicBarrier使用场景：一组线程之间互相等待
```
Vector<P> pos;
Vector<D> dos;

Excutor excutor = Excutor.newFixedThreadPool(1);

final CyclicBarrier barrier = new CyclicBarrier(2, () ->{
    excutor.excute(() -> check())
})

void check(){
    P p = pos.remove(0);
    D d = dos.remove(0);

    diff = check(p,d);
    save(diff);
}

void checkAll(){
    Thread t1 = new Thread(() - {
        while(//condition){
            pos.add(getOrders);
            barrier.await();
        }
    })

    T1.start();
    Thread t2 = new Thread(() - {
        while(//condition){
            dos.add(getDOrders());
            barrier.await();
        }
    })
    t2.start();
}
```
