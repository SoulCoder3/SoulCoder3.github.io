---
layout:     post
title:      Python Multithreaded Programming
subtitle:   Python核心编程笔记
date:       2018-10-27
author:     JIAWEI HUANG
header-img: img/post-bg-net.jpg
catalog: true
tags:
    - 笔记
    - 个人
    - Python
---

# Thread Introduction
Prior to the advent of multi-threaded programming, the execution of a computer program consisted of a single sequence of steps that were executed in a synchronized sequence in the host's CPU. Multi-threaded programming is ideal for programming tasks that have the following characteristics: essentially Is asynchronous: multiple concurrent activities are required; the order of processing for each activity may be indeterminate, or random, unpredictable. This programming task can be organized or divided into multiple execution flows, each of which performs The flow has a task that is specified to be completed. Depending on the application, these subtasks may need to calculate intermediate results and then merge them into the final output.

# Threads and Porcesses
## Processes
Computer programs are just executable binary files stored on disk. Only when they are loaded into memory and called by the operating system, have a life cycle. The process is an executing program. Each process has its own address space. Memory, data stacks, and other auxiliary data used to track execution, the operating system manages the execution of all processes on it, and allocates time for these processes. Processes can also perform other tasks by spawning new processes, but because each Degree has its own memory and data stack, so it can only share information by means of interprocess communication.

## Threads
Threads are similar to processes, but they are executed under the same process, sharing the same context. They can be thought of as "mini-processes" running in parallel in a main process.
A thread consists of a start, an execution sequence, and an end. It has an instruction pointer that records the currently running context. When other threads are running, it can be preempted (interrupted) and temporarily suspended (sleep) -- this practice Called concession.
In a process, each thread and the main thread share the same piece of data space, so independent of each other, information sharing and communication between threads is easier. In a single-core CPU system, the execution of threads is actually planned like this: Threads run for a short while, then give way to other threads (re-queue again for more CPU time). During the execution of the entire process, each thread executes its own specific task, communicating with other threads when necessary. .
Of course, this kind of communication is not without risk. If two or more threads access the consent slice data, the result may be inconsistent due to different data access order. This situation is usually called a race condition.

# Threads and Python
## Global Interpreter Lock(GLO)
The execution of Python code is performed by the Python virtual machine (aka the main loop of the interpreter). Python is designed to be baked like this, and only one control thread can be executed in the main loop, just like in a single-core CPU system. Multithreading. There are many programs in memory, but only one program can run at any given time.
Access to the Python virtual machine is controlled by the Global Interpreter Lock (GIL). This lock is used to ensure that only one thread can run at a time. In a multi-threaded environment, the Python virtual machine will execute as described below.
1. Set up GLI
2. Switch into a thread to run
3. Do one of the following
a. The specified number of bytecode instructions
b. Thread actively gives up control
4. Set the thread back to sleep
5. Unlock GIL
6. Repeat the above steps

## using Thread in Python
### Thread Class
* Create an instance of the Thread class and pass it a function
* Create an instance of the Thread class and pass it a class instance that can be used
* Derive a Thread subclass and create an instance of a subclass
  The first and third methods are generally used because the second method is a bit embarrassing and difficult to read.

#### Create a Thread instance and pass it a function
```python
import threading
from time import sleep, ctime
loops = [4,2]

def loop(nloop,nsec):
	print 'start loop', nloop,'at:', ctime()
	sleep(nsec)
	print 'loop', nloop, 'done at:', ctime()
	
def main():
	print 'starting at:', ctime()
	threads = []
	nloops = range(len(loops))
	
	for i in nloops:
		t = threading.Thread(target=loop,args=(i,loops[i]))
		threads.append(t)
	for i in nloops:
		threads[i].start()
	
	for i in nloops:
		threads[i].join()
	
	print 'all DONE at:' , ctime()

if __name__=='_main_':
	main()
```

#### Create thread instance and pass it a callable class instance
```python
improt threading
from time import sleep, ctime

loops = [4,2]

class ThreadFunc(object):
	def __init__(self, func, args, name=''):
		self.name = name
		self.func = func
		self.args = args
	def __call__(self):
		self.func(*self.args)
def loop(nloop,nsec):
    print 'start loop', nloop,'at:', ctime()
    sleep(nsec)
    print 'loop', nloop, 'done at:', ctime()

def main():
    print 'starting at:', ctime()
    threads = []
    nloops = range(len(loops))

    for i in nloops:
        t = threading.Thread(target=ThreadFunc(loop,(i,loops[i]),loop.__name__))
        threads.append(t)
    for i in nloops:
        threads[i].start()

    for i in nloops:
        threads[i].join()

    print 'all DONE at:' , ctime()

if __name__=='_main_':
    main()

```

#### Derive a Thread subclass and create an instance of a subclass
```
import threading
from time import sleep, ctime

loops = (4,2)

class MyThread(threading.Thread):
	def __init__(self, func, args, name=''):
		threading.Thread.__init__(self)
		self.name = name
		self.func = func
		self.args = args
		
	def run(self):
		self.func(*self.args)
		
def loop(nloop,nsec):
    print 'start loop', nloop,'at:', ctime()
    sleep(nsec)
    print 'loop', nloop, 'done at:', ctime()

def main():
    print 'starting at:', ctime()
    threads = []
    nloops = range(len(loops))

    for i in nloops:
        t = MyThread(loop,(i,loops[i]),loop.__name__))
        threads.append(t)
    for i in nloops:
        threads[i].start()

    for i in nloops:
        threads[i].join()

    print 'all DONE at:' , ctime()

if __name__=='_main_':
    main()
```
***
<br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

