| Category | Variable | Values | Description |
| :--- | :--- | :--- | :--- |
| | | (default is FASTEST_FIRST) | heuristic, and make that device 0, leaving the order of the rest of the devices unspecified. PCI_BUS_ID orders devices by PCI bus ID in ascending order. |
| Compilation | CUDA_CACHE_DISABLE | 0 or 1 (default is 0) | Disables caching (when set to 1) or enables caching (when set to 0) for just-in-time compilation. When disabled, no binary code is added to or retrieved from the cache. |
| | CUDA_CACHE_PATH | filepath | Specifies the folder where the just-in-time compiler caches binary codes; the default values are:
> on Windows, %APPDATA%\NVIDIA\ComputeCache,
> on MacOS, $HOME/Library/Application Support/NVIDIA/ComputeCache,
> on Linux, ~/.nv/ComputeCache |
| | CUDA_CACHE_MAXSIZE | integer (default is 268435456 (256 MiB) and maximum is 4294967296 (4 GiB)) | Specifies the size in bytes of the cache used by the just-in-time compiler. Binary codes whose size exceeds the cache size are not cached. Older binary codes are evicted from the cache to make room for newer binary codes if needed. |
| | CUDA_FORCE_PTX_JIT | 0 or 1 (default is 0) | When set to 1, forces the device driver to ignore any binary code embedded in an application (see Application Compatibility) and to just-in-time compile embedded PTX code instead. If a kernel does not have embedded PTX code, it will fail to load. This environment variable can be used to validate that PTX code is embedded in an application and that just-in-time compilation works as expected to guarantee application forward compatibility with future architectures (see Just-in-Time Compilation). |
| Execution | CUDA_LAUNCH_BLOCKING | 0 or 1 (default is 0) | Disables (when set to 1) or enables (when set to 0) asynchronous kernel launches. |
| | CUDA_DEVICE_MAX_CONNECTIONS | 1 to 32 (default is 8) | Sets the number of compute and copy engine concurrent connections (work queues) from the host to each device of compute capability 3.5 and above. |
| | CUDA_AUTO_BOOST | 0 or 1 | Overrides the autoboost behavior set by the -auto-boost default option of nvidia-smi. If an application requests via this environment variable a behavior that is different from nvidia-smi, its request is honored if there is no other application currently running on the |