# Asynchrony

From [Wikipedia](https://en.wikipedia.org/wiki/Asynchrony_(computer_programming)), Asynchrony, in computer programming, refers to the occurrence of events independent of the main program flow and ways to deal with such events. This events includes various type of operations like HTTP requests, disk I/O requests etc. For example, a program may want to read some string from a file. The file is located in the hard disk. And the whole operation for accessing and reading the file is independent of the program that wants to read the file. Another example may be a file download from a server. When a client program requests a server for a file, the request is independent of the client program. Because this operation doesn't depend on any operation of the program. So,these types of operations are Asynchronous operations.

We know that each line of a program is executed sequentially one after another. Each operation blocks the execution of next operation until it itself is executed. So, an asynchronous operation will also block the execution. As the asynchronous operations are independent of the program, it really wasting CPU time. While an asynchronous operation is completing, CPU can do other tasks. 
In a multi threaded CPU, these operations can be distributed into different threads and then be executed. But in a single threaded CPU, this is not possible. An asynchronous operation will block the whole thread until it excutes while wasting CPU time. This is where asynchronous programming come into play.

# Asynchronous Programming

Asynchronous programming is a way of executing asynchronous operations like I/O operations, HTTP requests, database queries in a the same thread without waiting for those operations or using different threads.

Unlike many other programming languagues including C# that are multi threaded, Javascript is single threaded languague.
So, asynchronous programming comes naturally in Javascript. 
But for programming languagues like C# that also supports asynchronous programming, this is an efficient approach towards activities that are blocked or accesses that are delayed in a long running application. For example, in a desktop application consider a HTTP request is executing synchronously in the main UI thread. This request will block the whole thread until its done. So, the application will freeze and become unusable for some time. This is not good for any type of application. To tackle this problem asynchronous programming can be used.  And This is where ```async/await``` come into play.

# Async / Await

There are two ways asynchronous programming can be done in C#.  First approach is using callbacks and the second approach is using ```async/await```.
The second approach is the latest and preferred approach to do asynchronous programming. This approach enable us to write code that like a sequence of statements. asynchronous programming in C# involves these following classes.

### Task / Task<Tresult\>

```Task```  in C# is an class that represents some works to be done. This object indicates if the works are completed or not. ```Task<Tresult>```  returns value for operations and ```Task``` class doesn't return any value. Because the work performed by a ```Task``` object typically executes asynchronously on a thread pool thread rather than synchronously on the main application thread, you can use the Status property, as well as the ```IsCanceled```, ```IsCompleted```, and ```IsFaulted``` properties, to determine the state of a task.  
### async
```async``` keyword enables the ```await```  keyword. Any ```async``` method run like all other methods. It runs synchronously until  the compiler hit the ```await``` keyword. It creates a state machine for the method. 

### await
```await``` can be thought of as a unary operator that takes an expression. The expression is called awaitable. This expression or awaitable represents an asynchronous operation.

``` await awaitable ```

```await``` will pause its async method until awaitable / operation completes. Here,

1. If the operation is already completed, the async method won't be paused.
2. If the operation fails, then raise an exception.

When the async method is paused by ```await```, an incomplete ```Task``` is returned whose result is still not known yet to the caller. This ```Task``` represents the async method. the current context is also captured. This context is used to resume the method when the task is complete.  This context is the current ```SynchronizationContext``` unless it’s null. In practical terms the context in a program maybe a UI context, ASP.NET request context or a thread pool.

### SynchronizationContext

```SynchronizationContext``` is a representation of the current environment that our code is running in. That is, in an asynchronous program, when we delegate a unit of work to another thread, we capture the current environment and store it in an instance of ```SynchronizationContext``` and place it on Task object. Simply put, ```SynchronizationContext``` represents a location “where” code might be executed.  Every thread has its own ```SynchronizationContext```. That means if we delegate work from one thread pool to another thread, we can get the snapshot of the current running environment and pass it to another thread.