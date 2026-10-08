To report information about all devices in the current system, you can use the cuda devices
subcommand. Here is output from a system with two Fermi M2090 GPUs:

```
(cuda-gdb) info cuda devices
Desc SM Type Sms Warps/SM Lanes/Warp Max Reg/Lane Active SMs Mask
* 0 GF100GL sm_ 20 48 32 64 0x000003ff
  1 GF100GL sm_ 20 48 32 64 0x00000000
```

Note that a number of these subcommands duplicate functionality described earlier in the "CUDA
Focus" section of this chapter, and that all of these subcommands operate relative to the currentocus of cuda-gdb. However, a wider variety of metadata is accessible through the info cuda
command. But the cuda commands, and the info subcommands have their own owners
dending on the type and amount of information you are seeking.

# CUDA Debugging Tunable Parameters

cuda-gdb exposes a number of tunable parameters through the set subcommand that are useful for
tweaking cuda-gdb behavior:

```
(cuda-gdb) help set cuda
Generic command for setting gdb cuda variables
```

List of set cuda subcommands:

+   * set api_failures - Set the api_failures to ignore/stop/hide on CUDA driver
API call errors
* set break_on_launch - Automatically set a breakpoint at the entrance of
kernels
...

A list of useful tunables by cuda-gdb is summarized in Table 10-1. You can obtain
additional information about each of these parameters using help set cuda <tunable-name>. These parameters can be set using set cuda <tunable-name> <value>. The choice for
<value> for many commands is either on/off, but others have non-Boolean values.

| Table 10-1: CUDA-GDB Parameters |
| TUNABLE | DESCRIPTION | DEFAULT |
| --- | --- | --- |
| api_failures | Alters how cuda-gdb responds to error codes returned from\CUDA API functions | ignore |
| break_on_launch | Auto-sets a breakpoint at the start of every __global__\function launched by the user application or by the CUDA\nruntime | none |
| context_events | Controls informational messages on CUDA context creation\nand destruction | on |