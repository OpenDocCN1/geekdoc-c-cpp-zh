# AppContainer capabilities

As you just saw, UWP applications have restricted access rights. So how, for example, is the Microsoft Edge application able to parse the local file system and open PDF files in the user's Documents folder? Similarly, how can the Music application play MP3 files from the Music directory? Whether directly through kernel access or by brokers (which you'll see in the next section), the key lies in capability SIDs. Let's see where these come from, how they are created, and what they are used for.

First, UWP developers begin by creating an application manifest that specifies many details of their application, such as the package name, resources, supported devices, and more. One of the keys for capability management is the list of capabilities in the manifest. For example, let's look at Cortana's application manifest, located in %SystemRoot%\SystemApps\Windows.Cortana_cw5n1htxy2AppManifest.xml.

```
<Capabilities>
<!-- for resolving MRT ranges -->
<Capability Name="cortanaSettings />
<Capability Name="cloudStore />
<Capability Name="visualElementsSystem />
<Capability Name="perceptionSystem />
<Capability Name="internetClient />
<Capability Name="internetNetworkServer />
<Capability Name="privateNetworkClientServer />
<Capability Name="enterpriseAuthentication />\n<Capability Name="musicLibrary />
<Capability Name="phoneCall />
<Capability Name="picturesLibrary />
<Capability Name="sharedUserCertificates />
<rescap Name="locationHistory />
<rescap Name="userDataSystem />
<rescap Name="contactsSystem />
<rescap Name="phoneCallHistorySystem />
<rescap Name="appointmentSystem />
<rescap Name="chatSystem />
<rescap Name="smsSend />
<rescap Name="emailSystem />
<rescap Name="packageQuery />
<rescap Name="s1QueryLicenseValue />
<rescap Name="secondaryAuthenticationFactor />
<DeviceCapability Name="microphone />
<DeviceCapability Name="location />
<DeviceCapability Name="wifiControl />
</Capabilities>
```

You'll see many types of entries in this list. For example, the Capability entries contain well-known SIDs associated with the original capability set that was implemented in Windows 8. These begin with SECURITY_CAPABILITY—for example, SECURITY_CAPABILITY_INTERNET_CLIENT, which is part of the capability RID under the APPLICATION PACKAGE AUTHORITY. This gives us a SID of S-1-15-3 in string format.