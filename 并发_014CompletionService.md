# 并发编程

## completionService

CompletionService 的实现原理也是内部维护了一个阻塞队列，当任务结束后就把任务的执行结果Future加入到阻塞队列中

CompletionService 的时间接口是 ExecutorCompletionService,这个实现类的构造方法有两个

* ExecutorCompletionService(Executor executor)
* ExecutorCompletionService(Executor executor, BlockingQueue)

实例代码

```
ExecutorService executor = new Executor.newFixedThreadPool(3);

CompletionService<Integer> cs = new ExecutorCompletionService<>(executor);

cs.submit(() -> getPriceByS1());
cs.submit(() -> getPriceByS2());
cs.submit(() -> getPriceByS3());

for(int i = 0; i<3; i++){
    Integer r = cs.take().get();
    executor.execute(() ->save(r))
}
```