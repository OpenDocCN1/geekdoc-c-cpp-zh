
- **6. Add Boost.Build to the path using the command for your particular platform.**
  
  For example, when working with Windows, type `path=C:\Boost.Build\bin;%path%` and press Enter.

Now that you have an application to build the Boost tools, you can build the tools themselves. A number of the tools come with build directories or build files in their main directory. In those directories are the instructions required to create the tools. For example, look in the `\CodeBlocks\boost_1_73_0\tools\auto_index\build` directory and you see a `Jamfile.v2` file. This is the file that contains the instructions for building the AutoIndex tool. Likewise, you find a `Jamfile.v2` file in the `\CodeBlocks\boost_1_73_0\tools\bcp` folder. (The file is in the main directory, rather than a build directory in this case.) No matter where the `Jamfile.v2` file is located, you use it to build the associated tool.

However, the easiest method to build the tools is to build them all at one time. A special `Jamfile.v2` file is located in the `\CodeBlocks\boost_1_73_0` directory. You use it to create all the tools simultaneously, using the following steps.

![](img/128ab511de4e7360e167e3b15cdd5dd0_854_0.png)

- **1. Open a command prompt or terminal window using the technique appropriate for your platform.**

- **2. Type** `CD \CodeBlocks\boost_1_73_0\tools` **and press Enter.**
  
  The command processor takes you to the main tools directory.

- **3. (Optional) If you haven't already created a path to the CodeBlocks compiler at the command line or terminal, create one.**
  
  For example, when working with Windows, type `path=C:\CodeBlocks\MinGW\bin;%path%` and press Enter.

- **4. (Optional) If you haven't already created a path to Boost.Build at the command line or terminal, create one.**
  
  For example, when working with Windows, type `path=C:\Boost.Build\bin;%path%` and press Enter.

- **5. Type** `b2` **and press Enter.**
  
  Be patient; the build process will take several minutes. The executable files for Inspect (`inspect.exe`), bcp (`bcp.exe`), and QuickBook (`quickbook.exe`) will automatically appear in the `\CodeBlocks\boost_1_73_0\dist\bin` directory on your system after the build process is complete. BoostBook content appears in the `\CodeBlocks\boost_1_73_0\dist\share\boostbook` directory.

```cpp
{
    cout << "Hello, I am your computer talking." << endl;
    return 0;
}
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_856_0.png)

You don’t even need to use Code::Blocks to perform this task. Any editor that produces plain-text output will work fine. For example, you could use Notepad to produce the code in Windows.

To use Boost.Build, you also need to create a `Jamfile.v2` file, which is just another plain-text file that you can create using Notepad or another text editor. The resource at https://www.boost.org/doc/libs/1_33_1/doc/html/bbv2/advanced/jamfiles.html makes things look a bit complex, but for this example, it comes down to a single line of text:

```text
exe Hello : hello.cpp ;
```

Notice the space between cpp and ;. You must include this space or the build process will fail. The error message isn’t very helpful either. It tells you that you’ve encountered an odd escape character and then the end of file. All that this file says is to create an executable named Hello from hello.cpp.

To perform the build, you open a command prompt in the folder you chose, type **b2 --toolset=gcc**, and press Enter. The output tells you what Boost.Build does:

```text
...found 8 targets...
...updating 5 targets...
gcc.compile.c++ bin\gcc-6.2.0\debug\hello.o
gcc.link bin\gcc-6.2.0\debug\Hello.exe
...updated 5 targets...
```

The fourth line tells you the location of the file: `bin\gcc-6.2.0\debug\`. When you go to this directory, you can type Hello, press Enter, and see the expected output. You can do a lot more than this section tells you, but it provides you with a very basic idea of how Boost.Build works.

Many organizations want to make changes to the Boost library to ensure that the library meets their needs or to augment the Boost library to meet a new requirement. Whenever you change something, there is a chance that the change will cause compatibility issues because it doesn’t meet the Boost library guidelines. In addition, a developer might introduce errors into the Boost library that others will find difficult to fix. The Inspect utility enables you to scan for potential Boost library errors after you make a change to it.

## Using Inspect

Start Inspect from the directory that you want to check. To make this process more efficient, make sure to set a path to the copy of Inspect that you built in the “Creating the Boost Tools” section of the chapter using the method appropriate for your platform. For example, when working with Windows, you type `path=C:\CodeBlocks\boost_1_73_0\dist\bin;%path%` and press Enter.

Inspect looks for errors in the current directory and all subdirectories. You can try it by checking the library files you find out how to build in the “Building the libraries” section, earlier in this chapter. These files usually appear in the `\CodeBlocks\boost_1_73_0\boost` directory. Normally, Inspect performs a complete check of the libraries. However, you can modify Inspect behavior using the following command-line switches to perform specific tests:

- `-license`
- `-copyright`
- `-crlf`
- `-end`
- `-link`
- `-path_name`
- `-tab`
- `-ascii`
- `-apple_macro`
- `-assert_macro`
- `-deprecated_macro`
- `-minmax`
- `-unnamed`
- `-version-string version_message`

![](img/128ab511de4e7360e167e3b15cdd5dd0_857_0.png)

You can use any number of these command-line switches. If you forget the Inspect command-line switches, type `Inspect -help` and press Enter. Inspect shows you a list of the command-line switches that you can use for testing.

**-version-string** *version_message*: Reduces the amount of output text by locating entries with a specific version string (as defined by *version_message*). What you're normally looking for is the version string provided with the library, such as 1_73_0 for the 1.73.0 version.

![](img/128ab511de4e7360e167e3b15cdd5dd0_859_0.png)

Inspect is sensitive about the ordering of command-line switches. You must place the `-cvs`, `-text`, or `-brief` command-line switch first, followed by the test switches; otherwise, Inspect displays an error message. The website at https://www.boost.org/doc/libs/1_73_0/tools/inspect/index.html tells you more about working with Inspect.

## Understanding BoostBook

The world abounds with documentation formats — everything from .docx files produced by Word to the seemingly ubiquitous .pdf file. Of all the documentation formats, the most universal and compatible is the lowly .txt file. However, .txt files lack formatting (except for control characters like tab, carriage return, and linefeed), which means that they limit you solely to words, which may not be enough to describe your documentation. Because you can choose from so many different file formats, and formatting code can prove especially difficult, the Boost library relies on a special document format called BoostBook.

![](img/128ab511de4e7360e167e3b15cdd5dd0_859_1.png)

Documentation seems to be the bane of developers everywhere. No one seems to want to write the documentation, and the attempts at documentation often leave readers with more questions than answers. BoostBook won’t make you a good writer. Although it does help you produce highly formatted documentation with a standardized format, it can’t overcome deficiencies in writing skill. When creating documentation for your project, the best writer in your group is still the unsurpassed choice for documentation tasks.

If you have installed the Boost library using the instructions in the “Obtaining and Installing Boost for Code::Blocks” section of this chapter, you already have access to BoostBook. However, as with some other Boost utilities, you need to know a bit about Python to use this feature. In addition, you need an Apache server setup and must also download a number of other utilities. In short, even though BoostBook is accessible from a Boost library perspective, you still need to do some work to make this feature useful. The instructions at https://www.boost.org/doc/libs/1_73_0/doc/html/boostbook/getting/started.html describe the additional steps you need to perform.
