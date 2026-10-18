![](bbox=[0.12, 0.11, 0.88, 0.48])

# FIGURE 7.3

The Intel® Many-Core Platform Software Stack (Intel® MPSS) showing the SCIF driver and user mode library.

# MEMORY REGISTRATION

Every process has a virtual address space (VAS). Virtual addresses (VAs) in this space are backed by physical pages by the operating system when a thread of that process faults on a read or write access. SCIF introduces the concept of a registered address space (RAS). This address space is sparse and only specific ranges which have been registered, via scif_register(), by the application, called registered windows or just windows, can be accessed by the remote peer of the process after a connection has been established. Figure 7.6 shows the relationship between the physical, virtual and RAS for a process. A set of physical pages (P) backs a virtual range (V) that is referenced by the window offset (W) in the RAS. A point worth noting is that the physical and VAS on the host processor and all the coprocessors are only accessible by a locally running process. The RAS, however, allows a process to access the physical memory backing it in the context of a remote process.

Put another way, use of scif_register() marks a region of memory ready for remote access. It takes a page aligned VA and a length parameter (plus some flags) and returns an offset that represents the window in the RAS of the process. Optionally, the offset can be chosen by the application and provided as an input to scif_register() by specifying the SCIF_MAP_FIXED flag. The physical pages that