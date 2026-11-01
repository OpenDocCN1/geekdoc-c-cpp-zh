a blinking icon next to the control that caused the validation error, and the error message is displayed as a tooltip. You can call SetError again with an empty error string to remove the error condition.

# ImageList

An ImageList component is exactly what the name implies — a list of images. Typically, this component is used for holding a collection of images that are used as toolbar icons or icons in a TreeView control. Many controls have an ImageList property. The ImageList property typically comes with an ImageIndex property. The ImageList property is set to an instance of the ImageList component, and the ImageIndex property is set to the index in the ImageList that represents the image that should be displayed on the control. You add images to the ImageList component by using the Add method of the ImageList.Images property. The Images property returns an ImageCollection.

The two most commonly used properties are ImageSize and ColorDepth. ImageSize uses a Size structure as its value. The default value is 16 3 16, but it can be any value from 1 to 256. The ColorDepth uses a ColorDepth enumeration as its value. The color depth values go from 4-bit to 32-bit, with a default of ColorDepth.Depth8Bit.

# Label

Labels are generally used to provide descriptive text to the user. The text might be related to other controls or the current system state. You usually see a label together with a text box. The label provides the user with a description of the type of data to be entered in the text box. The Label control is always read-only — the user cannot change the string value of the Text property. However, you can change the Text property in your code. The UseMnemonic property allows you to enable the access key functionality. When you precede a character in the Text property with the ampersand (&), that letter will appear underlined in the label control. Pressing the Alt key in combination with the underlined letter puts the focus on the next control in the tab order. If you wish to display an ampersand in the text, you need to escape it with another ampersand. For example, if the label text should be “Nuts & Bolts,” set the property to “Nuts & & Bolts.” Because the Label control is read-only, it cannot gain focus; that’s why focus is sent to the next control. Because of this, it is important to remember that if you enable mnemonics, you must be certain to set the tab order properly on your form.

The AutoSize property is a Boolean value that specifies whether the Label will resize itself based on the contents of the Label. This can be useful for multi-language applications where the length of the Text property can change based on the current language.

# ListView

The ListView control enables you to display items in one of four different ways. You can display text with an optional large icon, text with an optional small icon, or text and small icons in a vertical list or in detail view, which allows you to display the item text plus any subitems in columns. If this sounds familiar, it should, because this is similar to the right-hand side of Windows Explorer. A ListView contains a collection of ListViewItems. ListViewItems allow you to set a Text property used for the display. ListViewItem has a property called SubItems that contains the text that appears in detail view.

# PictureBox

The PictureBox control is used to display an image. The image can be a BMP, JPEG, GIF, PNG, metafile, or icon. The SizeMode property uses the PictureBoxSizeMode enumeration to determine how