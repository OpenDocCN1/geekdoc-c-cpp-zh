```
bool __stdcall CSimpleHPF::userInterfaceChange(int nControlIndex)
{
    // decode the control index
    switch(nControlIndex)
    {
        case 0:
        {
            m_f_al_left = m_fS1lder_al;
            m_f_al_right = m_fS1lder_al;

            m_f_a0_left = m_f_al_left - 1.0;
            m_f_a0_right = m_f_al_right - 1.0;

            break;
        }
        case 1:
        {
            m_fVolume = pow(10.0, m_fVolume_dB/20.0);
            break;
        }
        default:
        break;
    }
    return true;
}
```

Build and test your code to make sure the plug-in works as expected. You now understand the basics of writing a plug-in from a block diagram and design equations.

# Add some presets

Now that you have a GUI with more than one control, try adding some presets. If you look at the preset list in the toolbar, you will see the first one is named Factory Preset. This preset contains your initial settings for the GUI controls. You cannot delete this preset and it is automatically updated whenever you add, edit, or delete controls. This preset takes you back to your initial state. With your plug-in loaded and (optionally) audio streaming through it, adjust the controls to affect the signal. Hit the Save Preset button on the toolbar or choose it from the plug-in menu. A box will pop up allowing you to name the preset. You can also overwrite an existing preset. You can store up to 32 presets in your plug-in.

# 3.13 The User Plug-In Menu in RackAFX

As you use more plug-ins, you will notice that they begin to automatically populate the user plug-in menu item in RackAFX. By now, you should have three plug-ins in this menu. There are a few things you need to understand about this menu.

+   - It allows you to play with the plug-ins without having to open your compiler and manually load and unload the DLLs.
+   - You can select different plug-ins from this menu while audio is streaming and they will automatically slot in and out, so you can audition or show off your plug-ins quickly.
+   - It allows RackAFX to behave just like other plug-in clients by loading all the DLLs it finds in its PlugIns folder at once when you start the software. This can be dangerous!

That last item poses a problem during the course of development—if you write a DLL that does bad