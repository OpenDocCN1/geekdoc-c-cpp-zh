# XRef scene options

In the XRef Scenes dialog box are several options for controlling the appearance of the scene objects, how often the scene is updated, and to which object the scene is bound. This dialog box is modeless, and you can open and change the options in this dialog box at any time.

The pane on the left lists all XRef scenes in the current scene. These scenes are displayed using their full path unless the Convert Local File Paths to Relative option in the Files panel of the Preference Settings dialog box is enabled. To the right are the settings, which can be different for each XRef scene in the list. To view or apply a setting, you first need to select the scene from the list. You can remove any scene by selecting it from the list and clicking the Remove button.

# Caution

If an XRef scene in the list is displayed in red, then the scene could not be loaded. If the path or name is incorrect, you can change it in the Path field at the bottom of the list.

The Convert Selected button converts any selected objects in the current scene to XRef objects by saving them as a separate file. This button opens a dialog box to let you name and save the new file. If no objects are selected in the current scene, then this option is disabled.

Use the Enabled option to enable or disable all XRef scenes. Disabled scenes are displayed in gray. The Merge button lets you insert the current XRef scene into the current scene. This button removes the scene from the list and acts the same way as the Application Button Import Merge command.

# Updating an external scene

Automatic is a key option that can set any XRef scene to be automatically updated. Enable this option by selecting a scene from the list and checking the Automatic option box; thereafter, the scene is updated anytime the source file is updated. This option can slow the system if the external scene is updated frequently, but the benefit is that you can work with the latest update.

The Update Now button is for manually updating the XRef scene. Click this button to update the external scene to the latest saved version.

# External scene appearance

Other options let you decide how the scene is displayed in the viewports. You can choose to make the external scene invisible or to display it as a box. Making an external scene invisible removes it from the viewports, but the scene is still included in the rendered output. To remove a scene from the rendered output, deselect the Enabled option.

The Ignore section lists objects such as lights, cameras, shapes, helpers, and animation; selecting them causes them to be ignored and to have no effect in the scene. If an external scene's animation is ignored, then the scene appears as it does in frame 0.

# Positioning an external scene

Positioning an external scene is accomplished by binding the scene to an object in the current scene (a dummy object, for example). The XRef Scenes dialog box is modeless, so you can select the object to bind to without closing the dialog box. After a binding object is selected, the external scene transforms to the binding object's pivot point. The name of the parent object is also displayed in the XRef Scenes dialog box.

Transforming the object to which the scene is bound can control how the external scene is repositioned. To unbind an object, click the Unbind button in the XRef Scenes dialog box. Unbound scenes are positioned at the World origin for the current scene.