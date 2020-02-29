# 并发编程

## fork join
Fork/join是一个并行计算的框架，主要用来处理分治任务模型的，这个计算框架里的Fork对应的是分治模型里的任务分解，join对应的是结果合并。Fork/join计算框架包含两部分，一部分是分治任务的线程池ForkJoinPool,另一部分是分治任务ForkJoinTask.类似于ThreadPoolExecutor 和 runnable的关系。
ForkJoin是一个抽象类，最核心的方法是fork和join,其中fork()方法会异步的执行一个子任务，而join()方法则会阻塞当前线程来等待子任务的执行结果。
```
public static void main(String[] args){
    ForkJoinPool fjp = new ForkJoinPool(4);
    Fibonacci fib = new Fibonacci(30);

    Integer result = fbj.invoke(fib);

    System.out.println(result);
}

public static class Fibonacci extends RecurSiveTask<Integer>{
    final int n;

    Fibonacci(int n){this.n = n}

    protected Integer compute(){
        if(n <= 1 ) return n;

        Fibonacci f1 = new Fibonacci(n - 1);

        f1.fork();
        Fibonacci f2 = new FiboNacci(n - 2);

        return f2.compute() + f1.join();
    }
}
```