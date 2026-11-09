These last three settings are equivalent to the `LegacyAuthenticationLevel`, `LegacyImpersonationLevel`, and `LegacySecureReferences` settings in the `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Ole` registry key. These were discussed in Chapter 8. The settings are called legacy settings because newer COM+ objects should call `CoInitializeSecurity()` to set these settings. Legacy COM+ objects created before DCOM+ did not call this function because it was not available. COM+ uses these legacy settings when calling `CoInitializeSecurity()` on behalf of these legacy objects.

# Default Security

The third tab of the DCOMCNFG property sheet dialog is the Default Security property page, shown in Figure 13.3. There are three categories that this tab brings to view: Default Access Permissions, Default Launch Permissions, and Default Configuration Permissions. They all work together to form the default security for COM+ objects.

**FIGURE 13.3**  
*The DCOMCNFG*  
*Default Security*  
*page.*

![](bbox=[0.309, 0.399, 0.613, 0.654])

# Setting the Access Permissions

When you click Edit Default in the Default Access Permissions box, you can modify the `DefaultAccessPermission` value in the `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Ole` registry key. This setting determines who can call objects that do not specify custom access permissions.

Let’s go from the theoretical to the practical. Earlier in this chapter, in the section “Creating an Automation Server,” you created and installed a COM+ server that can be used as an example. Listing 13.6 shows you how changes in configuration using DCOM-CNFG reflect in successful and unsuccessful calls to the COM+ API.