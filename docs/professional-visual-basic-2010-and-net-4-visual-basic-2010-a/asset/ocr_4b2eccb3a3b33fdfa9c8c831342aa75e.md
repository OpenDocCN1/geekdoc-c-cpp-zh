Namespaces provide identification beyond the component name. With a namespace, it is possible to use a more meaningful title (for example, `System`) followed by a grouping (for example, `Text`) to group together a collection of classes that contain similar functions. For example, the `System.Text` namespace contains a powerful class called `StringBuilder`. To reference this class, you can use the fully qualified namespace reference of `System.Text.StringBuilder`, as shown here:

```
Dim sb As New System.Text.StringBuilder()
```

The structure of a namespace is not a reflection of the physical inheritance of classes that make up the namespace. For example, the `System.Text` namespace contains another child namespace called `RegularExpressions`. This namespace contains several classes, but they do not inherit or otherwise reference the classes that make up the `System.Text` namespace.

Figure 4-6 shows how the `System` namespace contains the `Text` child namespace, which also has a child namespace, called `RegularExpressions`. Both of these child namespaces, `Text` and `RegularExpressions`, contain a number of objects in the inheritance model for these classes, as shown in the figure.

![](bbox=[0.08, 0.44, 0.64, 0.66])

# FIGURE 4-6

As shown in Figure 4-6, while some of the classes in each namespace do inherit from each other, and while all of the classes eventually inherit from the generic `Object`, the classes in `System.Text.RegularExpressions` do not inherit from the classes in `System.Text`.

To emphasize the usefulness of namespaces, we can draw another good example from Figure 4-6. If you make a reference to `System.Drawing.Imaging.Encoder` in your application, then you are making a reference to a completely different `Encoder` class than the namespace shown in Figure 4-6 — `System.Text.Encoder`. Being able to clearly identify classes that have the same name but very different functions, and disambiguate them, is yet another advantage of namespaces.

If you are an experienced COM developer, you may note that unlike a ProgID, which reflects a one-level relationship between the project assembly and the class, a single namespace can use child namespaces to extend the meaningful description of a class. The `System` namespace, imported by default as part of every project created with Visual Studio, contains not only the default `Object` class, but also many other classes that are used as the basis for every .NET language.

What if a class you need isn’t available in your project? The problem may be with the references in your project. For example, by default, the `System.DirectoryServices` namespace, used to get programmatic access to the Active Directory objects, is not part of your project’s assembly. Using it requires adding a