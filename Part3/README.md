# Reasons for concurrency and parallelism


To complete this exercise you will have to use git. Create one or several commits that adds answers to the following questions and push it to your groups repository to complete the task.

When answering the questions, remember to use all the resources at your disposal. Asking the internet isn't a form of "cheating", it's a way of learning.

 ### What is concurrency? What is parallelism? What's the difference?
 > Both concurrency and parallelism means, that multiple threads are making progress simultaneously over a certain time frame. However, in a concurrent system, these threads don't have to run at the same time. A scheduler can switch between them.
 > In a true parallel system, the threads (or processes) are executed at the same time. For that multiple CPUs or multi core CPUs are required. [[1]][1]

 ### Why have machines become increasingly multicore in the past decade?
 > In a single core system, the number of cpu executions per time is usually proportional to the clock frequency of the cpu. In the past, clock frequencies have been increased from around 2 MHz (Intel 8080, 1974) to about 4 GHz (Intel 10th Gen i7). Increasing it further would result in a number of problems: Due to the increasing transistor count in modern CPUs and the effect called Dennard Scaling, which means the power consumption per unit volume stays constant no matter the transistor count, thermal issues arise. Other aspects such as timing and communication to other components such as RAM and cache are problematic, too. [[2]][2]
 >
 > In order to increase system performance, it is easier to add more cores to the system and to adapt programs for using them.

 ### What kinds of problems motivates the need for concurrent execution?
 (Or phrased differently: What problems do concurrency help in solving?)
 > Driven by the environment and possibly the user, for a computer system it is often required to execute multiple (logical) tasks simultaneously: A web server has to serve multi clients (browsers), A smartphone should refresh a webpage while still be responsible to user input or an embedded computer should fetch data and generate outputs at the same time.
 > Without a concurrency mechanism, these tasks would be very hard to program.

 ### Does creating concurrent programs make the programmer's life easier? Harder? Maybe both?
 (Come back to this after you have worked on part 4 of this exercise)
 > The examples described in the previous question could be solved with a sequential approach in a 'traditional' matter. But this would be very hard to implement, debug and to be documented.
 >
 > Concurrency allows for easier to develop applications. But still, bugs in these applications are hard to find, because concurrency also brings a lot of undesired side effects, such as possible race conditions etc.

 ### What are the differences between processes, threads, green threads, and coroutines?
 > A process can be viewed as an isolated, virtual computer, with its own resources that are independent from other processes. A thread could then be viewed as a piece of code running on a virtual cpu. Threads for example can share memory. Switching between threads is done by the OS. [[3]][3]
 >
 > Green threads are threads that are not scheduled by the OS operating on physical hardware, but by a virtual machine. Thats why they are common n programming languages using a virtual machine, like Java. [[4]][4]
 >
 > Architectures using coroutines mostly use cooperative context switching in contrast to an OS scheduler. That means, the programmer has to take care of switching and must ensure each coroutine will return after a certain time limit. [[5]][5]

 ### Which one of these do `pthread_create()` (C/POSIX), `threading.Thread()` (Python), `go` (Go) create?
 > * `pthread_create()`: thread
 > * `threading.Thread()`: thread (green threads are called greenlet)
 > * `go`: somewhere between a thread and a coroutine. The *goroutines* are more lightweight than a thread, but context switching is still done implicitly by go runtime at certain suitable points in the routine [[6]][6]

 ### How does pythons Global Interpreter Lock (GIL) influence the way a python Thread behaves?
 > Since the GIL only allows one thread at a time access to the python interpreter, computing tasks that are limited by the CPUs core speed are not speed up when dividing the task into multiple threads. [[7]][7]

 ### With this in mind: What is the workaround for the GIL (Hint: it's another module)?
 > There are Python implementations like *Jython* that don't use a GIL. For *CPython*-based projects, instead of using a thread-based approach, multiprocesses can be used with the [multiprocessing](https://docs.python.org/2/library/multiprocessing.html)-module.

 ### What does `func GOMAXPROCS(n int) int` change? 
 > It sets the number of CPUs to be used. [[8]][8]



## References

[1]: https://docs.oracle.com/cd/E19455-01/806-5257/6je9h032b/index.html
[2]: https://www.micron.com/about/blog/2018/october/metamorphosis-of-an-industry-part-two-moores-law
[3]: https://web.mit.edu/6.005/www/fa14/classes/17-concurrency/
[4]: https://c9x.me/articles/gthreads/intro.html
[5]: https://www.boost.org/doc/libs/1_55_0/libs/coroutine/doc/html/coroutine/overview.html
[6]: https://stackoverflow.com/questions/18058164/is-a-go-goroutine-a-coroutine
[7]: https://realpython.com/python-gil/
[8]: https://golang.org/pkg/runtime/#GOMAXPROCS