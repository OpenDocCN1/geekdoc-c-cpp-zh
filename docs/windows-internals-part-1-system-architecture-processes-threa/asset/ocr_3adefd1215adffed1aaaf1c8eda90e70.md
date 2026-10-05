# Task Manager

| Name | PID | Status | CPU | UAC virtualiz... |
| --- | --- | --- | --- | --- |
| Eego.Service... | 3792 | Running | 02 bit | Not Allowed |
| EpcMonto... | 13724 | Running | 02 bit | Disabled |
| self_assist_ga_... | 3728 | Running | 64 bit | Disabled |
| self_uf_exe | 3636 | Running | 64 bit | Not Allowed |
| Evnt.exe | 00 | Running | 64 bit | Disabled |
| explorer.exe | 9188 | Running | 64 bit | Disabled |
| FileCoAuth.exe | 10168 | Running | 32 bit | Enabled |
| firefox.exe | 17376 | Running | 32 bit | Disabled |
| firefox.host... | 16400 | Running | 32 bit | Disabled |
| fortondh... | 25900 | Running | 64 bit | Not Allowed |
| Whatdef.exe | 7288 | Running | 64 bit | Not Allowed |
| HidMoniti_S... | 3492 | Running | 64 bit | Not Allowed |
| HPVewer.exe | 13132 | Running | 32 bit | Disabled |
| HPNotificat... | 11034 | Running | 64 bit | Not Allowed |
| hqpwmxie.exe | 8792 | Running | 32 bit | Not Allowed |
| hqpwmxie.exe | 14984 | Running | 64 bit | Not Allowed |
| HPSupport... | 1748 | Running | 32 bit | Not Allowed |
| IAStorData... | 14603 | Running | 32 bit | Disabled |
| ibtisa.exe | 3516 | Running | 64 bit | Not Allowed |
| explore.exe | 12652 | Running | 64 bit | Disabled |
| explore.exe | 16460 | Running | 64 bit | Enabled |
| igfxCUIServic... | 00 | Running | 64 bit | Not Allowed |
| IpOverUdsV... | 3532 | Running | 32 bit | Not Allowed |

FIGURE 7-22 Using Task Manager to view virtualization status.

| Flag | Meaning |
| --- | --- |
| ElevateCreateProcess | This CreateProcess to handle ERROR_ELEVATION_REQUIRED errors by calling the application service to prompt for elevation. |
| ForceAdminAccess | This spoofs queries of Administrator group membership. |
| VirtualizeDeleteFile | This spoofs successful deletion of global files and directories. |
| LocalMappedObject | This forces global section objects into the user's namespace. VirtualizeHKCRite This redirects global registration of COM objects to a per-user location. VirtualizeRegisterTypeLib | This converts per-machine typelib registrations to per-user registrations. |