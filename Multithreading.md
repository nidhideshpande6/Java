# Java Multithreading Notes

## Multithreading
Multithreading is a feature in Java that allows concurrent execution of two or more threads. A thread is the smallest unit of a process.

### Key Benefits
- **Improved Performance**: Efficient utilization of CPU by running multiple tasks simultaneously.
- **Responsive UI**: Keeps user interfaces responsive by handling heavy tasks in the background.
- **Better Resource Sharing**: Threads share the same memory space.

---

## Threads in Java
Threads can be created in Java using:
1. **Extending the `Thread` class**
2. **Implementing the `Runnable` interface**

### Example: Extending Thread Class
```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is running");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread thread = new MyThread();
        thread.start();
    }
}
```

### Example: Implementing Runnable Interface
```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Thread is running");
    }
}

public class Main {
    public static void main(String[] args) {
        Thread thread = new Thread(new MyRunnable());
        thread.start();
    }
}
```

---

## Synchronization
Synchronization in Java is used to control access to shared resources in a multithreaded environment.

### `synchronized` Keyword
The `synchronized` keyword can be used:
1. To synchronize a **method**
2. To synchronize a **block**

### Example: Synchronizing a Method
```java
class Counter {
    private int count = 0;

    public synchronized void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }
}
```

### Example: Synchronizing a Block
```java
class Counter {
    private int count = 0;

    public void increment() {
        synchronized (this) {
            count++;
        }
    }

    public int getCount() {
        return count;
    }
}
```

---

## Deadlock
A deadlock occurs when two or more threads are waiting for each other to release resources, and none can proceed.

### Example of Deadlock
```java
class A {
    synchronized void methodA(B b) {
        System.out.println("Thread1 starts execution of methodA");
        try { Thread.sleep(1000); } catch (InterruptedException e) {}
        b.last();
    }

    synchronized void last() {
        System.out.println("Inside A's last method");
    }
}

class B {
    synchronized void methodB(A a) {
        System.out.println("Thread2 starts execution of methodB");
        try { Thread.sleep(1000); } catch (InterruptedException e) {}
        a.last();
    }

    synchronized void last() {
        System.out.println("Inside B's last method");
    }
}

public class DeadlockExample {
    public static void main(String[] args) {
        A a = new A();
        B b = new B();

        Thread t1 = new Thread(() -> a.methodA(b));
        Thread t2 = new Thread(() -> b.methodB(a));

        t1.start();
        t2.start();
    }
}
```

### How to Avoid Deadlock
- **Avoid Nested Locks**: Do not lock multiple resources if not required.
- **Lock Ordering**: Always acquire locks in a specific and consistent order.
- **Timeouts**: Use `tryLock` with timeouts in `java.util.concurrent.locks`.

---

## Asynchronous Programming
Asynchronous programming allows tasks to run in the background without blocking the main thread.

### Using `CompletableFuture`
```java
import java.util.concurrent.CompletableFuture;

public class AsyncExample {
    public static void main(String[] args) {
        CompletableFuture.runAsync(() -> {
            try {
                Thread.sleep(1000);
                System.out.println("Async task completed");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });

        System.out.println("Main thread continues");
    }
}
```

---

## Thread Pooling
Thread pools manage a pool of worker threads, improving performance by reusing threads.

### Using `Executors` API
```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ThreadPoolExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(3);

        for (int i = 0; i < 5; i++) {
            int taskId = i;
            executor.execute(() -> System.out.println("Task " + taskId + " executed by " + Thread.currentThread().getName()));
        }

        executor.shutdown();
    }
}
```

---

## Inter-thread Communication
Inter-thread communication is achieved using methods like `wait()`, `notify()`, and `notifyAll()`.

### Example
```java
class SharedResource {
    synchronized void produce() {
        try {
            System.out.println("Producing...");
            wait();
            System.out.println("Resumed production");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    synchronized void consume() {
        System.out.println("Consuming...");
        notify();
    }
}

public class CommunicationExample {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource();

        new Thread(resource::produce).start();
        new Thread(() -> {
            try {
                Thread.sleep(1000);
                resource.consume();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }).start();
    }
}
```

---

## Conclusion
- **Threads**: Smallest unit of execution.
- **Synchronization**: Prevents thread interference.
- **Deadlock**: Avoid using best practices.
- **Asynchronous Programming**: Allows non-blocking execution.
- **Thread Pooling**: Efficient management of threads.

Mastering these concepts enables robust and efficient multithreaded applications in Java.
