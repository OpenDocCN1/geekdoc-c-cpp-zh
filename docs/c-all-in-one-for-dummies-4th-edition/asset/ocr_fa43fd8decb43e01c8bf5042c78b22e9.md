+   8. **Click Add in the Linker subtab.**
+   
+      You see the Add Directory dialog box (refer to Figure 4-2).

+   9. **Type the location of the Boost library files in the Directory field and then click OK.**
+   
+      The Boost library files are typically located in the `C:\CodeBlocks\boost_1_73_0\libs` directory. After you click OK, you see the directory added to the Linker tab.

+   10. **Select the Linker Settings tab.**
+   
+       This tab contains two lists — one for link libraries and another for linker options.

+   11. **Click Add.**
+   
+       Code::Blocks displays the Add Library dialog box, shown in Figure 4-4. This example requires use of the `libboost_regex-mgw6-mt-d-x32-1_73.a` library file.

![](bbox=[0.259, 0.438, 0.508, 0.525])

+   12. **Click the Browse button, locate the library you need to use, and click Open.**
+   
+       The `libboost_regex-mgw6-mt-d-x32-1_73.a` library is normally found in the `C:\CodeBlocks\boost_1_73_0\bin.v2\libs\regex\build\gcc-6.2.0\debug\address-model-32\link-static\threading-multi\visibility-hidden` directory.

+   13. **Click OK.**
+   
+       You see the library file added to the Link Libraries list, as shown in Figure 4-5.

+   14. **Click OK.**
+   
+       The Compiler Settings dialog box closes.

+   15. **Build the application by choosing Build > Build.**
+   
+       The application should build without warnings or errors. If you see warnings or errors, ensure that you've added both header and library search paths, and the required library file.