call to host_mic(). At exit from the offload construct, the array v[] is scaled by $4^{2/3}$
onon both the host and the MIC device.

The function call hostmic_scale() on line 21 on the host. At the end of
this, the array v[] is scaled by 4 on the host and by $4^{2/3}$ on the MIC device.

The definition of leibniz3() is completed as follows:

```
22 double sum;
23 #pragma offload target(mic:0) \
24 in(v)length(n) align(64) alloc_if(0) free_if(1)
25 sum = hostmic_sum(v
```

Notice that the clause (line 24) v[] copies from host to MIC. The array v[]
scaled by 4 on the host but only $4^{2/3}$ on the MIC device. Therefore, a copy is
essential if we are to get the correct value of $\pi$. Here v[] is freed from the MIC device
on exit. The sum is computed on the MIC device on line 25.

# Host and MIC pointers

The function leibniz3() shows the close connection between the array v[] stored
on the host and its counterpart on the MIC device. The function prints the pointer
v the host (line 10). There are three calls to hostmic_scale() (lines 16, 19, and
21), two of them from the MIC device and one from the host. Each of these
prints the value of the pointer. The following lines are printed:

```
host pointer v = 0x2af1d0000040
scale:host/mic pointer v = 0x7fe5cd07040
scale:host/mic pointer v = 0x7fe5cd07040
scale:host/mic pointer v = 0x2af1d0000040
```

Evidently, the pointer has a different value on the host and the MIC, although it has
same name in the program.
Entry during an offload region, the host needs to know the value of the pointer
on the MIC device to set up function calls correctly and to implement clauses such