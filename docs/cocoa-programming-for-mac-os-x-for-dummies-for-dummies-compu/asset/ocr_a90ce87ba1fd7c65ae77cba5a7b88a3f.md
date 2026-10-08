If the window title is the name of a document, use the `setTitleWith` `RepresentedFilename` method instead of `setTitle`. This method converts from a file path to a window title suitable for viewing:

```
`[theWindow setTitleWithRepresentedFilename:theFileName];`
```

# ## Windows that you can see through

Cocoa windows have an alpha setting that enables you to set the translu-
cency of a window. To see this magic in action, use the `setAlpha` method of
`NSWindow`, passing it a value between 0.0 and 1.0. A value of 1.0 means that
a window is fully visible; a value of 0.0 displays a window that’s completely
transparent. This line of code makes a window 50-percent transparent:

```
`[theWindow setAlphaValue:0.5];`
```

Figure 8-4 shows the difference between a window with `setAlpha` values
of 0.5 and 1.0.

![](bbox=[0.14, 0.48, 0.675, 0.875])