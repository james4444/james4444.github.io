# 并发编程

## Executor

线程是一个重量级的对象，应该使用线程池来避免频繁创建和销毁线程。

线程池普遍采用的是生产者，消费者模式。线程池的使用方是生产者，线程池本身是消费者。

考虑到ThreadPoolExcutor 的构造函数实在有些复杂，java并发包提供了一个线程池的静态工厂Excutors,因为Excutor提供的很多默认方法都是使用的无界的LinkedBlockingQueue,高负载环境下，无界队列很容易导致OOM,所以不建议使用Excutor.

线程池没有空闲现线程的拒绝策略
* CallerRunsPolicy: 提交任务的线程自己去执行该任务
* AbortPlicty : 默认的拒绝策略，会抛出RejectedExecutionException
* DiscardPolicy: 直接丢弃任务，没有任何异常抛出
* DiscardOldestPolicy: 丢弃最老的任务，其实就是把最老的任务丢弃，然后把最新的任务加入队列

```
class MythreadPool {
    BlockingQqueue<Runalbe> workQueue;
    List<WorkerThread> threads = new ArrayList<>();

    MythreadPool(int poolSize, BlockingQueue<Runable> workqueue){
        this.workqueue = workqueue;
        for(int idx = 0; idx < poolSize; idx++){
            WorkThread work = new WorkThread();
            work.start();
            threads.add(work);
        }
    }

    void excute(Runnable command){
        workqueue.put(command);
    }

    class WorkThread extends Thread(){
        public void run(){
            while(true){
                Runnable task = workQueue.take();
                task.run();
            }
        }
    }
}

//使用线程池
BlockingQueue<Runnable> workQueue = new LinkedBlockingQueue<>(2);

MyThreadPool pool = new MyThreadPool(10,workQueque);

pool.excute(() ->{
    System.out.println("hello");
})
```