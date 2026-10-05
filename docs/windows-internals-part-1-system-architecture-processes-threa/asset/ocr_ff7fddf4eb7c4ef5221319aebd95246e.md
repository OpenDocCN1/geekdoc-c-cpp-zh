If a user declines an elevation, Windows returns an access-denied error to process the launch. When a user agrees to an elevation by entering administrator credentials or clicking Yes, AIS calls CreateProcessAsUser to launch the process with the appropriate administrative identity. AIS is technically the parent of the elevated process, AIS uses new support in the CreateProcessAsUser API that sets the parent's process ID to that of the process originally launched it. That's why elevated processes don't appear in charts of the AIS service-hosting tools like Process Explorer that show process trees. Figure 7-28 shows the operations involved in launching an elevated process from a standard user account.

![](bbox=[0.159, 0.226, 0.642, 0.439])

**FIGURE 7-28** Launching an administrative application as a standard user.

# # Requesting administrative rights

There are a number of ways the system and applications identify a need for administrative rights. One that shows up in the Explorer interface is the Run as Administrator context menu command and shortcut option. These items also include a blue and gold shield icon should be placed next to any button or menu item that will result in an elevation of rights when it is selected. Choosing the Run as Administrator command causes Explorer to call the ShellExecute API with the run verbs.

The vast majority of installation programs require administrative rights, so the image loader, which initiates the launch of an executable, includes installer-detection code to identify legacy installers. Some of the heuristics it uses are as simple as detecting internal version information or whether the name has words install, or update in its name. More sophisticated methods of detection involve scanning for byte sequences that are common to third-party installation wrappers. The image loader also calls the application-compatibility library to see if the target executable requires administrator rights. The library looks in the application-compatibility database to see whether the executable has the ReqAdministrator or RunAsInvoker flag associated with it.

The most common way for an executable to request administrative rights is for it to include a requestedExecutionLevel tag in its application manifest file. The element’s level attribute can have one of the three values shown in Table 7-17.