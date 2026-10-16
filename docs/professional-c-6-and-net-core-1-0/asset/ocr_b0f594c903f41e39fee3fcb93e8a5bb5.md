values that are different by setting the properties afterward.

Calling the method Register registers the new culture with the operating system. Indeed, you can find the file that describes the culture in the directory <windows>\Globalization. Look for files with the extension .nlp (code file CustomCultures\Program.cs):

```
using System;
using System.Globalization;
using static System.Console;

namespace CustomCultures
{
    class Program
    {
        static void Main()
        {
            try
            {
                // Create a Styria culture
                var styria = new CultureAndRegionInfoBuilder("de-AT-ST",
                    CultureAndRegionModifiers.None);
                var cultureParent = new CultureInfo("de-AT");
                styria.LoadDataFromCultureInfo(cultureParent);
                styria.LoadDataFromRegionInfo(new RegionInfo("AT"));
                styria.Parent = cultureParent;
                styria.RegionNativeName = "Steiermark";
                styria.RegionEnglishName = "Styria";
                styria.CultureEnglishName = "Styria (Austria)";
                styria.CultureNativeName = "Steirisch";
                styria.Register();
            }
            catch (UnauthorizedAccessException ex)
            {
                WriteLine(ex.Message);
            }
        }
    }
}
```

Because registering custom languages on the system requires administrative privileges, the sample application is built using the Console Application project template, and an application manifest file is added. This manifest file specifies the requested execution rights. In the project properties, the manifest file needs to be set in the Application settings:

```
<?xml version="1.0" encoding="utf-8"?>
<asmv1:assembly manifestVersion="1.0" xmlns="urn:schemas-microsoft-com:asm.v1"
xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"
xmlns:asmv2="urn:schemas-microsoft-com:asm.v2" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <assemblyIdentity version="1.0.0.0" name="MyApplication.app"/>
    <trustInfo xmlns="urn:schemas-microsoft-com:asm.v2">
        <security>
            <requestedPrivileges xmlns="urn:schemas-microsoft-com:asm.v3">
                <requestedExecutionLevel level="requireAdministrator" uiAccess="false" />
            </requestedPrivileges>
        </security>
    </trustInfo>
</asmv1:assembly>
```