```
-p t45 -c usbasp -P usb -U flash:w:"$(OutDir)Debug\$(TargetName).hex"
```

![](bbox=[0.23, 0.155, 0.81, 0.57])

Figure A.9: The External Tools Dialog Box in Microchip Studio

After filling in the fields of the External Tools dialog box, click the OK button to save the changes and close the dialog box. The tool, or programmer, that was set up using the External Tools dialog box can now be found on the top Tools menu in Microchip Studio, above the External Tools... item.

# A.3.5.3 Add a Toolbar Button for the External Tool

It is much easier to click a toolbar button to load a program to the target AVR than having to select the external programmer using the top Tools menu. We now set up a toolbar button for the external tool that we just added to Microchip Studio.

In Microchip Studio, select Tools ▶ Customize... from the top menu. In the Customize dialog box, click the Commands tab. Now click the Toolbar radio button. In the drop-down list next to the Toolbar radio button, select Device and Debugger – this selects a toolbar