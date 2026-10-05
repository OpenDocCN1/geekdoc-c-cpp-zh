# Win32-Internals www.sysinternals.com

| Name | Type |
| --- | --- |
| {GUID}-P(ID)D112-TD(1308) 567a5d3-aab0-4569-9c6222242... | ALPC Port |
| {GUID}-P(ID)D112-TD(1308) 57623c55-efae-4fc0-a2c8-8c2b876... | ALPC Port |
| App_AmendedContainer | Event |
| App_Cc_000002b7 | Event |
| App_CS_000003b6 | Semaphore |
| Section | Event |
| BuildTreeCreated | Event |
| Section | Semaphore |
| DefragmentationOperationsComplete | Event |
| DownloadStarted | Event |
| Section | SymbolicLink |
| | | BaseNamedObjects |

+   - 3-1-5-1062537810-19541251-109421509
- 3-1-5-1190255376-27554773-70261612-10
- 3-1-5-1190247398-121934718-123046713-20394246
- 3-1-5-1190247398-121934718-123046713-20394246
- 3-1-5-2204069669-325473807-219533710-20394246
- 3-1-5-2235517699-235553858-235553858-24861161
- 3-1-5-2235517699-235553858-235553858-24861161
- 3-1-5-3117335332-193553452-103778396-24861161
- 3-1-5-467716838-377386951-273833692-24861161

FIGURE 7-19 Object manager directory for Calculator.
-3-1-5-467716838-377386951-273833692-427270567-108733535-24861161

Outside of official broker services, a desktop app can create a named (or even unnamed) object normally, and then use the DllCreateHandle function to inject into the same object as the UWP process manually. This works because desktop apps typically run with medium integrity level and there's nothing preventing them from duplicating handles within UWP processes—unless the other way.

> Communication between a desktop app and a UWP is not usually required because a store app cannot have a desktop companion, and cannot rely on such an app to exist on the device. The capacity to inject into a UWP app may be needed in specialized cases such as using the desktop bridge (Centennial) to convert a desktop app to a UWP app and communicate with another app that is known to.

# AppContainer and handles

In a typical Win32 application, the persistence of the session-local and global BaseNamedObjects directory is guaranteed by the Windows subsystem, as it creates this on boot and session creation. Unfortunately, the AppContainerBaseNamedObjects directory is directly created by the launch instance. In the case of UWP application, this is the trusted DC launch, but not all AppContainers are necessarily tied to UWP. They can also be manually created through the process-create attributes (See Chapter 3 for more information on which one to use). In this case, it's possible for an untrusted application to have created the object directory (and symbolic links within it), which would result

CHAPTER 7 Security 705