
- 1. Locate the `C:\CodeBlocks\boost_1_73_0\libs\regex\example\timer` folder on your system.
- 2. Double-click the `regex_timer.cpp` file.

Code::Blocks automatically opens the file for you. If you attempt to compile the file at this point, Code::Blocks displays a considerable number of errors. The errors aren't due to problems with the code, but with issues in the configuration. You need to configure Code::Blocks to work with this example.

- 3. Choose **Settings → Compiler**.

You see the Compiler Settings dialog box, shown in Figure 4-1. You need to perform three configuration tasks to make the example usable:

- Tell Code::Blocks where to find the Boost include (header) files.
- Tell Code::Blocks where to find the Boost library files.
- Configure Code::Blocks to add the required libraries to the application.

![](img/128ab511de4e7360e167e3b15cdd5dd0_848_0.png)

**FIGURE 4-1:** Use the Compiler Settings dialog box to configure Code::Blocks to use Boost.

- 4. Select the Search Directories tab.

You see three subtabs: Compiler, Linker, and Resource Compiler.

- 5. **Click Add in the Compiler subtab.**

You see an Add Directory dialog box like the one shown in Figure 4-2.

**FIGURE 4-2:** Add appropriate search directories for Boost header and library files.

![](img/128ab511de4e7360e167e3b15cdd5dd0_849_0.png)

- 6. **Type the location of the Boost header files in the Directory field.**

As an alternative, you can click the Browse button to use a Browse for Folder dialog box to find them. The files are normally located in the `C:\CodeBlocks\boost_1_73_0\boost` folder.

- 7. **Click OK.**

You see the search folder added to the Compiler tab, as shown in Figure 4-3.

**FIGURE 4-3:** The Search Directories tab will display any compiler, linker, or resource compiler search locations.

![](img/128ab511de4e7360e167e3b15cdd5dd0_849_1.png)

- 8. **Click Add in the Linker subtab.**

You see the Add Directory dialog box (refer to Figure 4-2).

- 9. **Type the location of the Boost library files in the Directory field and then click OK.**

The Boost library files are typically located in the `C:\CodeBlocks\boost_1_73_0\libs` directory. After you click OK, you see the directory added to the Linker tab.

- 10. **Select the Linker Settings tab.**

This tab contains two lists — one for link libraries and another for linker options.

- 11. **Click Add.**

Code::Blocks displays the Add Library dialog box, shown in Figure 4-4. This example requires use of the `libboost_regex-mgw6-mt-d-x32-1_73.a` library file.

![](img/128ab511de4e7360e167e3b15cdd5dd0_850_0.png)

- 12. **Click the Browse button, locate the library you need to use, and click Open.**

The `libboost_regex-mgw6-mt-d-x32-1_73.a` library is normally found in the `C:\CodeBlocks\boost_1_73_0\bin.v2\libs\regex\build\gcc-6.2.0\debug\address-model-32\link-static\threading-multi\visibility-hidden` directory.

- 13. **Click OK.**

You see the library file added to the Link Libraries list, as shown in Figure 4-5.

- 14. **Click OK.**

The Compiler Settings dialog box closes.

- 15. **Build the application by choosing Build > Build.**

The application should build without warnings or errors. If you see warnings or errors, ensure that you've added both header and library search paths, and the required library file.

![](img/128ab511de4e7360e167e3b15cdd5dd0_852_0.png)

**FIGURE 4-6:** The example displays the result of the search.

## Creating the Boost Tools

It’s always nice when a vendor provides tools for making it easier to work with a product, and Boost is no exception. You find these tools in the `\boost_1_73_0\` tools directory. The sections that follow this one describe a number of these tools in detail, but here is a quick list of the tools you get:

- **Boost.Build:** Helps you build applications that use Boost by automating some of the process from the command line. This product is actually an add-on for an updated version of Boost.Jam, which used to appear as a separate product.
- **Inspect:** Determines whether there are any errors in the Boost directory hierarchy. Errors in the directory hierarchy can cause the automatic Boost features to work incorrectly.
- **BoostBook:** Provides the developer with a fast and easy method for accessing the Boost documentation. It relies partially on DocBook (`https://docbook.org/`), the eXtensible StyleSheet Language (XSL), and some Boost functionality. This tool is used by some Boost libraries.
- **bcp:** Extracts subsets of Boost for use with your application. To perform this task, bcp also provides a method for determining which parts of Boost your code relies upon and it also makes it possible to print reports of Boost usage (including any required licensing information).
- **QuickBook:** Generates BoostBook XML files. This tool provides a WikiWiki (wiki) style documentation geared toward C++ documentation requirements. A wiki is a collection of hypertext documents. Wiki pages are collaborative and allow all users or registered users to change the content in these collections, which makes them different from a collection of static hypertext documents. It relies on simple rules and markup for providing output formatting.
- **Wave:** Preprocesses your C/C++ application code. You can use it with any compiler. The main purpose of the Wave preprocessor is to check the expansion of macros in your code as part of the debugging process. You can also use it as a preprocessor replacement if you don't like how the preprocessor supplied with your compiler works.
- **AutoIndex:** Creates indexes for BoostBook and DocBook documents.

All these tools come in source code format as part of your Boost installation. They’re not ready for use when you unpack Boost. Of course, the lack of executable code makes sense considering the number of platforms that Boost supports. In order to use the tools, you must first build them.

The first task is to create a version of Boost.Build for your system. You use Boost.Build to build all the other tools. The following steps describe how to build Boost.Build:

- 1. **Open a command prompt or terminal window using the technique appropriate for your platform.**

For example, when working with Windows, you choose Start➜Programs➜Accessories➜Command Prompt. When working with a Mac, you navigate to the /Applications/Utilities window and double-click Terminal. The method of opening a terminal window in Linux varies with the distribution you use.

- 2. **Type** `CD \CodeBlocks\boost_1_73_0\tools\build` **and press Enter.**

This is the Windows version of the command. For other platforms, you need to change directories to the directory that contains the Boost 1.73 tools. The command processor takes you to the Boost.Build directory.

- 3. **(Optional) If you haven’t already created a path to the CodeBlocks compiler at the command line or terminal, create one.**

For example, when working with Windows, type `path = C:\CodeBlocks\MinGW\bin;%path%` and press Enter.

- 4. **Type** `bootstrap gcc` **and press Enter.**

You see a message, `Building the B2 engine` (along with a lot of other text), at the command prompt or terminal window for a few seconds. When the Boost.Build compilation is complete, you see additional text telling you how to use the resulting B2 command.

- 5. **Type** `b2 --prefix=DIR install` **and press Enter.**

You must replace the placeholder text DIR shown previously with the location you want to use to install Boost.Build. For example, if you have a Windows system and want to install Boost.Build in C:\Boost.Build, you type **b2 --prefix=C:\Boost.Build install** and press Enter.

![](img/128ab511de4e7360e167e3b15cdd5dd0_853_0.png)
