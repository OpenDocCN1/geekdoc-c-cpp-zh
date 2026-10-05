# Configuring the Environment Variables

After installing the CUDA Toolkit, it’s essential to configure your system’s environment variables. This will allow you to compile and run CUDA programs from the command line or your preferred IDE.

For Windows users, add the CUDA Toolkit’s bin directory to the PATH environment variable. For Linux and macOS users, the process involves editing your shell profile (e.g., .bashrc or .bash_profile) to include the following lines:

```
export PATH=/usr/local/cuda/bin:$PATH export
LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```

These commands make the CUDA compiler (nvcc) and libraries accessible system-wide.