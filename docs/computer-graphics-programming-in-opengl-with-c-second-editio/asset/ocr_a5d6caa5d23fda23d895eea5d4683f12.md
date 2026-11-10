# A.5.4 Preparing GLEW

An overview of the GLEW “extension wrangler” library was given in Chapter 1. Download the 64-bit binaries from glew.sourceforge.net [GE17]. The items in particular we will need to obtain are:

+   - **glew32.lib** (found in the “lib” folder) - yes the name includes “32”, but currently these are still the correct files for 64-bit installation
+   - **glew32.dll** (found in the “release” folder)
+   - the **GL** folder, which includes several header files (found in the “include” folder)

# A.5.5 Preparing GLM

An overview of the math library GLM was given in Chapter 1. Visit glm.g-truc.net/0.9.9/index.html [GM20] and download the latest version that includes release notes. The download folder, after being unzipped, contains a folder named “glm”. That folder (and its contents) is the item that we will need to use.

# A.5.6 Preparing SOIL2

An overview of the image loading library SOIL2 was given in Chapter 1. Installing SOIL2 [SO20] requires utilizing a tool called “premake” [PM20]. Although the process involves several steps, they are relatively straightforward:

+   1. Download and uncompress “premake.” The only file in it is “premake4.exe.”
+   2. Download SOIL2 (use the “downloads” link at the bottom of the left panel), and uncompress it.
+   3. Copy the “premake4.exe” file into the soil2 folder.
+   4. Open a command window, navigate to the soil2 folder, and enter:

```
```
premake --platform=x64 vs2012
```
```

It should display a number of files that are then created.

+   5. In the soil2 folder, open the “make” folder, then the “windows” folder. Double-click SOIL2.sln.
+   6. If prompted by VisualStudio to upgrade libraries, do it by clicking “ok.”
+   7. Switch from x86 to x64 using the dropdown box near the top, then in the panel on the right, right-click on “soil2-static-lib” and select “build.”