#books

### Compute number of theads

^c4a31a

```ad-note
title: Compute number of threads
Number of threads = Number of available cores / (1 - Blocking coefficient)
```

### Computationally intensive
#blocking-coefficient is 0, the number of threads is equal to the number of cores.
Having more threads than that will not help speedup, it may actually slow things down.

```java
import java.util.ArrayList;  
import java.util.List;  
import java.util.concurrent.*;  
  
public class ConcurrentPrimeFinder extends AbstractPrimeFinder {  
    private final int poolSize;  
    private final int numberOfParts;  
  
    public ConcurrentPrimeFinder(int poolSize, int numberOfParts) {  
        this.poolSize = poolSize;  
        this.numberOfParts = numberOfParts;  
    }  
    public static void main(String[] args) {  
        new ConcurrentPrimeFinder(2, 2).timeAndCompute(10_000_000);  
    }  
    @Override  
    public int countPrimes(int number) {  
        int count = 0;  
        try {  
            final List<Callable<Integer>> partitions = new ArrayList<>();  
            final int chunksPerPartition = number / this.numberOfParts;  
  
            for (int i = 0; i < numberOfParts; i++) {  
                final int lower = (i * chunksPerPartition) + 1;  
                final int upper = (i == this.numberOfParts - 1) ? number : lower + chunksPerPartition - 1;  
                partitions.add(() -> countPrimesInRange(lower, upper));  
            }  
            final ExecutorService executorPool = Executors.newFixedThreadPool(this.poolSize);  
            final List<Future<Integer>> resultFromParts = executorPool.invokeAll(partitions, 1000, TimeUnit.SECONDS);  
            executorPool.shutdown();  
            for (final Future<Integer> result : resultFromParts) {  
                count += result.get();  
            }  
            return count;  
        } catch (Exception ex) {  
            throw new RuntimeException(ex);  
        }    
    }
}
```

- workload across the two threads/cores is not even distrubuted.
- The first half finishes much faster than the second.
- To achieve the maximum speedup, we need to partition the problem across the two threads evenly.

#### Speed up
- For computationally intensive operations a fair balance of workload among parts is critical.
- Keep an eye on the effort to divide the problem.

#### Strategies
- In order to benefit from concurrency, we must be able to partition problem into small tasks that can be run concurrently.
- If tasks are IO intensive or have significant IO operations, then having more threads will help. In this case, the number of threads should be much greater than the number of cores.

[[#^c4a31a]]

- For computationally intensive operations, having more threads than cores may actually slow things down. We should try to arrive at a fair workload by using a simple approach to partitioning.

# Design Approaches
- Manipulating state doesn't necessarily mean mutating state.

- Think of state transformation instead of state modification.

### Dealing with State
there are three ways for dealing with state:

- #shared-mutability - we create a variables and allow any thread to modify them.
- #isolated-mutability - variables are mutable but are never seen by more than one thread, ever.
- #pure-immutability - nothing is allowed to change.

#pure-immutability  is ideal. At minimum, we should aim to #isolated-mutability and avoid #shared-mutability .



#flashcards