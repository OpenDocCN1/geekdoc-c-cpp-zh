> Note In F#, the printf function's output result is interleaving in a multithreaded environment. You can either use the lock function to make it thread-safe or use Console.WriteLine instead.

# Asynchronous Workflows

If you read an article about the advantages of F#, you likely found some information about the ease of parallel programming and usually some association with the Async.Parallel method. If you want F# asynchronous workflows provide the cleanest way to do

Let's start by solving a simple problem with an asynchronous workflow: checking whether a sequence is in an increasing order. The algorithm is simple. Multiple threads are launched to count the incoming sequence into a number of two-element lists. If the first element is smaller than the second element, you increase a shared variable by one. At end of the execution, the shared variable value is the sequence length minus one, is in an increasing order. The code is shown in Listing 6-77. Note that this algorithm and code serve only as a sample for demonstrating the asynchronous workflow. I do not intend to use this code to discuss the performance between single-ithreaded and multithreaded programming.

According to the algorithm, the first problem that needs to be solved is to lock a variable so that the write operation is thread-safe. You can use the lock function presented in Listing 6-75 to solve this problem. The real interesting part starts with the use of async, which specifies that an asynchronous workflow can be executed in parallel. The function takes a two-element array. If the first element x is smaller than the second element y, the shared variable is increased by one.

You use Seq.windowed function to create the two-element sequences that will be used as input. Async.Parallel is then used to make sure that threads execute in parallel and wait to join the result when executing Async.RunSynchronously. This is known as the Fork/Join pattern.

LISTING 6-77 An asynchronous workflow is used to check an increasing sequence

```
type AsyncSample(1:seq<int>) =
  member this.IsIncreasing() =
    // declare a reference cell to hold the shared variable
    let num = 0
    // safely increase the shared variable
    let inc () = Lock(num) (fun _ -> num := (num) + 1)
    // make the sequence into a sequence containing a number of small two-element sequences
    let windowedList = 1 |> Seq.windowed 2
```