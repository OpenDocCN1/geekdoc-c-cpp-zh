```
// copy B to the accelerator asynchronously, with ID 0
#pragma acc enter data copyin(B[0:N]) async(0)
```

```
// do work on the host
do_some_heavy_work(C);
```

```
// execute this block of code asynchronously on the accelerator.
// use wait(0) to ensure that it waits for the transfer of B to complete first.
#pragma acc kernels async(1) wait(0)
{
    for (i = 0; i < N; i++) {
        A[i] = do_work(B[i]);
    }
}
```

```
// copy A to the host after the kernels region finishes
#pragma acc exit data copyout(A[0:N]) async(2) wait(1)
```

```
// do work on the host
do_lots_more_work(D);
```

```
// wait for the transfer of A to finish
#pragma wait(2);
```

Here, the data directive is used to asynchronously transfer B to the device, with do_some_heavy_work. The kernels directive then uses wait to ensure that the asynchronous copy of B completes and launches an asynchronous computational task. The exit data directive is used to transfer A back asynchronously, with do_lots_more_work waiting for the kernels region to complete first. Finally, a wait directive must be used to ensure that A has been transferred to the host.

Like kernels and parallel, the data directives support and share a variety of clauses. A list of supported clauses and the directives with which they can be used is shown in Table 8-6.

# TABLE 8-6: Data Clauses

| CLAUSE | BEHAVIOR | SUPPORTED BY? |
| --- | --- | --- |
| | | DATA ENTER EXIT DATA |
| if (cond) | Only perform the copies if cond is true. | Y Y Y |
| copy (var1, ...) | The variables listed should be copied to the accelerator at the start of the data region and back at the end. | Y N N |
| copyin (...) | The variables listed should only be copied to the accelerator. | Y Y N |
| copyin (var1, ...) | The variables listed should only be copied to the accelerator. | Y Y N |
|