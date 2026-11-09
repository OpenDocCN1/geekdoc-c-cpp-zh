experimentation. To create an MTS component project simply choose File, New from the Visual C++ main menu and select the ATL COM App Wizard. Give your project a name and directory; then, at the first wizard dialog, choose the MTS support check box. MTS components are always DLLs, which enables MTS to supply a complete runtime environment. If you maintain the same project and class names used in the previous example, you won’t have to create a new COM+ application or modify the client application.

The DSP file is the only file that is modified from those generated for a normal ATL DLL project. MTS components are linked against the MTS support libraries, mtx.lib and mtxguid.lib. It is also worth noting that VC 6 introduces a new performance feature that enables your build to flag certain DLLs for delayed (just-in-time) loading. This keeps the size of the application image in memory to a minimum and speeds up initial program load times. ATL links to the mtxex.dll (the MTS Executive) in this way, using the /delayload linker switch. Use of the /delayload switch requires helper functions to load the DLL on-the-fly. You can roll your own or link in the presupplied routines found in delayimp.lib, as ATL does.

Next, add a new ATL object to the project by right-clicking the project icon in the Class View pane and selecting New ATL Object. Select the MS Transaction Server Component type and choose Next. Give your class a name (like Sum) and then click the MTS tab in the ATL Object Wizard Properties dialog to configure MTS-specific settings.

Checking support for IObjectControl causes the ATL Wizard to add interface support and starter code for all the IObjectControl methods. Checking Can Be Pooled causes ATL to generate a CanBePooled() method that returns true.

After creating the class, you’ll note that ATL adds a smart pointer attribute to reference the MTS IObjectContext interface. ATL adds code to initialize the pointer in the Activate() method and release it in the Deactivate() method. The generated code should look something like this:

```
HRESULT CSum::Activate()
{
    HRESULT hr = GetObjectContext(&m_spObjectContext);
    if (SUCCEEDED(hr))
        return S_OK;
    return hr;
}

BOOL CSum::CanBePooled()
{
    return TRUE;
}

void CSum::Deactivate()
```