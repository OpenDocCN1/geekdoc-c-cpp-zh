
On the other hand, if `CreateCurExchanger` fails to create the `XML_CurrencyExchanger` object, then an empty `all_my_options` is returned, and an error message is printed on line [91].
In this section, we learned about the following:

- Using the filesystem path object
- Composing a namespace inside another namespace (nested namespaces)
- Using `std::transform` to copy elements of `std::map` to a file
- Polymorphism when passing a derived object to a function defined to accept an object of the base class

## 6.2.6 Building a Static Library and a Terminal Window Application

We could easily add the `main` function to the previous example to create a terminal window version of our application. But since our project is growing and we have further plans to use the *CurrencyCalc* component from Figure 3.29 in various projects, it is a good idea to split it from the main function and put into a separate *static library*. The new arrangement of the software components is shown in UML component diagram in Figure 6.8.

To build a static library out of an application project, we need to do the following:

- 1. Remove the `main` function (i.e. the entire file containing main). It can then be used in other projects, as we will discuss.
- 2. Change the *CMakeLists.txt* file to generate a *static library project*,<sup>2</sup> as discussed in Appendix A.6.1.
- 3. Run *CMake.exe*, build a library project, and then build the library.

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_420_0.png)

**Figure 6.8**  UML component diagram of the basic *CurrencyExchanger*.

This way, we can build our first library, named *CurrencyCalc_Lib*. The new *CurrencyCalc_Terminal* component is linked to *CurrencyCalc_Lib*, as shown in Figure 6.8. It contains only the `main` function, as shown in Listing 6.7.

2 It is also possible to build a library without using the *CMake* tool. That is, we can create a new project in our programming environment, select its type as a static library, and manually add the files. However, *CMake* gives us flexibility between various platforms and programming tools.

| Member | Description |
| --- | --- |
| /- | Path concatenation, which appropriately inserts slash or backslash symbols, depending on the filesystem. Multiple such symbols are compressed to one. |
| / | Concatenates paths without adding separators (like string). |
| filename | Returns a filename (File.txt). |
| stem | Returns a stem (File). |
| extension | Returns an extension (.txt). |
| parent_path | Returns a parent path.^ |
| relative_path | Returns a relative path. |
| root_directory | Returns the root directory. |
| root_name | Returns the root name. |
| root_path | Returns the root path. |

| Object | Description | Examples |
| path | path is a class that represents paths to files, directories, and their links in various systems. It behaves like a container and supports many useful functions for splitting the path and concatenating parts. Selected members of the path class: | To use the new filesystem features of C++, the filesystem header needs to be included. fs is a short name for the std::filesystem, defined as follows: 1 #include <filesystem> 2 3 namespace fs = std::filesystem; The following function on line [6] converts a wide string std::wstring into a fs::path object. Then, on lines [9-10], each part of the path is printed on the screen. 4 void DisplayPathParts( const wstring & inPath_str ) { 5 6 const fs::path inPath( inPath_str ); 7 8 // We can iterate through different parts of a path 9 for( const auto & p : inPath ) 10 wcout << p << "\n"; 11 } For the example input pathb D:\\Research\\SC++\\Projects\\CCppBookCode\\ReadMe.txt the following output is obtained: D: Research RC Projects CCppBookCode ReadMe.txt |

| Object | Description | Examples |
| --- | --- | --- |
| file_size | Returns the file size in bytes. | \
| is_regular_ file | Returns true if a path represents a regular file (i.e. not a directory and not a link). | \
| file_status | Returns an object with information about a file. | The following function prints basic information about the supplied path to a directory or a file: \
|  |  | void DisplayDirFileInfo( const wstring & inPath_str ) { \
|  |  |  const fs::path inPath( inPath_str ); \
|  |  |  \
|  |  |  wcout << L"exists - \\t\\t" << fs::exists( inPath ) << endl; \
|  |  |  \
|  |  |  // Let's call all important members of fs::path \
|  |  |  wcout << L"filename - \\t\\t" << inPath.filename() << endl; \
|  |  |  wcout << L"stem - \\t\\t" << inPath.stem() << endl; \
|  |  |  wcout << L"extension - \\t\\t" << inPath.extension() << endl; \
|  |  |  \
|  |  |  // If a file, then print its size in bytes \
|  |  |  if( fs::is_regular_file( inPath ) ) o << val << mp; \
|  |  |  std::cout << L"file size - \\t\\t" << fs::file_size( inPath ) << endl; \
|  |  |  \
|  |  |  wcout << L"parent_path - \\t\\t" << inPath.parent_path() << endl; \
|  |  |  wcout << L"relative_path - \\t\\t" << inPath.relative_path() << endl; \
|  |  |  \
|  |  | }

| 19 | wcout << L"root_directory - \\t" << inPath.root_directory() << endl; |
| 20 | wcout << L"root_name - \\t" << inPath.root_name() << endl; |
| 21 | wcout << L"root_path - \\t" << inPath.root_path() << endl; |
|    | To call file_size on line [14], an object is checked on line [13] with is_regular_file to see if it is a valid file. On lines [8-10], as well as [16-21], numerous members of path are called to get parts of the path. For an example C:\\Temp\\Readme.txt input file in the test system, the following is obtained: |
|    | exists - 1
|    | filename - ReadMe.txt
|    | stem - ReadMe
|    | extension - .txt
|    | file_size - 44
|    | parent_path - C:\\Temp
|    | relative_path - Temp\\ReadMe.txt
|    | root_directory - \\
|    | root_name - C:
|    | root_path - C:\\ |

| Object | Description | Examples |
|---|---|---|
| `copy` | Copies files and/or directories with their contents. | The following function shows how to create two directories [13, 16] and then create a file in one of them [19], copy that file to the second directory [22], move that file back to the first directory [27], and finally remove all files and directories [31]. The last function should be used with great care. To concatenate elements of a path, on line [9], the overloaded `/` operator of the path class is used. |
| `remove` | Removes a file or a directory with its contents. |  |
| `remove_all` |  |  |
| `create_directory` | Creates a directory or directories. |  |
| `create_directories` |  |  |
| `rename` | Renames or moves a file. |  |

```cpp
void CreateDirsAndFiles(const wstring& subPath, const wstring& subdir)
{
    try
    {
        // There are conventions stating where to put the path
        filesystem::path subPath;
        // Use overloaded operator / to
        // add path to directory
        indirPath /= subdir; // add subdir
        // Create directory
        fs::path sub_2_path{ indirPath / L"subdir_1" };
        fs::create_directory(sub_2_path); // create subdir_1
        fs::path sub_2_path{ indirPath / L"subdir_2" };
        fs::create_directories(sub_2_path); // create subdir_2
        // Create a new file
    }
}
```

```cpp
void CreateDirsAndFiles(const wstring& subPath, const wstring& subdir)
{
    try
    {
        // There are conventions stating where to put the path
        filesystem::path subPath;
        // Use overloaded operator / to add subdirectory
        indirPath /= subdir;
        // Create directory
        fs::path sub_2_path{ indirPath / L"subdir_1" };
        fs::create_directory(sub_2_path);
        fs::path sub_2_path{ indirPath / L"subdir_2" };
        fs::create_directories(sub_2_path);
        // Create a new file
    }
}
```
