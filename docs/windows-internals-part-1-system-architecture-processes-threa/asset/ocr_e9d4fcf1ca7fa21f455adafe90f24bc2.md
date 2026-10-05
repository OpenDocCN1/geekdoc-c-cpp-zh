Other examples of architecture-specific code in the kernel include the interfaces to provide buffer and CPU cache support. This support requires different code for the different architectures because of the ways caches are implemented.

Another example is context switching. Although at a high level the same algorithm is used for thread selection and context switching (the context of the previous thread is saved, the context of the new thread is loaded, the new thread is started), there are architectural differences among the implementations on different processors. Because the context is described by the processor state (registers and on), what is saved and loaded varies depending on the architecture.

# Hardware abstraction layer

As mentioned at the beginning of this chapter, one of the crucial elements of the Windows design is its portability across a variety of platforms. With OneCore and the myriad device forms available, this is more important than ever. The hardware abstraction layer (HAL) is a key part of making this portability possible. The HAL is a loadable kernel-module (Hal.dll) that provides the low-level interface to the hardware platform on which Windows is running. It hides hardware-dependent details as I/O interfaces, interrupt controllers, and microprocessor communication mechanisms—any functions that are architecture-specific and machine-dependent.

So rather than accessing hardware directly, Windows internal components and user-written drivers maintain portability by calling the HAL routines when they need platform-dependent information. For this reason, many HAL routines are documented in the WDK. To find out more about the HAL and its use by device drivers, refer to the WDK.

A couple of x86 HALs are included in a standard desktop Windows installation (as shown in Table 2-4), Windows has the ability to detect at boot-time which HAL is used, eliminating the problem that existed on earlier versions of Windows when attempting to boot an installation on a different kind of system.

| HAL File Name | Systems Supported |
| Halacpi.dll | Advanced Configuration and Power Interface (ACPI) PCs. Implies uniprocessor-only machine, without APIC support. (The presence of either one would make the system use the HAL below instead.) |
| Halmacpi.dll | Advanced Programmable Interrupt Controller (APIC) PCs with an ACPI. The existence of an APIC implies SMP support |

On x64 and ARM machines, there is only one HAL image, called Hal.dll. This results from having the same motherboard configuration, because the processors require ACPI and APIC support. Therefore, there is no need to support machines without ACPI or with a standard PIC. Similarly, all ARM systems use ACPI and interrupt controllers, which are similar to a standard APIC. Once again, a single HAL can support this.

On the other hand, although interrupt controllers are similar, they are not identical. Additionally, the actual timer and memory/DMA controllers on some ARM systems are different from others.