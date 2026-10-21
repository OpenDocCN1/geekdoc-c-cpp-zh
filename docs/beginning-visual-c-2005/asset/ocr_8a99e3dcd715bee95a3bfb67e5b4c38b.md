for `ScaleDialog.h` from `SketcherView.cpp`. At this stage, all references to the original dialog class have been removed from the project. Are you all done yet? Almost. The IDs for the resources should have been deleted for you. To verify this, right-click `Sketcher.rc` in Resource View and select the `Resource Symbols` menu item from the pop-up; you can check that `IDC_SCALE` and `IDC_SPIN_SCALE` are no longer in the list. Of course, the `OnViewScale()` handler in the `SketcherView` class still refers to `ScaleDialog`, so the Sketcher project won’t compile yet. You’ll fix that when you have added the list box control.

Select the `Build > Clean Solution` menu item to remove any intermediate files from the project that may contain references to `CScaleDialog`. After that’s done, you can start by recreating the dialog resource for entering a scale value.

# Creating a List Box Control

Right-click Dialog in Resource View and add a new dialog with a suitable ID and caption. You could use the same ID as before, `IDD_SCALE_DLG`.

Select the list box button in the list of controls and click on where you want the list box positioned in the dialog box. You can enlarge the list box and adjust its position in the dialog by dragging it appropriately. Right-click the list box and select Properties from the pop-up. You can set the ID to something suitable, such as `IDC_SCALELIST` as shown in Figure 16-18.

![](bbox=[0.408, 0.464, 0.703, 0.928])

Figure 16-18