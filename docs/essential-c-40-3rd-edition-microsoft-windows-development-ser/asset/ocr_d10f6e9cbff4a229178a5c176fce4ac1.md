# Output 18.5:

```
Push ENTER to exit.
31.415926535897932384626433832795028841971693993751058209749445923078164
0A62B4B6796E810B3D5295291770879B2140B06513282D06A470938446095505822317253
97402062A1B17F0
*****************************************************************
2
```

Rather, the Cancel() call sets the IsCancellationRequested property on all cancellation tokens copied from CancellationTokenSource.Token. There are a couple things to note from the previous sentence.

+   - Cancellation token: A CancellationToken, not a CancellationTokenSource, is evaluated in the asynchronous task. A CancellationToken is seemingly similar to the CancellationTokenSource except that the CancellationToken is for monitoring and responding to a cancellation request while the CancellationTokenSource is for canceling the task itself (see Figure 18.2).
+   - Copied: A CancellationToken is a struct, so calling CancellationTokenSource.Token will create a copy of the token. As a result, all instances of the cancellation token will be thread-safe.

![](bbox=[0.2, 0.59, 0.85, 0.88])

# FIGURE 18.2: CancellationTokenSource and CancellationToken Class Diagrams