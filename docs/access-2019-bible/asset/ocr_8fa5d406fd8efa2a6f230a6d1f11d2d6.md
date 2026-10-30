The <tabs> (line 5) and </tabs> (line 18) tags indicate the beginning and end of the tabs on the Ribbon. Ribbons are hierarchical, with tabs containing groups, which contain controls. The tabs, therefore, are the highest-level objects within a Ribbon and enclose all other Ribbon objects.

Line 6 defines the leftmost tab on the Ribbon. In this example, the tab's name is tab1. The other attributes for this tab are not shown but are implied by the ellipsis (...). The ending tag for tab1 is located on line 10.

Line 7 begins the definition of the first group on tab1 and line 9 ends this group. Within the group are the controls displayed by the group.

The rest of this prototype Ribbon is simple repetition of the first few items.

> NOTE
> XML is case sensitive. Be careful to use exactly the same case and spelling for all references in your XML as well as in the callback code driving the Ribbon.

# Adding Ribbon Controls

The previous section presented a simple prototype Ribbon. In this example, the controls were indicated by ... Controls go here ... on lines 8 and 13. In this section, you'll see the XML and the callback procedures for several controls. Many XML attributes are common to more than one control. We won't discuss every attribute for every control; rather, we'll look at the most-used attributes.

# Specifying imageMso

Most, but not all, Ribbon controls include an imageMso attribute that specifies the picture attached to the control. You can't provide simple references to image files; instead, you must use an imageMso identifier for this purpose. Every Ribbon control in the Office 2019 applications has an associated imageMso value. You use these values on your custom Access Ribbon controls and provide a label that tells your users the exact purpose of the control.

To find the imageMso for a particular Ribbon control, use the Customize the Ribbon window to open a particular Ribbon. Then use the drop-down in the upper left of the designer to select the Ribbon category containing the Ribbon command and hover the mouse over the command's entry in the list (see Figure 30.19).

The imageMso for the Layout View command (ViewsLayoutView) is shown in parentheses in the ScreenTip that appears near the selected command.