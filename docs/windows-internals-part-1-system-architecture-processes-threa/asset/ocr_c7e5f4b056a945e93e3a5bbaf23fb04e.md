packageQuery(S-1-S-15-1024-1926-68429891-68847262-357147821-362867630-80258028-
192256387-202611640-333523193) (ENABLED)
elQueryLicenseValue(S-1-S-15-1024-357870329-384271876-7859573-193084442-
249799616-291701580-1780209906-4415419541) (ENABLED)
-1-S-13-186189761-665163147-292754265-642690995-32784025-265974315-263031742
(ENABLED)
-1-S-13-377848524-120972858-355853632-1059889664 (ENABLED)
-1-S-13-3215430884-133981692-98275616-1145831019 (ENABLED)
-1-S-13-307167614-134410966-9840074-11750610-358415017 (ENABLED)
-1-S-53-99315259-124458892-284007664-355328420 (ENABLED)
-1-S-13-3078010518-1154311996-9966967-30170930-4117416952
-1-S-13-210144330-123101406-402110719-248794518 (ENABLED)
-1-S-13-2345035981-117411712-53288075 (ENABLED)
-1-S-15-363849274-1266744000-199443125-2376837358 (ENABLED)
-1-S-15-2569730672-109526119-535273203-1209357796 (ENABLED)
-1-S-15-245236844-125748821-2818397580-3350426111 (ENABLED)

Output the package name, executable directory, AppContainer SID, publisher information, version, and list of capabilities. Also shown is the LowerBox number, which is just a local index of the app.

Lastly, you can inspect these properties in the kernel debugger with the :token command.

UWP apps are called trusted, although they use the Windows runtime like other U apps, which do not run inside an AppContainer and have an integrity level higher than low. The canonical system is the Settings app %SystemRoot%\ImmersiveControlPanel\Settings.exe; this seems reasonable, as the Settings app must be able to make changes to the system that would be impossible to do from an AppContainer-hosted process. If you look up its token, you will see three attributes—PKG, SYSAPP, and PKHOSTID—which confirms that it is a packaged application, even without the AppContainer token.

# AppContainer and object namespace

Desktop applications can share kernel objects by name. For example, suppose process A creates an event by calling CreateEvent(Ex) with the name MyEvent. It gets back a handle to it later to manipulate it. Process B running in the same session can call CreateEvent (Ex) or OpenEvent with the same name, MyEvent, and assuming it has appropriate permissions, which is usually the case if running under the same session) get another handle to the underlying event object. Now if process A calls SetEvent on the event while process B was blocked in a call to WaitForSingleObject on its event process, process B's waiting would be released because it is the same event object. This sharing works because objects are created in the object manager directory Sessions\BaseNamedObjects, as shown in Figure 7-18 with the WinObj prefixed with Global\.

Furthermore, desktop apps can share objects between sessions by using a name in Global\. This creates the object in the session 0 object directory located in BaseNamedObjects (refer to Figure 7-18).