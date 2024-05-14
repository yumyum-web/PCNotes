# Multithreading Issues and Solutions

## Thread Interference and Memory Consistency Errors

- **Thread Interference**: When two or more threads try to access the same resource at the same time and interleave
  their operations.
- **Memory Consistency Errors**: When different threads have inconsistent views of what should be the same data.

> These problems can be solved by creating **happens-before relationships** between the actions of different threads.

### Thread.start()

- Statements that appear before a thread start call are guaranteed to happen before the thread starts.

### Thread.join()

- When a thread joins another thread, it is guaranteed that the complete execution of the joined thread happens before
  the join returns.

### Object initialization

- When an object is initialized, all the fields are guaranteed to be visible to all threads that access the object.

### Actions on the same thread

- Actions on the same thread are guaranteed to happen in the order they are written.

### Synchronization

- Synchronization is a way to create happens-before relationships between threads.
- Synchronization mechanism is built using Intrinsic Locks. _(Every object in Java has an intrinsic lock associated with
  it.)_
- Only one thread can hold the lock of an object at a time.
- It is possible to call a synchronized method inside another synchronized method or a block, because the thread already
  holds the
  lock of the object.
- When a thread acquires the lock of an object, it is guaranteed that all the changes made by the thread are visible to
  all other threads that subsequently acquire the lock of the same object.

#### Synchronized Methods

- When a method is synchronized, it is required that the thread acquires the lock of the object before executing the
  method.

```java
public class SynchronizedCounter {
    private int c = 0;

    public synchronized void increment() { // only one call to increment or decrement can execute at a time
        c++;
    }

    public synchronized void decrement() {
        c--;
    }

    public int value() {
        return c;
    }
}
```

#### Synchronized Blocks

- When a block of code is synchronized, it is required that the thread acquires the lock of the object before executing
  the block.

```java
public void addName(String name) {
    synchronized (this) {
        lastName = name;
        nameCount++;
    }
    nameList.add(name);
}
```

## Liveness

- A concurrent application is said to be live if it keeps making progress. If a thread is blocked, waiting for
  resources, it is not making progress.

### Deadlock

- A deadlock occurs when two or more threads are blocked forever, waiting for each other to,
    - release locks (improper synchronization)
    - finish execution (thread join)
- Deadlocks can be avoided by ensuring that the threads always acquire the locks in the same order.
- Deadlocks can be prevented by using a timeout when acquiring locks.
    - But this can lead to **livelocks.**

```java
/**
 * This demonstrates a possible deadlock.
 */

class Friend {
    private String name;

    public synchronized void bow(Friend bower) {
        System.out.format("%s is bowing to %s\n", this.name, bower.getName());
        bower.bowBack(this);
    }

    public synchronized void bowBack(Friend bower) {
        System.out.format("%s is bowing back to %s\n", this.name, bower.getName());
    }
}

public class Deadlock {
    public static void main(String[] args) {
        final Friend alphonse = new Friend("Alphonse");
        final Friend gaston = new Friend("Gaston");
        new Thread(() -> alphonse.bow(gaston)).start();
        new Thread(() -> gaston.bow(alphonse)).start();
    }
}
```

### Starvation

- Starvation occurs when a thread is unable to gain access to shared resources because other threads are constantly
  accessing them.
- Starvation can be avoided by using a fair lock, which ensures that the longest waiting thread gets access to the
  resource.

### Livelock

- Livelock occurs when two or more threads keep changing their states in response to the other threads, without making
  any progress.
- Livelocks can be avoided by introducing randomness in the thread behavior.

```java
/**
 * This demonstrates a possible livelock.
 */

import java.util.concurrent.locks.Lock;

class Safe {
    private final Lock lock1;
    private final Lock lock2;

    public void open() {
        while (true) {
            if (lock1.tryLock()) {
                System.out.println("Lock1 acquired");
                if (lock2.tryLock()) {
                    System.out.println("Lock2 acquired");
                    System.out.println("Safe opened");
                    return;
                } else {
                    System.out.println("Lock2 not acquired");
                    lock1.unlock();
                }
            } else {
                System.out.println("Lock1 not acquired");
            }
        }
    }
}

public class Livelock {
    public static void main(String[] args) {
        Safe safe = new Safe();
        new Thread(() -> safe.open()).start();
        new Thread(() -> safe.open()).start();
    }
}
```

## Producer-Consumer Problem

- The producer produces data and the consumer consumes the data.
- The producer and consumer share a common buffer.
    - The producer should wait if the buffer is full
    - The consumer should wait if the buffer is empty.
- The producer and consumer should not access the buffer at the same time, i.e., they should be synchronized.

### Guarded Blocks

- Guarded blocks are used to ensure that a thread waits until a condition is satisfied.
- This is a thread coordination mechanism.

```java
public class Line {
    private int buffer;
    private boolean occupied = false;

    public synchronized void put(int value) {
        while (occupied) {
            try {
                wait(); // release the lock and wait, until notified. The lock is reacquired when notified.
            } catch (InterruptedException _) {
            }
        }
        buffer = value;
        occupied = true;
        notifyAll(); // notify all waiting threads, the lock must be released before one can execute.
    }
}
```

- The `wait()` method releases the lock and waits until it is notified.
- The `notifyAll()` method notifies all waiting threads.
- receiving a notification puts the thread in the **blocked state** until it can reacquire the lock.
