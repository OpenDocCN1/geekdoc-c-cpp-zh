# The Windows Driver Foundation

The Windows Driver Foundation (WDF) is a framework for developing drivers that simplifies common tasks such as handling Plug and Play and IRPs correctly. WDF includes the Kernel-Mode Driver Framework (KMDF) and the User-Mode Driver Framework (UMDF). WDF is now open source and can be found at https://github.com/Microsoft/Windows-Driver-Frameworks. Table 6-9 shows the Windows version support (for Windows 7 and later) for KMDF. Table 6-10 shows the same for UMDF.

KMDF versions

| KMDF Version | Release Method | Included in Windows | Drivers Using It On |
|---|---|---|---||
| 1.9 | Windows 7 WDK | Windows 7 | Windows XP and later |
| 1.11 | Windows 8 WDK | Windows 8 | Windows Vista and later |
| 1.13 | Windows 8.1 WDK | Windows 8.1 | Windows 8.1 and later |
| 1.15 | Windows 10 WDK | Windows 10 | Windows 10, Server 2016 |
| 1.17 | Windows 10 1511 WDK | Windows 10 1511 | Windows 10 1511 and later, Windows Server 2016 |
| 1.19 | Windows 10 1607 WDK | Windows 10 1607 | Windows 10 1607 and later, Windows Server 2016 |

TABLE 6-10 UMDF versions

| UMDF Version | Release Method | Included in Windows | Drivers Using It On |
|---|---|---|---||
| 1.9 | Windows 7 WDK | Windows 7 | Windows XP and later |
| 1.11 | Windows 8 WDK | Windows 8 | Windows Vista and later |
| 2.0 | Windows 8.1 WDK | Windows 8.1 | Windows 8.1 and later |
| 2.15 | Windows 10 WDK | Windows 10 | Windows 10 and later, Windows Server 2016 |
| 2.17 | Windows 10 1511 WDK | Windows 10 1511 | Windows 10 1511 and later, Windows Server 2016 |
| 2.19 | Windows 10 1607 WDK | Windows 10 1607 | Windows 10 1607, and later, Windows Server 2016 |

UMDF 10 introduced the concept of Universal Drivers, briefly described in Chapter 2, "System architecture." These drivers use a common set of DDIs implemented in multiple editions of Windows 10—from IoT Core, to Mobile, to desktops. Universal drivers can be built with KMDF, UMDF 2.x, or WDM. Building such drivers is relatively easy with the aid of Visual Studio, where the Target Platform setting is set to Universal.

UMDF versions 1.x used a COM based model for programming drivers, which is a very different programming than KMDF, which uses object-based C. UMDF 2 has been aligned with KMDF and provides an identical API, reducing overall cost associated with WDF driver development; UMDF 2.x can be converted to KMDF if the need arises with little work. UMDF 1.x will not be discussed in this book; consult the WDK for more information.