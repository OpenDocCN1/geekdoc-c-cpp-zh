We don't suggest that you use the registry to store configuration parameters for your Java programs. The java preferences API is a better solution (see Volume I, Chapter 13 for more information). We'll simply use the registry to demonstrate how to wrap a nontrivial native API into a Java class.

The principal tool for inspecting the registry is the *registry editor*. Because of the potential for error by naive but enthusiastic users, there is no icon for launching the registry editor. Instead, start a DOS shell (or open the Start → Run dialog box) and type `regedit`. Figure 12.4 shows the registry editor in action.

![](bbox=[0.19, 0.36, 0.91, 0.65])

**Figure 12.4** The registry editor

The left side shows the keys, which are arranged in a tree structure. Note that each key starts with one of the `HKEY` nodes like

+   - HKEY_CLASSES_ROOT
+   - HKEY_CURRENT_USER
+   - HKEY_LOCAL_MACHINE
+   - . . .