# 线程简介
在多线程编程出现之前,计算机程序的执行是由单个步骤序列组成的,该序列在主机的CPU中按照同步顺序执行.多线程编程对于具有如下特点的编程任务而言是非常理想的:本质上是异步:需要多个并发活动;每个活动的处理顺序可能是不确定的,或者说是随机的,不可预测的.这种编程任务可以被组织或划分为多个执行流,其中每个执行流度有一个指定要完成的任务.根据应用的不同,这些子任务可能需要计算出中间结果,然后合并为最终输出结果.

# 线程和进程
## 进程
计算机程序只是存储在磁盘上的可执行二进制文件.只有把它们加载到内存中并被操作系统调用,才拥有生存周期.进程则是一个执行中的程序.每个进程度拥有自己的地址空间,内存,数据栈以及其他用于跟踪执行的辅助数据,操作系统管理其上所有进程的执行,并为这些进程合理分配时间.进程也可以通过派生新的进程来执行其他任务,不过因为每个进程度拥有自己的内存和数据栈等,所以只能采用进程间通信方式共享信息.

## 线程
线程与进程类似,不过它们是在同一个进程下执行的,共享相同的上下文.可以将它们认为是在一个主进程中并行运行的一些"迷你进程"
线程包括开始,执行顺序和结束三部分.它有一个指令指针,用于记录当前运行的上下文.当其他线程运行时,它可以被抢占(中断)和临时挂起(睡眠)--这种做法叫做让步.
一个进程中各个线程和主线程共享同一片数据空间,因此彼此独立的进程而言,线程间的信息共享和通信更容易.在单核CPU系统中,线程的执行实际上是这样规划的:每个线程运行一小会,然后让步给其他线程(再次排队等待更多的CPU时间).在整个进程的执行过程中,每个线程执行它自己特定的任务,在必要时和其他线程进行结果通信.
当然这种通信并不是没有风险的.如果两个或多个线程访问同意片数据,由于数据访问顺序不同,可能导致结果不一致.这种情通常称为竞态条件.

# 线程和Python
## 全局解释器锁
Python代码的执行是由Python虚拟机(又名解释器主循环).Python设计时是这样烤炉的,在主循环管中同时只能有一个控制线程在执行,就像单核CPU系统中的多线程一样.内存中可以有许多程序,但是在任意给定时刻只能有一个程序在运行.
对Python虚拟机的访问是由全局解释器锁(GIL)控制的.这个锁是用来保证同时只能有一个线程运行,在多线程环境中,Python虚拟机将按照下面所述方式执行.
1. 设置GLI
2. 切换进一个线程去运行
3. 执行下面操作之一
a. 指定数量的字节码指令
b.线程主动让出控制权
4. 把线程设置回睡眠状态
5. 解锁GIL
6. 重复上述步骤

## 在Python中使用线程
### Thread类
 * 创建Thread类的实例,传给它一个函数
 * 创建Thread类的实例,传给它一个可谓用的类实例
 * 派生Thread子类,并创建子类的实例
 一般使用第一和第三种方法,因为第二种方法显得有些尴尬并难以阅读.

#### 创建Thread实例，并传给它一个函数
```python
import threading
from time import sleep, ctime
loops = [4,2]

def loop(nloop,nsec):
	print 'start loop', nloop,'at:', ctime()
	sleep(nsec)
	print 'loop', nloop, 'done at:', ctime()
	
def main():
	print 'starting at:', ctime()
	threads = []
	nloops = range(len(loops))
	
	for i in nloops:
		t = threading.Thread(target=loop,args=(i,loops[i]))
		threads.append(t)
	for i in nloops:
		threads[i].start()
	
	for i in nloops:
		threads[i].join()
	
	print 'all DONE at:' , ctime()

if __name__=='_main_':
	main()
```

#### 创建Thread的实例，传给它一个可调用的类实例
```python
improt threading
from time import sleep, ctime

loops = [4,2]

class ThreadFunc(object):
	def __init__(self, func, args, name=''):
		self.name = name
		self.func = func
		self.args = args
	def __call__(self):
		self.func(*self.args)
def loop(nloop,nsec):
    print 'start loop', nloop,'at:', ctime()
    sleep(nsec)
    print 'loop', nloop, 'done at:', ctime()

def main():
    print 'starting at:', ctime()
    threads = []
    nloops = range(len(loops))

    for i in nloops:
        t = threading.Thread(target=ThreadFunc(loop,(i,loops[i]),loop.__name__))
        threads.append(t)
    for i in nloops:
        threads[i].start()

    for i in nloops:
        threads[i].join()

    print 'all DONE at:' , ctime()

if __name__=='_main_':
    main()

```

#### 派生Thread子类，并创建子类的实例
```
import threading
from time import sleep, ctime

loops = (4,2)

class MyThread(threading.Thread):
	def __init__(self, func, args, name=''):
		threading.Thread.__init__(self)
		self.name = name
		self.func = func
		self.args = args
		
	def run(self):
		self.func(*self.args)
		
def loop(nloop,nsec):
    print 'start loop', nloop,'at:', ctime()
    sleep(nsec)
    print 'loop', nloop, 'done at:', ctime()

def main():
    print 'starting at:', ctime()
    threads = []
    nloops = range(len(loops))

    for i in nloops:
        t = MyThread(loop,(i,loops[i]),loop.__name__))
        threads.append(t)
    for i in nloops:
        threads[i].start()

    for i in nloops:
        threads[i].join()

    print 'all DONE at:' , ctime()

if __name__=='_main_':
    main()
```
