```
// Force garbage collection
GC.Collect();
GC.WaitForPendingFinalizers();
Console.WriteLine("GC forced manually.");
}
static void CreateAndForget() {
Test t = new Test();
// 't' goes out of scope here, eligible for GC
}
}
```

![](bbox=[0.12, 0.54, 0.22, 0.59])

# [Execution Result]

Finalizer called.

GC forced manually.

![](bbox=[0.12, 0.86, 0.22, 0.91])

Normally, C#'s garbage collector runs automatically in the background. It decides the best time to clean up unused memory to avoid performance issues.