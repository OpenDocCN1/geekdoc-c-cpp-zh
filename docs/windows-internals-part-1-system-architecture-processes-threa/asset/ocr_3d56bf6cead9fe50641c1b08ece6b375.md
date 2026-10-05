use) is separated from the work involved in creating a Windows subsystem process. So, although the following description of the flow of the Windows CreateProcess function is complicated, that part of the work is specific to the semantics addressed by the Windows subsystem as opposed to the core work needed to create an executive process object.

The following list summarizes the main stages of creating a process with the Windows CreateProcess functions. The operations performed in each stage are described in detail in the subsequent sections.

> Note Many steps of CreateProcess are related to the setup of the process virtual address and therefore refer to memory-management terms and structures that are defined in Chapter 5.

+   1. Validate parameters; convert Windows subsystem flags and options to their native counters; parse, validate, and convert the attribute list to its native counterpart.
2. Open the image file (.exe) to be executed inside the process.
3. Create the Windows executive process object.
4. Create the initial thread (stack, context, and Windows executive thread object).
5. Perform post-creation, Windows subsystem–specific process initialization.
6. Start execution of the initial thread (unless the CREATE_SUSPENDED flag was specified).
7. In the context of the new process and thread, complete the initialization of the address space (for example, load DLLs) and begin execution of the program's entry point.

Figure 3-10 shows an overview of the stages Windows follows to create a process.

![](bbox=[0.128, 0.606, 0.762, 0.905])

FIGURE 3-10 The main stages of process creation.