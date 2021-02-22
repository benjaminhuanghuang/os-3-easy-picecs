# fork(), exec(), wait()


## fork()
The process that is created is an (almost) exact copy of the calling process. 

That means that to the OS, it now looks like there are two copies of
the program p1 running, and both are about to return from the fork()
system call. 

The newly-created process (called the child, in contrast to the
creating parent) doesn’t start running at main(), like you might expect
(note, the “hello, world” message only got printed out once); rather, it
just comes into life as if it had called fork() itself

The value it returns to the caller of fork() is different. Specifically, while the parent receives the `PID` of the newly-created child, the child receives a return code of `0`. 

The output (of p1.c) is not deterministic.



## wait()
wait() this system call won’t return until the child has run and exited

Adding a wait() call to the code above makes the output deterministic


## exec()
This system call is useful when you want to run a program that is different from the calling program.

given the name of an executable (e.g., wc), and some arguments (e.g., p3.c), it loads code (and static data) from that executable and overwrites its current code segment (and current static data) with it; the heap and stack and other parts of the memory space of the program are re-initialized. 

Then the OS simply runs that program, passing in any arguments as the argv of that process. 

Thus, `it does not create a new process`; rather, it transforms the currently running program into a different running program (wc). After the exec() in the child, it is almost as if the parent process never ran; a successful call to exec()
never returns.