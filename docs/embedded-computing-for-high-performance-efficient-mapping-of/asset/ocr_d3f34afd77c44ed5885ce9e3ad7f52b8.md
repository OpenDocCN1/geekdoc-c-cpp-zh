```
// create execution context
cl::Context context(device);

// create command-queue
cl::CommandQueue queue(context, device);

// load kernel source
#if defined(KERNEL1)
    ifstream fs("kernel1.cl");
#elif defined(KERNEL2)
    ifstream fs("kernel2.cl");
#endif

if (!fs.is_open()) {
    throw cl::Error(CL_INVALID_VALUE, "cannot open kernel source!");
}

stringstream ss;
ss << fs.rdbuf();
string code = ss.str();
cl::Program::Sources sources,
    sources.push_back({code.c_str(), code.length()});

// build
cl::Program program(context, sources);
try {
    program.build({device});
} catch (cl::Error e) {
    cout << program.getBuildInfo<CL_PROGRAM_BUILD_LOG>(device) << endl;
    throw e;
}
```

Next, we create buffers for matrices $A$ and $B$ with their respective sizes and submit a command through the command-queue of the device to copy matrices $A$ and $B$ from the host to the global memory of the device.

```
cl::Buffer bufA (context, CL_MEM_READ_ONLY, sizeof(float) * nx * ny);
cl::Buffer bufB (context, CL_MEM_READ_ONLY, sizeof(float) * ny * nz);
queue.enqueueWriteBuffer(bufA, CL_TRUE, 0, sizeof(float) * nx * ny, A);
queue.enqueueWriteBuffer(bufB, CL_TRUE, 0, sizeof(float) * ny * nz, B);
```

We then select the matrix multiplication ("mmul") kernel and set the kernel arguments. Note that in the case of kernel 2, we pass an extra argument, which is the local array.

```
cl::Kernel kernel = cl::Kernel(program,"mmul");
kernel.setArg(0, nx); kernel.setArg(1, ny); kernel.setArg(2, nz);
kernel.setArg(3, bufA); kernel.setArg(4, bufB); kernel.setArg(5, bufC);

#if defined(KERNEL2)
kernel.setArg(6, sizeof(float)*ny, NULL);
#endif
```

Finally, we execute the kernel by specifying the global and local dimensions and get the results back from global memory: