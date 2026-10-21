# Chapter 18

Now that the MFC DLL wizard has done its stuff, you can look into the code that has been generated on your behalf. If you look at the contents of the project in the Solution Explorer pane, you’ll see that the MFC DLL wizard has generated several files, including a .txt file that contains a description of the other files. You can read what they’re all for in the .txt file, but the following two are the ones of immediate interest in implementing our DLL:

| Filename | Contents |
|---|---|
| ExtDLLExample.cpp | This contains the function DllMain() and is the primary source file for the DLL. |
| ExtDLLExample.def | The information in this file is used during compilation. It contains the name of the DLL, and you can also add to it the definitions of those items in the DLL that are to be accessible to a program using the DLL. You’ll use an alternative and somewhat easier way of identifying such items in the example. |

When your DLL is loaded, the first thing that happens is that DllMain() is executed, so perhaps you should take a look at that first.

# Understanding DllMain()

If you look at the contents of ExtDLLExample.cpp, you will see that the MFC DLL wizard has generated a version of DllMain() for you, as shown here:

```
extern "C" int APIENTRY
DllMain(HINSTANCE hInstance, DWORD dwReason, LPVOID lpReserved)
{
    // Remove this if you use lpReserved
    UNREFERENCED_PARAMETER(lpReserved);

    if (dwReason == DLL_PROCESS_ATTACH)
    {
        TRACE0("EXTDLLEXAMPLE.DLL Initializing!\n");

        // Extension DLL one-time initialization
        if (!AfxInitExtensionModule(ExtDLLExampleDLL, hInstance))
            return 0;

        // Insert this DLL into the resource chain
        // NOTE: If this Extension DLL is being implicitly linked to by
        // an MFC Regular DLL (such as an ActiveX Control)
        // instead of an MFC application, then you will want to
        // remove this line from DllMain and put it in a separate
        // function exported from this Extension DLL. The Regular DLL
        // that uses this Extension DLL should then explicitly call that
        // function to initialize this Extension DLL. Otherwise,
        // the CDynLinkLibrary object will not be attached to the
        // Regular DLL's resource chain, and serious problems will
        // result.

        new CDynLinkLibrary(ExtDLLExampleDLL);
    }
```