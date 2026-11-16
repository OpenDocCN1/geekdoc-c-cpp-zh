# # WPF TREES

We've talked about how XAML elements are hierarchical. Programmers find it useful to think of hierarchies as trees, and in WPF there are three. The object tree is probably the simplest to understand: It represents the way elements are nested in the XAML markup (or in code).

The LOGICAL TREE is similar to the object tree, and probably best understood by example. Logically, the parent of the items in a ListBox is the <ListBox> itself, and that's what the logical tree reflects. But in the object tree, the items are contained in the ListBox.Items collection. In other words, the logical tree omits most of the interim objects.

Finally, the VISUAL TREE contains all the elements that are displayed on the screen. Almost all of the WPF controls you'll work with are actually composed of multiple visual elements—the default Button, for example, includes a Border, a ContentPresenter, and a TextBlock. (As we'll see in Chapter 21 when we examine control templates, you have a lot of control over the elements that compose a WPF control, so this isn't an absolute.)

![](bbox=[0.085, 0.525, 0.915, 0.915])