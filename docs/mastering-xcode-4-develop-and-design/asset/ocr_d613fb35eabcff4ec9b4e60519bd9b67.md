Very few developers are likely to work for a company called "My Company Name," yet Xcode insists on inserting this in the copyright block at the top of any source files it creates. If you’re not currently employed by My Company Name, it’s wise to change the Organization field associated with the project so the copyright of newly created files reflects your actual organization (or even just your name).

To do this, select the project itself (the top-level object) in the Project navigator; then open the Utility area and select the File Inspector pane. Under the Project Document section, type the name of the desired copyright holder in the Organization field. Any source files Xcode creates from that point forward will insert that name instead of the standard __My Company Name__ placeholder.

# WRAPPING UP

This gentle introduction to the more advanced (or simply less common) aspects of Xcode 4 has given you a handful of powerful Source Editor features. These features offer elegant solutions to tedious and error-prone editing tasks developers encounter often when writing or maintaining code.

In the next chapter, you’ll learn about Xcode 4’s new Schemes system and how to customize the build and archive process, set up target dependencies, and more.