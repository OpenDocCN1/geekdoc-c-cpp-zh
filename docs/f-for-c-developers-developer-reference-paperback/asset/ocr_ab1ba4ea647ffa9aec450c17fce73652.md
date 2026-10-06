action—which initializes the operation asynchronously. The other is a method called End<Operation>, which is invoked when the operation finishes. The problem with APM is that it makes the code difficult to understand and maintain because related code is scattered in multiple places.

Asynchronous workflows are designed to solve this problem and simplify asynchronous programming tasks. Listing 6-80 shows how to read a file and write the processed result into a new file asynchronously with an F# asynchronous workflow. If you have a file named tt.txt in c:\MyCode that contains the text "A", the content will become "B" after the execution.

# LISTING 6-80 File with an asynchronous workflow

open System.IO

```
let encryptFile fn =
let operation =
    async {
        use fs = new FileStream(fn, FileMode.Open)

        // read the file content
        let data = fs.AsyncRead(int fs.Length)
        let data = data | Array.map(fun n -> n+1)
        use encryptedFile = new FileStream(fn + ".out", FileMode.Create)

        // write the new content to the new file
        do! encryptedFile.AsyncWrite(data)
    }
```

// start the operation with a three-scenario handler function
Async.StartWithContinuations(operation,
    (fun _ -> printf! "finished"), // print when finished successfully
    (fun e -> printf! "something bad happened, %A") // print when exception thrown
    (fun _ -> printf! "user gives up") // print when operation is cancelled

```
encryptFile @"c:\mycode\tt.txt"
```

There is something unique in Listing 6-80—the let (pronounced let-bang) and do! (pronounced do-bang). The let extracts the underlying result of the Async<T>. If you position your pointer over the AsyncRead function, you find its return type is Async<byte>; while the variable data's type is byte[]. The do! is a special case of let!. It is used to handle the Async<unit> type where the return type is unit. The dol is used to start the asynchronous operation. The real computation is started when the operation variable is passed into the Async.StartWithContinuation function. StartWithinuation takes four parameters. The first is the asynchronous operation, and the other three are used to specify the normal callback function, exception-handler function, and user-cancellation handler, respectively.

The scattered code no longer exists for let! and do! You might be thinking that this sounds like the Async and await features in C# 5.0. If so, you are absolutely correct. F# has provided this functionality for many years, and the success of F# asynchronous workflows is the reason C# 5.0 introduces these features.