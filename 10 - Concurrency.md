# Concurrency

## What is Concurrency?

- concurrency is a property of systems in which several computations are executing simultaneously,
  and potentially interacting with each other.
- It doesn't necessarily mean they'll ever both be running at the same instant.

## Concurrency vs Parallelism

- Concurrency is when two or more tasks can start, run, and complete in overlapping time periods.
  It is a **property of the system.**
- Parallelism is when tasks literally run at the same time, e.g., on a multicore processor.
  It is an **implementation of concurrency.**

## Advantages of Concurrency

- **Multicore processors**: Concurrency is essential for utilizing the full power of multicore processors.
- **Responsiveness**: Concurrency can help improve the responsiveness of a system.

## Processes Vs Threads

### Processes

- A process is an instance of a program running in a computer.
- A process has its own memory space, which means that a process runs independently and is isolated from other
  processes.

### Threads

- A thread is a lightweight sub-process.
- Threads exist within a process — every process has at least one.
- Threads share the same memory space as the process that created it.

## Java Threads

- Each thread in Java is created and controlled by the `java.lang.Thread` class.

### Creating Threads

```java
/*
 * Creating thread by extending the Thread class
 */

class MyThread extends Thread {
    public void run() {
        System.out.println("MyThread running");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread myThread = new MyThread();
        myThread.start();
    }
}
```

```java
/*
 * Creating thread by implementing the Runnable interface
 */

class MyRunnable implements Runnable {
    public void run() {
        System.out.println("MyRunnable running");
    }
}

public class Main {
    public static void main(String[] args) {
        MyRunnable myRunnable = new MyRunnable();
        Thread thread = new Thread(myRunnable);
        thread.start();
    }
}
```

### Thread States

- Thread Scheduler is responsible for moving threads between different states.
- A thread is alive until,
    - The `run()` method completes.
    - The `stop()` method is called.
    - An uncaught exception is thrown.

<img alt="Java Thread Life Cycle.png" src="images/Java Thread Life Cycle.png" width="500"/>

- **New**: When a thread is created, it is in the new state.
- **Runnable**: A thread is in the runnable state after it has been started but before it has been selected by the
  scheduler to run.
- **Running**: The thread is in running state if the thread scheduler has selected it.
- **Blocked**: A thread is in the blocked state if it is waiting for a monitor lock.
- **Dead**: A thread is in dead state if it has completed execution or has been stopped.

### Methods

- `start()`: Schedules the thread for execution.
- `isAlive()`: Returns true if the thread has been started and has not yet died.
- `isInterrupted()`: Returns true if the thread has been interrupted.
- `yield()`: Causes the currently executing thread object to temporarily pause and allow other threads to execute.

#### Thread Name

- Threads have **unique** property name.
- `getName()`: Returns the name of the thread.
- `setName()`: Changes the name of the thread.

#### Sleeping

- `Thread.sleep()` causes the current thread to suspend execution for a specified period.
- Precise sleep times are not guaranteed.
- There are two ways to wake up a sleeping thread:
    - The sleep time expires.
    - Another thread can interrupt the sleeping thread.

#### Interrupting

- `Thread.interrupt()` method is used to interrupt a thread.
- It interrupts the specific thread and throws `InterruptedException` in the thread.
- A thread can `catch` the exception or throw it back to the caller.

#### Joining

- `join()` method waits for a thread to die.
- Can optionally specify a timeout.

#### Thread Priority

- Thread priority is an integer value that determines the priority of a thread.
- When creating a thread, the priority is set to the priority of the creating thread by default.
- There are three constants defined in the `Thread` class:
    - `MIN_PRIORITY`: Minimum priority that a thread can have.
    - `NORM_PRIORITY`: Default priority of a thread.
    - `MAX_PRIORITY`: Maximum priority that a thread can have.
- `setPriority()`: Sets the priority of the thread.

### Daemon Threads

- Daemon threads are low priority threads that run in the background.
- They do not prevent the JVM from exiting when all the user threads finish their execution.
- Main thread is a non-daemon thread.
- `setDaemon()`: Sets the thread as a daemon thread.
- The thread must be set as a daemon thread before starting it.