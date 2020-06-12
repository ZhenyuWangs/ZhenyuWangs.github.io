```python
import threading

def thread_job():
    print('This is an added Thread, number is %s' %threading.current_thread())

def main():
    added_thread = threading.Thread(target=thread_job)    #添加一个新线程 target为线程的任务
    added_thread.start()    # 运行新增加的线程
    
    #print(threading.active_count())    #有多少个激活的线程
    #print(threading.enumerate())    #查看每个线程都是什么
    #print(threading.current_thread())    #当前运行的是哪一个线程
    
if __name__ == '__main__':
    main()
```

    This is an added Thread, number is <Thread(Thread-6, started 2128)>6
    [<_MainThread(MainThread, started 4176)>, <Thread(Thread-4, started daemon 3368)>, <Heartbeat(Thread-5, started daemon 13116)>, <HistorySavingThread(IPythonHistorySavingThread, started 13172)>, <ParentPollerWindows(Thread-3, started daemon 13280)>, <Thread(Thread-6, started 2128)>]
    <_MainThread(MainThread, started 4176)>
    
    


```python
import threading
import time

def thread_job():
    print('T1 start\n')
    for i in range(10):
        time.sleep(0.1)
    print('T1 finish\n')    #多线程调用的函数不可以用return
    
def T2_job():
    print('T2 start\n')
    print('T2 finish')
    
def main():
    added_thread = threading.Thread(target=thread_job,name='T1')
    thread2 = threading.Thread(target=T2_job,name='T2')
    added_thread.start()
    thread2.start()
    added_thread.join()    #很重要  决定了主线程和次线程的运行先后顺序
    print('all done\n')

    #此时产生的结果显示
'''   
    T1 start

    all done

    T1 finish
    
'''
    #表明主程序在新增加的线程还没运行结束就提前结束了， 此时我们可以使用added_thread.join()
'''
    T1 start

    T1 finish
    
    all done

'''
if __name__ == '__main__':
    main()
```

    T1 start
    
    T2 start
    
    T2 finish
    T1 finish
    
    all done
    
    


```python
import threading
import time
from queue import Queue

def job(ls,q):
    for i in range(len(ls)):
        ls[i] = ls[i]**2
    q.put(ls)    #多线程调用的函数不能用return
    
def multithreading():
    q = Queue()
    threads = []
    data = [[1,2,3],[3,4,5],[4,5,6],[5,6,7]]
    for i in range(4):
        t = threading.Thread(target=job,args=(data[i],q))
        t.start()
        threads.append(t)
    
    for thread in threads:
        thread.join()
        
    results = []
    for _ in range(4):
        results.append(q.get())
    print(results)
if __name__ == '__main__':
    multithreading()
```

    [[1, 4, 9], [9, 16, 25], [16, 25, 36], [25, 36, 49]]
    


```python
import threading
from queue import Queue
import copy
import time

def job(l, q):
    res = sum(l)
    q.put(res)

def multithreading(l):
    q = Queue()
    threads = []
    for i in range(4):
        t = threading.Thread(target=job, args=(copy.copy(l), q), name='T%i' % i)
        t.start()
        threads.append(t)
    [t.join() for t in threads]
    total = 0
    for _ in range(4):
        total += q.get()
    print(total)

def normal(l):
    total = sum(l)
    print(total)

if __name__ == '__main__':
    l = list(range(1000000))
    s_t = time.time()
    normal(l*4)
    print('normal: ',time.time()-s_t)
    s_t = time.time()
    multithreading(l)
    print('multithreading: ', time.time()-s_t)
    
#从结果可以看出多线程实际上在python中并不是真正的多线程，因为有一个线程锁，保证了同一时间只有一个线程的程序在运行，速度并没有变成
#原来的0.25倍，仅仅是少了一个参数输入的时间  因此对于批量数据等情况运用多线程并不会明显提速，此时应该考虑多核multiprocessing
print(threading.active_count())
```

    1999998000000
    normal:  0.16253352165222168
    1999998000000
    multithreading:  0.155623197555542
    5
    


```python
import threading 

def job1():
    global A,lock
    lock.acquire()
    for i in range(10):
        A += 1
        print('job1',A)
    lock.release()

def job2():
    global A,lock
    lock.acquire()
    for i in range(10):
        A += 10
        print('job2',A)
    lock.release()

if __name__ == '__main__':
    A = 0
    lock = threading.Lock()
    t1 = threading.Thread(target=job1)
    t2 = threading.Thread(target=job2)
    t1.start()
    t2.start()
    
```

    job1 1
    job1 2
    job1 3
    job1 4
    job1 5
    job1 6
    job1 7
    job1 8
    job1 9
    job1 10
    job2 20
    job2 30
    job2 40
    job2 50
    job2 60
    job2 70
    job2 80
    job2 90
    job2 100
    job2 110
    
