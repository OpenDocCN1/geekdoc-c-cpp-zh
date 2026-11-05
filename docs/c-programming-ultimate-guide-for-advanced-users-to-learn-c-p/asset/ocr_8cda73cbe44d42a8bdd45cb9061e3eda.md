```
richTextBox1.LoadFile("file.rtf", RichTextBoxStreamType.PlainText );
```

RichTextBoxStreamType is a specification characterized in the System.Windows.Forms namespace. You should utilize the completely qualified name or guarantee there is an utilizing articulation that alludes to the System.Windows.Forms namespace.

Sparing a Text File RichTextBox.SaveFile plays out the symmetric activity to LoadFile. SaveFile composes the substance of the RichTextBox control to a RTF or TXT record by calling SaveFile and passing a document name.

Utilizing the ZoomFactor RichTextBox.ZoomFactor is an intriguing property. With ZoomFactor you can express a rate increment in the size of the content. Setting ZoomFactor to 2 will twofold the size of the content, and .64 will diminish the size of the content by around half. Adequate esteems are from .64 to 64, the last being multiple times the typical size. This property is an amazing element for applications supporting individuals with incapacities and for introductions. Assume, for instance, that you are showing the substance of the RichTextBox on an overhead projector. Setting the ZoomFactor to expand content size will make it simpler for your crowd to see the substance in the RichTextBox control.

Utilizing the LinkLabel the LinkLabel control speaks to a Windows Forms hyperlink, further obscuring the lines among Windows and Web applications. Enter a URL in the LinkLabel.Text property and, when a client taps on the LinkLabel control, the estimation of the Text property can be utilized to open IE, for instance.

The Process class is characterized in the System.Diagnostics namespace, and Start is a static technique. The Process class is valuable for beginning, halting, controlling, and observing applications. In this model, the http//moniker verifiably teaches Process.Start to begin another case of IE, given the relationship among URLs and Internet Explorer.

Precious stone Reports, which is a famous device from Seagate Software, is currently Crystal Decisions. For cutting edge printing and detailing, you can incorporate Crystal Decisions–based controls into your application, however fundamental printing is upheld by the PrintDocument control.