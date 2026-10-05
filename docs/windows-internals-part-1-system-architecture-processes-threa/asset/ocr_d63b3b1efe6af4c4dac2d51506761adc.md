# TABLE 5-23 Limitations on physical memory support in Windows

| Operating System Version/Edition | 32-Bit Maximum | 64-Bit Maximum |
|---|---|--|
| Windows 8.x Professional and Enterprise | 4 GB | 512 |
| Windows 8.x (all other editions) | 4 GB | 128 GB |
| Windows Server 2012/R2 Standard and Datacenter | N/A | 4 TB |
| Windows Server 2012/R2 Essentials | N/A | 64 GB |
| Windows Server 2012/R2 Foundation | N/A | 32 GB |
| Windows Storage Server 2012 Workgroup | N/A | 32 GB |
| Windows Storage Server 2012 Standard Hyper-V Server 2012 | N/A | 4 TB |
| Windows 10 Home | 4 GB | 128 GB |
| Windows 10 Pro, Education and Enterprise | 4 GB | 2 TB |
| Windows Server 2016 Standard and Datacenter | N/A | 24 TB |

At the time of this writing, the maximum supported physical memory is 4 TB on Server 2012/R2 editions and 24 TB on Server 2016 editions. The limitations don't come from any implementation or hardware limitation, because Microsoft will support only configurations it can test. As of this writing, these were the largest and supported memory configurations.

# Windows client memory limits

64-bit Windows client editions support different amounts of memory as a differentiating feature, with the low end being 4 GB increasing to 2 TB for Enterprise and Professional editions. All 32-bit Windows client editions, support a maximum of 4 GB of physical memory, which is the highest physical address accessible with the standard x86 memory management mode.

Although client SKUs PAE addressing modes on x86 systems in order to provide hardware no-execution protection (which would allow access to more than 4 GB of physical memory), revealing that systems would crash, hang, or become unbootable some device drivers, commonly those for video and audio devices found on clients but not servers, were not programmed to expect physical addresses larger than 4 GB. As result the drivers truncated addresses, resulting in memory corrections and corruption side effects. Server systems commonly have more generic, with simpler and more stable drivers, and therefore had not generally revealed these problems. The problematic client ecosystem led to the decision for client editions to ignore physical memory that remains above 4 GB, even though they could theoretically address it. Driver developers are encouraged to test their systems with the nomem option, which will force the kernel to use physical addresses above 4 GB only if sufficient memory exists on the system to allow it. This will immediately lead to the detection of such issues in faulty drivers.

Although 4 GB is the licensed for 32-bit clients, the effective limit is actually lower and depends on the system's chipset and connected devices. This is because the physical address map includes not only RAM but also device memory, and x86 and x64 systems map all device memory below the 4 GB address boundary to remain compatible with 32-bit operating systems that don't