This area is where you set the attributes of the controls that are embedded in the templates. The controls include knobs, option menus and edit boxes. The attributes you set are:

+   - origin: the (x,y) coordinates of the upper left corner of a control
- size: the width and height of the control
- bitmap: for the knob controls, you select the "knob" bitmap map
- control-tag: the control tag is a zero-based index that links the control to an underlying variable; although they can be any string, makes sense to match them with the enumerations you made in the SynthParamLimits.h file
- transparent: all template features with transparent backgrounds; you may change this by un-checking the "transparent" check-box
- title: for text-based controls, this is where you set the default text
- font: for text-based controls, this is where you set the font (and size)
- font color: color for the text fields, you may want to modify the font color

# D: Views/Tags/Bitmaps

This is an important area in the editor because it shows you the C++ objects (Views), the control ID values (Tags) and graphical elements (Bitmaps).

# Views

The Tabs reveal a list of the C++ objects you can drag and drop into the GUI. You click on a view as CViewContainer hold, drag and drop into the GUI. Once it is added to the interface, the control attributes will change to reflect this new GUI. At that point, you usually adjust the origin and size to move the control to an exact position in the GUI with an exact size. The columns you see in the MiniSynth GUI are CViewContainers with the bitmap set to "groupframe"—VSTUI automatically stretches the image to fit the container for some control types.

# Tags

Tags are a list of the indexed control values you set in the enumeration step in the GUI design. You use the + and buttons at the bottom to add or remove Tags. Double click on the Tag value in the second column to change it. The Tags are alphabetized, so they probably be in numerical order. The Tags can be any text string, but it makes sense to use the same strings for the enumeration (e.g. OCTAVE) so everything matches up. If you make mistakes with the Tags, your controls won't work properly. If you duplicate the Tag values, then any controls with the same index will move each other and move together if automated.

# Bitmaps

Bitmaps are the graphical elements in your GUI. They do not have to be strictly in the .BMP format; you can use JPEG, PNG or other type that Visual Studio supports. The bitmaps are resources you add to Visual Studio. You will see them in the Resources folder in the Visual Studio projects. The files we use for all of the projects:

+   - background.png: the grey image for the main CContainer
- groupframe.png: the transparent grey frames that are the background image for the columnar and row-shaped controls
- knob.png: the medium sized blue rotary used for most of the knob controls