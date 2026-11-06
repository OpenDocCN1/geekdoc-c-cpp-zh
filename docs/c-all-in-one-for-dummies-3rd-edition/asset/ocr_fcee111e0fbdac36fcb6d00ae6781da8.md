+   - **status:** Provides access to a Boost-wide test suite. Generally, you won’t need the contents of this folder unless you plan to augment the Boost libraries in some way.

+   - **tools:** Contains a wealth of tools you use when working with Boost. Much of this chapter tells you about these tools. You must build the tools before you can use them. Each folder contains complete instructions, but you’ll also find an example of building the tools later in this section.

# Using the header-only libraries

No matter which platform you work with, the header-only libraries are ready for use immediately after you unpack Boost. These libraries appear in the `boost_1_55_0\boost\` directory. Each library is contained in a separate subdirectory and you access the library through its header file. Boost 1.55.0 supports 97 different header-only libraries that address all sorts of issues, such as incremental statistical computation. (That particular area is covered by the accumulators library, which is found in the `accumulators\` subdirectory.)

Having access to the library doesn’t mean you’ll know how to use it right out of the box, but the Boost folks do make an effort to provide you with good documentation so you can discover how to use Boost. Look in the `boost_1_55_0\libs\` directory and you see another set of subdirectories containing the names of libraries, such as `accumulators\`. Each of these subdirectories contains a minimum of three subdirectories:

![](bbox=[0.142, 0.572, 0.229, 0.643])

+   - **doc:** The documentation for understanding and using the library. Access the documentation for an individual library by opening the `index.htm` file in its subdirectory. Access the documentation for Boost as a whole by opening the `libraries.htm` file found in the `boost_1_55_0\libs\` directory.

+   - **example:** A somewhat simple application that demonstrates how to use the library. (The example is designed to show both usage and functionality, so some complex libraries have larger examples to demonstrate them.) Some libraries include multiple examples to fully demonstrate the library’s functionality.

+   - **test:** A test suite you can use to ensure that any changes you make to Boost won’t break the library or cause undesirable side effects.

Depending on the needs of the library, you may find additional subdirectories that contain other information or resources, such as tools. Some of the libraries require additional processing before you can use them. The next section of the chapter describes the building process so that you have a complete Boost installation. Make absolutely certain that you build the libraries before you proceed.