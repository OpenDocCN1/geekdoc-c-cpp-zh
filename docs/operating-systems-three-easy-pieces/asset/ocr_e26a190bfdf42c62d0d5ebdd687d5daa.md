# THE ABSTRACTION: THE PROCESS

TIP: SEPARATE POLICY AND MECHANISM
In operating systems, a common design paradigm is to separate high-level policies from their low-level mechanisms [L+75]. You can think of the mechanism as providing the answer to a *how question* about a system; for example, *how does an operating system perform a context switch?* The policy provides the answer to a *which question*; for example, *which process should the operating system run right now?* Separating the two allows one easily to change policies without rethinking the mechanism and is thus a form of *modularity*, a general software design principle.

pointer are used to manage the stack for function parameters, local variables, and return addresses.
Finally, programs often access persistent storage devices too. Such I/O information might include a list of the files the process currently has.

# 4.2  Process API

Though we defer discussion of a real process API until a subsequent chapter, we first give some idea of what might be included in any interface of an operating system. These APIs, in some form, are available on any modern operating system.

+   * **Create**: An operating system must include method to create new processes. When you type a command into the shell, or double-click on an application icon, the OS is invoked to create a new process to run the process you have indicated.
* **Destroy**: As there is an interface for process creation, systems also provides an interface to destroy process forcibly. Of course, many processes will run and just exit by themselves when complete; they don't, however, the user may wish to kill them, and an interface to halt a running process is quite useful.
* **Wait**: It is useful to wait for a process to stop running; some kind of waiting interface is often.
* **Miscellaneous Control**: Other than killing or waiting for a process, there are some other controls that are possible. For example, most operating systems provide some kind of method to suspend a process (stop it from running for a while) and then resume it (continue running).
* **Status**: There are usually interfaces to get some status information about a process as well, such as long it has run for, or for what state it is in.

© 2008–19, ARPACI-DUSSEAU

THREE
ASY
PIECES