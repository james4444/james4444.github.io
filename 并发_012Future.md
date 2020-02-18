# 并发编程

## Future

线程池的调用，可以通过ThreadPoolExecutor的excute方法，传入runnable参数执行。但是runnable是没有返回值的，如果需要返回值，需要使用ThreadPoolExecutor的submit方法。ThreadPoolExecutor提供三种submit方法，分别是：
* Future <?> submit(Runnable task);
* <T> Future<T> submit(Callable<T> task);
* <T> Future<T> submit(Runnable task, T result);

三个方法的返回值都为Future,Future提供5个方法，分别是：
* boolean cancel (boolean mayInterruptIfRunning);
* boolean isCancelled();
* boolead isDone();
* get();
* get(long timeout,TimeUnit unit);



