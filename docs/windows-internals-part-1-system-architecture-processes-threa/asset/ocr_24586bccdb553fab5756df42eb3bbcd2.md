> Note Drivers installed using setup programs that manually configure the registry and copy driver files to a system and driver files that are dynamically loaded by applications aren't checked for signatures by the PnP manager's signing policy. Instead, they are checked by the kernel-mode code-signing policy described in Chapter 8 in Part 2. Only drivers installed using INF files are validated against the PnP manager's driver-signing policy.

> Note The user-mode PnP manager also checks whether it's about to install is on the protected driver list maintained by Windows Update and, if so, the installation with a warning to the user. Drivers that are known to have incompatibilities or bugs are added to the list and blocked from installation.

# General driver loading and installation

The preceding section showed how drivers for hardware devices are discovered and loaded by the PnP manager. These drivers mostly load "on demand," meaning a driver is not loaded unless needed—a device that the driver is responsible for the system; conversely, if devices managed by a driver are removed, the driver will be unloaded.

More generally, the Software key in the registry holds settings for drivers (as well as Windows Services). Although services are managed within the same registry key, they are user-mode programs and have no connection to kernel drivers (although the Service Control Manager can be used to load both services and device drivers). This section focuses on drivers; for a complete treatment of services, Chapter 9 in Part 2.

# Driver loading

Each subkey the Software key (HKLM\System\CurrentControlSet\Services) holds a set of values that control some aspects of a driver (or service). One value, ImagePath, was encountered already when we discussed the loading process of PnP drivers. Figure 6–36 shows an example of a driver key and 6–8 summarizes the most important values in a driver's Software key (see Chapter 9 in Part 2 for a complete list).

The Start value indicates the phase in which a driver (or service) is loaded. There are two main differences between device drivers and services in this regard:

+   - Only device drivers can specify Start values of boot-start (0) or system-start (1). This is because at these phases, no user mode exists yet, so services cannot be loaded.

+   - Device drivers can use the Group and Tag values to control the order of loading within a phase of the boot, but unlike services, they can't specify DependOnGroup or DependOnService values (see Chapter 9 in Part 2 for more details).