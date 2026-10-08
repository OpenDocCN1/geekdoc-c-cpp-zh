The instance constructor simply sets the background color to blue violet, and adds underline the font. If you examine the ClassificationFormatDefinition class, you will find other interesting properties such BackgroundBrush, BackgroundOpacity, FontTypeValue, TextEffects, and many more.

In addition to the Export attribute, you can find other metadata that are important for defining the behavior of the classification format. Let's take a look at them.

The ClassificationType attribute binds the format definition and will be assigned only to the "ordinary" classification. The Name attribute assigns a name that can be used to refer to the format definition. The DisplayName attribute defines a name for the format that can be displayed at several places in the IDE. The UserVisible attribute allows displaying the format in the Options dialog in the Fonts and Colors tab, and lets the user change the format programmatically.

Nothing prevents a span of text from having more than one classification at the same time. This is normal because more classifiers use the corresponding classification formats in a certain order. The Order metadata attribute is used to define the place of format. In this example, it is set so that this format will override the editor's default format.

Because the UserVisible attribute of the format definition is set to true, you can find and override the definition in the Fonts and Colors dialog, as shown in Figure 6-36.

![](bbox=[0.095, 0.513, 0.748, 0.863])

FIGURE 6-36: Classifier Format definition can be overridden