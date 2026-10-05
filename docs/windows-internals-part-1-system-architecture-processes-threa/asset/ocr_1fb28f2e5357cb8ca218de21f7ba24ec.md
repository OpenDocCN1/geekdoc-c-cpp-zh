+   A non-Plug Play driver or file-system driver that doesn't have to be present when the system boots a Start value of auto-start (2). An example is the Multiple Universal Naming Convention (UNC) Provider (MUP) driver, which provides support for UNC-based path names to remote resources (for example, \RemoteComputerName\SomeShare).

+   Plug and Play drivers that aren't required to boot the system specify a Start value of demand-start (3). Examples include network adapters drivers.

The only purpose is that the Start values for Plug and Play drivers and drivers for enumerable devices have to ensure that the operating system loads the driver—if the driver is required for the system to boot successfully. Beyond that, the PnP manager's device enumeration processes the load order for Plug and Play drivers.

# Driver installation

As we've seen, Plug and Play drivers require an INF for installation. The INF includes the hardware IDs this driver can handle and the instructions for copying files and registry values. Other type of drivers (such as file system drivers, file system filters and network filters) require an INF as well, which includes a unique set of values for the particular type of driver.

Software-only drivers (such as the one Process Explorer) can use an INF for installation, but don't have to. These can be installed by a call to the CreateService API or a tool such as sc.exe that wraps it, as Process Explorer extracts its driver from a resource within the executable (if running with elevated permissions). The API name suggests, is used to install services as well as drivers. The arguments to CreateService indicate whether it's installing a driver or a service, the Start value and other parameters (see the Windows SDK documentation for the details). Once installed, a call to StartService loads the driver (or service), calling DriverEntry(for a driver) as.

A software-only driver creates a device named a name it chooses. For example, Process Explorer creates a device named PROCEP152 that is then used by Process Explorer in a Create-F1e1 call, called by such as DeviceIoControl to request the driver (turned into IRPs by the I/O manager). Figure 6-4 shows the Process Explorer symbolic link (using the WinObj Sysinternals to \GLOBAL?? (recall that the names in this directory are accessible to user mode clients) that created by Process Explorer the first time it's running with elevated privileges. Notice that it points to the device object \Device directory and has the same name (which is not a requirement).

![](bbox=[0.151, 0.755, 0.715, 0.915])

FIGURE 6-4 Process Explorer symbolic link and device.