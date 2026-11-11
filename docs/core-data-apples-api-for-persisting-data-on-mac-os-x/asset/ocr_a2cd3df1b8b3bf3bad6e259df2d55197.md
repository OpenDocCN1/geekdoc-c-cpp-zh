```
<string>Grokking Recipe</string>
<key>UTITypeIdentifier</key>
<string>com.pragprog.grokkingrecipe</string>
<key>UTITypeTagSpecification</key>
<dict>
    <key>public.filename-extension</key>
    <string>grokkingrecipe</string>
</dict>
</dict>
</array>
```

This key describes exporting our UTI and tells Mac OS X how to link it to different file extensions. In addition, this section describes the data to Mac OS X, telling the OS a descriptive name for the data type and where in the UTI tree it fits.³

# Xcode Subproject

Our Spotlight importer is actually its own application. Xcode handles this by having a separate project for the importer.⁴ Since we want to include the importer as part of our primary application and we do not want to have to remember to rebuild the subproject every time we build our main project, we will set it up as a dependent or subproject within our primary project. To do this, we start with creating a new project in Xcode and selecting the Spotlight importer, as shown in Figure 7.2, on the next page. We want to save this project in a directory inside our primary recipe project. Don’t be too clever. Give the subproject an obvious name like SpotlightPlugin, and include it with the Spotlight example project. To make Xcode build this plug-in every time we build the main project, we need to link the two together. This is accomplished with the following steps:

+   1. Drag the subproject into the main project. See Figure 7.3, on the following page.
+   2. Open the target in the main project, and select the General tab.
+   3. Add the subproject as a dependency.
+   4. Add a new copy phase to the main project’s target, and set its destination to wrapper and path to Contents/Library/Spotlight.

3. For more information on UTIs, I suggest reviewing http://developer.apple.com/documentation/Carbon/Conceptual/understanding_uti/understand_uti_intro/chapter_1_section_1.html#//apple_ref/doc/uid/TP40001122

4. It is actually possible to include the plug-in as part of the main application project, but I have found that to be a complete mess and more hassle than it is worth.