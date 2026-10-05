+   A callback whenever a fault during a probe and lock operation on a memory descriptor list
(MDL) occurs inside a Pico thread

+   A callback whenever a caller is requesting the name of a Pico process

+   A callback whenever Event Tracing for Windows (ETW) is requesting the user-mode stack trace
a a Pico process

+   A callback whenever an application attempts to open a handle to a Pico process or Pico thread

+   A callback whenever someone requests the termination of a Pico process

+   A callback whenever a Pico thread or Pico process terminates unexpectedly

Additionally, a Pico provider leverages Kernel Patch Protection (KPP), described in Chapter 7,
to protect its callbacks and system calls as well as prevent fraudulent or malicious Pico providers
from registering on top of a legitimate Pico provider.

It now becomes clear that with such unparalleled access to any possible user-kernel transition or vis-
ner-kernel interactions between a Pico process/thread and the world, it can be fully encapsulated
a a Pico provider (and relevant user-mode libraries) to wrap a completely kernel imple-
tation that of Windows (with some exceptions, of course, as scheduling rules and memory
management rules, such as commit, still apply). Correctly written applications are not supposed to be
sensitive to internal algorithms, as they are subject to change even within the operating system
normally execute.

Therefore, Pico providers are essentially custom-written kernel modules that implement the neces-
sary callbacks to respond to the list of possible events (shown earlier) that a Pico process can cause to
arise. This is how WSL is capable of running unmodified Linux binaries in user-mode, limited only
by the completeness of its system call emulation and related functionality.

To complete the picture on regular NT processes versus minimal processes versus Pico processes,
Figure 3-8, showing the different structures for each.

![](bbox=[0.128, 0.655, 0.673, 0.923])

Figure 3-8 Process types.