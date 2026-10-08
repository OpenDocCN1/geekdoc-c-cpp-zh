
Before debugging a CUDA application with cuda-gdb, you must first compile your program using special flags. This process is nearly identical to compiling host applications for debugging with gdb and similar tools. Simply add two flags to nvcc: -g and -G:

```
$ nvcc -g -G foo.cu -o foo
```

These flags embed debugging information for both host and device code, and turn off optimizations to ensure that your program state can be inspected during execution.

Once the application has been compiled with debug flags, you can launch a CUDA application with cuda-gdb just as you would with gdb. Given a compiled and linked application foo, you pass the executable to cuda-gdb, as follows:

```
$ cuda-gdb foo
```

```
(cuda-gdb)
```

This leaves you at the (cuda-gdb) prompt, meaning cuda-gdb has loaded symbols from the executable and is ready to execute. To run the program, simply type the command run. Command-line arguments can be included after the run command or set the set args command.

In general, cuda-gdb fully supports many of the features provided by gdb including breakpoints, watch-points, and the ability to inspect program state. However, cuda-gdb also provides CUDA-specific debugging functionality. A brief summary of these extensions and an example of their usage is provided in the following subsections.

## CUDA Focus

While CUDA applications can contain multiple host threads and many CUDA threads at a time, cuda-gdb debugging sessions only focus on a single thread. In order for you to debug multiple device threads in the same application, cuda-gdb supports the ability for you to specify the context (that is, the device thread) to be inspected. You can use cuda-gdb to report information about the current focus including the current device, current block, thread, and more.

For example, if the current focus of a cuda-gdb debugging session is on a CUDA thread executing the device, then you can retrieve the full focus of that by:

```
(cuda-gdb) cuda thread lane warp block sm grid device kernel
```

An example of this would be:

```
kernel 1026, grid 1027, block (0,0,0), thread (64,0,0), device 0, sm 1, warp 2,
lane 0
```

You can change focus to a different device thread using a similar syntax. In addition to the thread focus, you can provide a specific thread, for example, the 128th thread in the current block, using:

```
(cuda-gdb) cuda thread (128)
```

If you do not explicitly set focus properties, cuda-gdb will reuse the property values from the current focus.

You can obtain additional information about CUDA focus options using the gdb help command:

```
(cuda-gdb) help cuda
```

## Inspecting CUDA Memory

As with gdb, cuda-gdb supports inspecting variables, one on the heap (i.e., CUDA global memory) and in registers using the print statement:

```
(cuda-gdb) print scalar
(cuda-gdb) print arr[0]
(cuda-gdb) print (*arr) [3]
```

cuda-gdb can also be used to inspect CUDA shared memory. For example, to access the second word in shared memory using the following command:

```
(cuda-gdb) print *@shared int*)0x4
```

Note that shared memory is local to each SM, that statement might not evaluate to the same memory cell in every focus:

```
(cuda-gdb) cuda sm sm
s 1
(cuda-gdb) print *(@shared int*)0x4
$1 = 0
(cuda-gdb) cuda sm 8
[Switching focus to CUDA kernel 1026, grid 1027, block (18,0,0), thread
(0,0,0), device 0, sm 8, warp 0, lane 0]
27> int tid = blockDim.x + threadIdx.x;
(cuda-gdb) print *(@shared int*)0x4
$2 = 4
```

Hence, using cuda-gdb, you can inspect shared memory data.

## Getting Information about the Environment

You can use the gdb info command to retrieve information about the current CUDA environment and platform. A full list of environmental information can be found using:

```
(cuda-gdb) help info cuda
```

Print informations about the CUDA activities. Available options:
- dev : information about all the devices
- sms : information about all the SMs in the current device
- warps : information about all the warps in the current SM
- lanes : information about all the lanes in the current warp
- kernels : information about all the active kernels
- contexts : information about all the contexts
- blocks : information about all the active blocks in the current kernel
- threads : information about all the threads in the current kernel
- launch trace : information about the parent kernels of the kernel in focus
- children : information about the kernels launched by the kernels in focus
- managed : information about global managed variables

To report information about all devices in the current system, you can use the cuda devices subcommand. Here is output from a system with two Fermi M2090 GPUs:

```
(cuda-gdb) info cuda devices
Desc SM Type Sms Warps/SM Lanes/Warp Max Reg/Lane Active SMs Mask
* 0 GF100GL sm_ 20 48 32 64 0x000003ff
  1 GF100GL sm_ 20 48 32 64 0x00000000
```

Note that a number of these subcommands duplicate functionality described earlier in the "CUDA Focus" section of this chapter, and that all of these subcommands operate relative to the current focus of cuda-gdb. However, a wider variety of metadata is accessible through the info cuda command. But the cuda commands, and the info subcommands have their own owners depending on the type and amount of information you are seeking.

## CUDA Debugging Tunable Parameters

cuda-gdb exposes a number of tunable parameters through the set subcommand that are useful for tweaking cuda-gdb behavior:

```
(cuda-gdb) help set cuda
Generic command for setting gdb cuda variables
```

List of set cuda subcommands:

- set api_failures - Set the api_failures to ignore/stop/hide on CUDA driver API call errors
- set break_on_launch - Automatically set a breakpoint at the entrance of kernels
...

A list of useful tunables by cuda-gdb is summarized in Table 10-1. You can obtain additional information about each of these parameters using help set <tunable-name>. The choice for <value> for many commands is either on/off, but others have non-Boolean values.

| Table 10-1: CUDA-GDB Parameters | TUNABLE | DESCRIPTION | DEFAULT |
| :--- | :--- | :--- |
| api_failures | Alters how cuda-gdb responds to error codes returned from API functions | ignore |
| break_on_launch | Auto-sets a breakpoint at the start of every __global__ function launched by the user | none |
| context_events | Controls informational messages on context creation and destruction | on |
| defer_kernel_launch | Controls whether the debugger is notified of launches immediately. Disabling this option can improve debugging session performance | on |
| kernel_events | Controls how often launch or termination notifications are displayed by the application and/or runtime | none |
| launch_blocking | Sets all kernels to be synchronous | off |
| memcheck | Enables the memcheck memory checks as part of cuda-gdb | off |
| ptx_cache | Might enable saving the state of more variables in registers, allowing them to be printed from the debugger | on |
| single_stepping_optimizations | Safely accelerates single-stepping through a kernel | off before CUDA 5.5, on after 6.0 |
| thread_selection | Controls selection of CUDA focus. logical selects the thread with the lowest logical coordinates. physical selects the thread with the lowest physical coordinates. | logical |
| value_extrapolation | If enabled, cuda-gdb will get the value of any variables that are not live whose values might be saved in registers | off |

Manipulating these cuda-gdb parameters enables you to get more out of a cuda-gdb debugging session, customizing its behavior to fit your requirements.

To get some hands-on experience with cuda-gdb, download the example debug-segfault.cu. You will use it to experiment with debugging an invalid memory access in CUDA. First, build debug-segfault.cu using the Makefile, which will set the flags -g and -G. Next, load the application into cuda-gdb:

```
$ cuda-gdb ./debug-segfault
...
(cuda-gdb)
```

Use the run command to launch debug-segfault. It does not take any command-line arguments:
(cuda-gdb) run

You will likely see a large amount of scrolling text providing rich information about the CUDA context and kernel events occurring. Eventually, your debugging session will restore control back to you.
