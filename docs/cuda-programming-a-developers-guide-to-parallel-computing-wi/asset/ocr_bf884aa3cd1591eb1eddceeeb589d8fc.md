Thrust provides two vector objects, host_vector and device_vector, which are used with C++ terminology to create an instance of these objects. For example,

```
thrust::host_vector <float> my_host_float_vector(200);
thrust::device_vector <int> my_device_int_vector(500);
```

In this code we declare two objects, one that physically resides on the host and one that will physically reside on the device.

The thrust:: part specifies a class namespace that you can largely think of as a library specifier in C. The host_vector and device_vector are functions (constructors) provided by the object. The <int> and <float> specifiers are passed to the constructor (the initialization function) for the object. The constructor then uses them along with the value passed into the function to allocate 200 elements of sizeof(float) and 500 elements of sizeof(int), respectively. Internally there may be other data structures, but at a high level this is effectively what you are doing when using such a C++ constructor.

Objects in C++ also have a destructor, a function that is called when the object goes out of scope. This function is responsible for deallocating any resources allocated by the constructor or during the runtime of the object. Thus, unlike C, it's not necessary to call free or cudaFree for Thrust vectors.

Having defined a vector you now need to get data into and out of the vector. A Thrust vector is conceptually simply a resizable array. Thus, a vector object provides a size() function that returns the number of elements in the vector. This allows you to use standard loop constructs, for example,

```
for (int i=0; i < my_device_int_vector.size(); i++)
{
    int x = my_device_int_vector[i];
    ...
}
```

In this example the array [] operator is being supplied by the class definition. Thus, in every iteration, a function is being called to transform i into a physical piece of data. Because of this, if the data happens to be on the device, Thrust will generate a transfer from the device to the host, in the background, which is completely hidden from the programmer. The size() function means the number of iterations is only known at runtime. As this can change within the loop body, it must be called on each loop iteration. This in turn prevents the compiler from statically unrolling the loop.

Depending on your view of such things, you'll either love it or hate it. The love it camp loves abstractions because they make programming easier and you don't have to care about the hardware. This camp is primarily made up of inexperienced programmers and people who simply want to get a calculation done. The hate it camp wants to know what is happening and is very keen to maximize performance from the hardware it has. They don't want to have a "simple" array dereference initialize a hugely inefficient 4-byte PCI-E transfer. They'd much prefer a far more efficient several-megabyte transfer to or from the device/host when they schedule it.

Thrust actually makes both camps happy. Large transfers are simply done by initiating a host vector with a device vector or vice versa. For example,

```
thrust::host_vector <float> my_host_float_out_vector
(my_device_float_results_vector.begin(), my_device_float_results_vector.end());
```