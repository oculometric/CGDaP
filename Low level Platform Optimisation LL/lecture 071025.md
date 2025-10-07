parallel processing. can be for concurrent processing (doing multiple things at once), but also to make use of multiple CPU cores to do more work at once.

parallelism is a type of concurrency, but concurrency is not parallelism.
parallelism is applying concurrency as a form of optimisation.

lambdas aka anonymous functions - a function which doesn't have a fixed presence in memory, and can be treated like a value. information mmust be captured in order to be used inside the lambda:
```
int x = 1;
int y = 2;

// you can capture by value or by reference!
// you can also have regular parameters passed when the function is invoked
// you cannot modify the value of a lambda (obviously)
auto lambda_func = [x, &y](int param)
{
	// body
};


// we can then invoke the lambda function:
lambda_func(4);
```

you can wrap all of this in `std::function` to make things saner and have a return type.

moore's law (transistor count) is still alive, but the free lunch has been dead for years.

paralellism can be implemented at different levels: OS/processor level, process threads, virtual threading and language level.

threads usually need to be `join()`ed, which waits for the other thread to finish.

we need to use locks (very carefully) or other synchronisation primitives otherwise we end up with data races (threads overwrite one another's work since CPU operations are not instant). 

- mutex (mutual access controller)
- lock_guard (automatically locks/unlocks a mutex based on scope)

you cannot do recursive locks - if function A locks M, then calls function B which also tries to lock M, you will have a deadlock. also, if thread A locks M1, then thread B locks M2, then thread A tries to lock M2, thread A will be stuck, and thread B locks M1, then thread B will be stuck, causing a deadlock.

`std::async` and `std::future`! future is a box which will hold a value at some point in the future, and you call `.get()` to get the value back out.

amdahl's law:
`speedup = 1 / (1 - p + p/n)`
n  is number of processors, p 

avoid cross-thread coordination. pool threads, and pool the work to be done. worker threads pull work when idle. work can be pushed as needed. context switching takes time, so limit the number of worker threads you use (absolute maximum of the physical hyperthreads).

contention - how much threads fight over shared resources. avoid having threads talk to one another if possible.