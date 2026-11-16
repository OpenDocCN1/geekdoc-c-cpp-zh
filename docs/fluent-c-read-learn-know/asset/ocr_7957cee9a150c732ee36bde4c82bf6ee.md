# PUT ON YOUR THINKING HAT

Have you noticed how close to the end of the book we are? Of course you have. In fact, you're almost finished, and I have a real challenge for you. Here's just a little bit of information about how to group items in a collection. Can you group your collection by the Available property?

+   - Both the CollectionView and CollectionViewSource objects expose a GroupDescriptions property, so you can implement grouping in XAML or code.
+   - The GroupDescriptions collection property accepts instances of the abstract GroupDescription class, which has a single descendant, PropertyGroupDescription. The key property of a PropertyGroupDescription is PropertyName, which accepts a String.
+   - In order to display the items in groups, you have to add a GroupStyle to the items control. The GroupStyle accepts (among other things) a HeaderTemplate, which accepts a single DataTemplate.
+   - The data template inside a HeaderTemplate works just like any other DataTemplate, but it doesn't bind to the collection; it binds to a CollectionViewGroup. The CollectionViewGroup.Name property contains the value of the current property group (the number available, in our example).

So, can you duplicate this window?

![](bbox=[0.45, 0.54, 0.85, 0.85])