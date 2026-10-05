The K20 device has 5.03 GB of memory. This DRAM memory is directly connected to the graphics device (see figure 8.1). For a large-scale computation, 5 GB of memory may prove to be too little.

# 8.1.2 Host and device memory

To set up any computation on the graphics device, data must be transferred from host to memory. To retrieve the result of a computation on the graphics device, data must be transferred in the other direction from device to host memory. We use the following C++ class to transfer between host and device memory:

```
1 template<class type > class dhstmem{
2 private:
3 type *devicemem;
4 type *hostmem;
5 int n;
6 cudaError_t errorCode;
7 public:
8 dhstmem(long int nin){
9 ...
10 }
11 -dhstmem()
12 ...
13 }
14 type *device(){return devicemem};
15 type *hostmem(){return hostmem};
16 void device2host(){
17 ...
18 }
19 void host2device(){
20 ...
21 }
22 };
```

This class is templated. It can be used for data of type double, int, or some other type. The private section of the class is given in full on lines 3 to 6, but the definitions