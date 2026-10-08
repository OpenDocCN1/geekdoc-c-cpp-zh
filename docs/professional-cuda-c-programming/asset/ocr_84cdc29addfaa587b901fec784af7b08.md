# TABLE 8-5 (continued)

| CLAUSE | BEHAVIOR IN A PARALLEL REGION | BEHAVIOR IN A KERNELS REGION |
|---|---|--|\| device_type(type) | Acts as a demarcator between clause lists for different device types. All clauses following a device_type and until the end of the directive or the next device_type clause apply when the loop is being run on the specified device type. | Same as parallel |
| independent | Asserts that the marked loop is parallelizable, overriding compiler analysis. | Same as parallel |
| private(var, ...) | Create grant-private copies of each of the specified variables for the marked loop. | Same as parallel |
| reduction | See the discussion of reduction earlier in this section. | Same as parallel |

You can also combine the **loop directive** with *parallel* or *kernels* in a single **pragma**:

```
#pragma acc parallel loop
for (i = 0; i < N; i++) {
}

#pragma acc kernels loop
for (i = 0; i < N; i++) {
}
```

These are simply shortcut directs that expand to *parallel* and *kernels* directives that are immediately followed by a loop directive:

```
#pragma acc parallel
{
#pragma acc loop
for (i = 0; i < N; i++) {
  
}
}
#pragma acc kernels
{
#pragma acc loop
for (i = 0; i < N; i++) {
  
}
}
```