# my-tools



# Table of Contents

- [0004-0001-POSIX_Thread.md](#0004-0001-posix_threadmd)
  - [主要议题](#主要议题)
  - [POSIX Thread 简介](#posix-thread-简介)
    - [简介](#简介)
      - [POSIX Thread 介绍：](#posix-thread-介绍：)
        - [POSIX Thread are desicribed by three parts](#posix-thread-are-desicribed-by-three-parts)
    - [线程基础](#线程基础)
      - [同进程中的线程](#同进程中的线程)
      - [线程特有](#线程特有)
    - [多核处理器](#多核处理器)
  - [POSIX Thread 基础 API](#posix-thread-基础-api)
    - [核心 API-创建线程](#核心-api-创建线程)
      - [Java API - new Thread(Runnable)     *MacOs*](#java-api---new-threadrunnable-----macos)
    - [核心 API-线程属性（pthread_attr_t）](#核心-api-线程属性（pthread_attr_t）)
      - [pthread_attr_*](#pthread_attr_)
    - [核心API-终止线程](#核心api-终止线程)
  - [POSIX Thread 同步 API](#posix-thread-同步-api)
    - [线程同步](#线程同步)
      - [三大原语（`primitives`）](#三大原语（`primitives`）)
      - [互斥（Mutex）](#互斥（mutex）)
        - [类型：](#类型：)
        - [函数：](#函数：)
      - [条件变量（Condition variable）](#条件变量（condition-variable）)
        - [类型](#类型)
        - [主要函数](#主要函数)

# 0004-0001-POSIX_Thread.md

### 主要议题

- POSIX Thread 简介
- POSIX Thread 基础 API
- POSIX Thread 同步 API
- 课程总结



## POSIX Thread 简介

### 简介

> - POSIX stands for Portable Operating System Interface for UNIX
> - POSIX is thus not an implementation of UNIX but rather specificationis of the APIs available for UNIX implementations 
> - The standards in POSIX are specified by the IEEE 
>
> > 



#### POSIX Thread 介绍：

> ​	The POSIX thread libraries are a standards based thread API for C/C++ . It allows one to spawn a new concurrent process flow. It is most effective on multi-processor or multi-core systems where the process flow can be scheduled to run on another processor thus gaining speed through parallel or distributed processing . Threads require less overhead than "forking" or spawning a new process because the system does not initialize a new system virtual memory space and environment for the process. While most effective on a multi-processor system, gains are also found on uniprocessor systems which exploit latency in I/O and other system functions which may halt process execution. 
>
> > 1995 年 已经成型。



> https://en.wikipedia.org/wiki/POSIX_Threads
>
> 影响到了很多操作系统的线程的实现。
>
> 
>
> https://sourceware.org/pthreads-win32/
>
> C 的实现，就是 windows 底层的适配。
>
> 





##### POSIX Thread are desicribed by three parts

- Functions for running threads
- Functions for synchronizing threads
- Functions for scheduling threads

一个 运行的线程的函数。Java 主要是静态

同步线程的函数

定时线程的函数



### 线程基础

#### 同进程中的线程

- 进程指令（Process instructions）
- 打开的文件描述（FD）  
- 信号和信号处理（signals and signal handlers）
- 当前工作目录（current working directory）



Linux 和 windows 都有线程数的限制

#### 线程特有

- 线程ID （Thread ID）
- 寄存器集合、栈指针（set of registers, stack pointer）
- 局部变量栈和返回地址（stack for local variables, return addresses）
- 信号掩码（signal mask）
- 优先级（priority）
- 返回值（Return value: errno）



Linux 2.6 之前，没有线程的概念， 线程 - 进程

线程会有自己的 寄存器和栈指针，java 没有办法控制。

方法去调用的话，一句代码可能是一帧，类似于入栈的操作

Java 是没有返回值的，只有异常的时候，抛出来异常。



### 多核处理器



英文不会带来价值，但是会带来附加价值。









PO









## POSIX Thread 基础 API

### 核心 API-创建线程

pthread_create

#### Java API - new Thread(Runnable)     *MacOs*

```c
int pthread_create(pthread_t _Nullable * _Nonnull _restrict,
                  const pthread_attr_t *_Nullable _restrict,
                  void * _Nullable (* _Nonnull)(void * _Nullable),
                  void * _Nullable _restrict);
```



window 的编程的风格

https://docs.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-createthread

```c++
HANDLE CreateThread(
  LPSECURITY_ATTRIBUTES   lpThreadAttributes,
  SIZE_T                  dwStackSize,
  LPTHREAD_START_ROUTINE  lpStartAddress,
  __drv_aliasesMem LPVOID lpParameter,
  DWORD                   dwCreationFlags,
  LPDWORD                 lpThreadId
);
```



visualstudio.com

- Visual Studio IDE
- Visual Studio Code

> 先安装 Revo Uninstaller 2.0.6
>
> 先全部卸载，再全部重新安装，像 JDK 一样。
>
> 安装
>
> visual-statio-space
>
> 右侧，引入目录，  32 下载到哪，设置哪里，include
>
> 库目录 lib
>
> #include <pthread.h>
>
> C++
>
> 连接器     `..../pthreads-win32-9-1/Pre-built.2/lig/x86/phreadVC2.lib` 

这个主要是 C 语言的实现

```c++
int main(){
    pthread_t t1;
    // 创建 t1 线程，并且将执行对象只想 void* helloWorld(void* ptr);
    int result = pthread_create(&t1, NULL, helloWorld, NULL);
    
    pthread_join(t1, NULL);
    
    return EXIT_SUCCESS;
}

void* helloWorld(void* ptr) {
    pthread_t t = pthread_self();
    printf("Thread[id:%d] - Hello World\n",t.x);
    return NULL;
}
```







```java
public class HelloWorldThreadDemo{
    public static void main(String[] args){
       // 创建 Java 线程
        Thread t1 = new Thread(HelloWorldThreadDemo::helloWorld);
        
        // 显示的启动
        t1.start(); // pthread_create()
        // 等待线程执行结束
        t1.join(); // pthread_join()
    }
    
    static void helloWorld() {
         System.out.println("Thread[name: "+ Thread.currentThread().getId() +"]Hello world!");
    }
}
```

- Action
- Consumer
- Producer
- Predicate







### 核心 API-线程属性（pthread_attr_t）

##### pthread_attr_*

- 状态：是否可 JOIN，默认值 `PTHREAD_CREATE_JOINABLE`
- 调度策略：是否实时，默认值
- 范围：内核（`PTHREAD_SCPE_SYSTEM`）、用户（`PTHREAD_SCOPE_PROCESS`）
- 栈：地址和大小



Java 栈的大小

> https://www.oracle.com/technetwork/java/javase/tech/vmoptions-jsp-140102.html
>
> | -XX:ThreadStackSize=512 | Thread Stack Size (in Kbytes). (0 means use default stack size) [Sparc: 512; Solaris x86: 320 (was 256 prior in 5.0 and earlier); Sparc 64 bit: 1024; Linux amd64: 1024 (was 0 in 5.0 and earlier); all others 0.] |
> | ----------------------- | ------------------------------------------------------------ |
> |                         |                                                              |
>
> 默认单位 kb，每个系统不一样。



`java` 和 `c` 的方法命名基本上都是一样的。



Java 有一个缺点，只能全局区设置栈的大小，



c 语言可以

```c

size_t_stack_size = 512 * 1000;

pthread_attr_setstacksize(&attr, stack_size);




```



 idea CL openjdk-8-src



```cpp
设置栈的大小


```



`JavaThread` 又不同的类型

- 栈
- 帧

`JavaThread` 就是一个 Java 线程，就是用 Java Thread 去进行包装，



`Thread` 

```java
start
-> start0() 方法 native


    
```

`jvm.h`

`#start` 

- `#start0`
  - `#run`

回调，



`os_linux.cpp` 

```cpp
// Thread start routine for all newly created threads
static void *java_start(Thread *thread) {
// Try to randomize the cache line index of hot stack frames.
//
//    
//
//
	
}
```



JNI



映射



- `Thread#start`
  - `Thread#start0` 
    - 回调： `run()` 





`ThreadLocalStorage`  TLS

第三期，讲到了 偏向锁，装到了对象上边。



`Thread#start` 为什么要加 `sychronized` ？如果不加就没有办法在 java 层面保证线程的启动顺序。 主线程 显示的启动子线程。



### 核心API-终止线程

- 等待函数执行完毕

- ```c
  void pthread_exit(void* value)
  ```

  - Java API - `Thread#exit()` （非公开方法）

- ```c
  int pthread_cancle(pthread_t thread)
  ```

  - Java API - `Thread#stop()` （不推荐方法）



`thread.cpp` 

```cpp
void JavaThread:thread_main_inner() {
    
    if(!this->has...)
    
    // 退出
    this -> exit(false);
    delete this;
}
```



```java
//Java 里边可以打印线程状态：

Thread.getState();

// false 时，JVM 里边这个线程已经消亡了
Thread.isAlive()
```









## POSIX Thread 同步 API

### 线程同步

#### 三大原语（`primitives`）

- 互斥（Mutex）
- 条件变量（Condition variable）
- 屏障（Barriers）



#### 互斥（Mutex）

A POSIX Threads mutex is a lock with a sleep queue - and not a spin lock.

简单的就是一个锁，

##### 类型：

`pthread_mutex_t` 

##### 函数：

- `pthread_mutex_init` - used to create mutex attribute objects respectively . 创建

- `pthread_mutex_destroy` - used to free a mutex object which is no longer needed .  消亡

- `phread_mutex_lock` - is used by a thread to acquire a lock on the specified mutex variable. If the mutex is already locked by another thread, this call will block the calling thread until the mutex is unlocked.  一个线程去获得锁，如果其它的线程获得锁了，需要等待其他的线程释放，才能拿到。

- `pthread_mutex_trylock` -  will attempt to lock a mutex. However, if the mutex is already locked, the routine will return immediately with a "busy" error code. This routine may be useful in preventing deadlock conditions, as in a priority-inversion situation. 已经锁住了，会返回 “busy”，这个方法可以防止死锁，作为一个优先级反转的情况。

- `pthread_mutex_unlock` - will unlock a mutex if called by the owning thread. Calling this routine is required after a thread has completed its use of protected date if other threads are to acquire the mutex for their work with the protected data. An error will be returned 

  - If：
    - If the mutex was already unlocked
    - If the mutex is owned by another thread

  会获取错误，当对象已经被解锁的时候，这个锁被其他线程获取到的时候。



```java
public class SynchronizedDemo {
    
    
    private static void addConter() {
       lock.lock();
        
    }
    
    private static getThreadPrefix(){
        return "Thread["+ Thread.currentthread().getId() +"]: ";
    }
}
```



#### 条件变量（Condition variable） 

A condition variable lets a thread wait for something to happen in the future, and another thread to inform it that it hash happened. 

##### 类型

`pthread_cond_t` 

##### 主要函数

- `pthread_cond_wait` - causes calling thred to wait 等待
- `pthread_cond_singal` - wakes up one waiting thread 唤醒一个
- `pthread_cond_broadcast` - wakes up all waiting threds 唤醒所有

pthread 需要放到 `Lock` 中

 java 的 `#await()` 和 `#singal()` 需要放在 `synchronized` 里边





Java 在 JVM 做了很多系统的适配。



- # 测试



















