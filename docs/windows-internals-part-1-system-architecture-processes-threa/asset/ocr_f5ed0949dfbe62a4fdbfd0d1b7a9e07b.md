mechanisms (such as SafeDisc and SecuROM) and disable execution protection to provide compatibility with other copy-protected software such as computer games. (See Chapter 3 for more information about the image loader).

# EXPERIMENT: Looking at DEP protection on processes

Process Explorer can show the current DEP status for all the processes on your system, including whether the process is opted in or benefiting from permanent protection. To look at the DEP status, right-click any column in the process tree, choose Select Columns, and then select DEP Status on the Process Image tab. There are three possible values:

+   - DEP (permanent) This means the process has enabled DEP because it is a "necessary Windows program or service."

+   - DEP This means the process opted in DEP. This may be due to a system-wide policy to opt in for all 32-bit processes, because of an API call such SetProcessDEPPolicy or because the /COMPAT linker flag was set when the image was built.

+   - Nothing If the column displays no information for this process, DEP is disabled because either a system-wide policy or an API call or shim.

Additionally, to provide compatibility with older versions of the ATL Framework (version 7.1 or earlier), the Windows kernel provides an ATL emulation environment. The environment detects ATL thread code that have caused the DEP exception and emulates the expected operation. Application developers can request that ATL emulation not be applied using the latest Microsoft C++ compiler and specifying the /COMPAT flag (which sets the IMAGE_DLL_NX_COMPAT flag in the PE header), which tells the system that the executable fully supports DEP. DEP emulation is disabled if the AlwaysOn value is set.

Finally, if the system is in OptIn or OptOut mode and executing a 32-bit process, the SetDEPPolicy allows a process to dynamically disable DEP or to permanently enable it. When is enabled through this API, DEP cannot be disabled programmatically. This function can also be used to dynamically disable ATL emulation if the image wasn't compiled with the /COMPAT flag. On 64-bit processes or systems with AlwaysOff or AlwaysOn, the function always returns a failure. The GetProcessDEPPolicy function returns the 32-bit process DEP policy (it fails on 64-bit systems, where the policy is the same—always), GetSystemDEPPolicy can be used to return a value corresponding to the policies in Table 5-3.

# Copy-on-write

Copy-on-write page protection is an optimization the memory manager uses to conserve physical memory. When a process maps a copy-on-write view of a section that contains read/write pages, the memory manager delays the copying of pages until the page is written instead of making a private copy at the time the view is mapped. For example, in Figure 5-4, two processes are sharing three pages, marked copy-on-write, but neither of the two processes has attempted to modify any data of the pages.

CHAPTER 5 Memory management