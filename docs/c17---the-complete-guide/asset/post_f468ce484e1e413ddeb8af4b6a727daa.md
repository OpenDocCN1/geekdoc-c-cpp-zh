
```
namespace fs = std::filesystem;

switch (fs::path p{argv[1]}; status(p).type()) {
    case fs::file_type::not_found:
        std::cout << "path \"" << p.string() << "\" does not exist\n";
        break;
    case fs::file_type::regular:
        std::cout << '\'' << p.string() << "\" exists with "
                  << file_size(p) << " bytes\n";
        break;
    case fs::file_type::directory:
        std::cout << '\'' << p.string() << "\" is a directory containing:\n";
        for (const auto& e : std::filesystem::directory_iterator{p}) {
            std::cout << "  " << e.path().string() << '\n';
        }
        break;
    default:
        std::cout << '\'' << p.string() << "\" is a special file\n";
        break;
}
}
```

## Namespace fs

First, we do something very common: we define fs as a shortcut for namespace std::filesystem:

```
namespace fs = std::filesystem;
```

Using this namespace we initialize, for example, the path p in the switch statement:

```
fs::path p{argv[1]};
```

The switch statement is an application of the new switch with initialization, where we initialize the path and provide different cases for its type:

```
switch (fs::path p{argv[1]}; status(p).type()) {
    ...
}
```

The expression status(p).type() creates a file_status for which type() creates a file_type. This way we can handle the different types directly instead of following a chain of calls like is_regular_file(), is_directory(), and so on. The type is intentionally provided in multiple steps (calling status() and then type()) so that we do not have to pay the price of operating system calls if we are not interested in all information.

Note also that an implementation-specific file_type might exist. For example, Windows provides the special file type junction. However, using it is not portable.

## 20.1.3 Create Different Types of Files

After having only read-access to the filesystem, let us now give a first example of modifying it. The following program creates different kinds of files in the subdirectory tmp:

filesystem/createfiles.cpp

```
#include <iostream>
#include <fstream>
#include <filesystem>
#include <cstdlib>    // for std::exit() and EXIT_FAILURE

int main ()
{
namespace fs = std::filesystem;
try {
    // create directories tmp/test/ (if they don't exist yet):
    fs::path testDir{"tmp/test"};
    create_directories(testDir);

    // create data file tmp/test/data.txt:
    auto testFile = testDir / "data.txt";
    std::ofstream dataFile{testFile};
    if (!dataFile) {
        std::cerr << "OOPS, can't open \"" << testFile.string() << "\"\n";
        std::exit(EXIT_FAILURE);  // exit program with failure
    }
    dataFile << "The answer is 42\n";

    // create symbolic link from tmp/slink/ to tmp/test/:
    create_directory_symlink("test", testDir.parent_path() / "slink");
}
catch (const fs::filesystem_error& e) {
    std::cerr << "EXCEPTION: " << e.what() << '\n';
    std::cerr << "    path1: \"" << e.path1().string() << "\"\n";
}

    // recursively list all files (also following symlinks)
    std::cout << fs::current_path().string() << ":\n";
    auto iterOpts{fs::directory_options::follow_directory_symlink};
    for (const auto& e : fs::recursive_directory_iterator(".", iterOpts)) {
        std::cout << "  " << e.path().lexically_normal().string() << '\n';
    }
}
```

Let us also go through this program step by step.

## Namespace fs

First, again, we define fs as the usual shortcut for namespace std::filesystem:

```
namespace fs = std::filesystem;
```

Using this namespace we initialize the paths for a basic subdirectory for temporary files:

```
fs::path testDir{"tmp/test"};
```

### Creating Directories

We then try to create the subdirectory:

```
create_directories(testDir);
```

By using create_directories(), we create all missing directories of the whole passed path (there is also create_directory() to create a directory only inside an existing directory).

It is not an error to perform this call if the directory already exists. However, any other problem is an error and raises a corresponding exception.

If testDir already exists, create_directories() returns false. Thus, you could also call:

```
if (!create_directories(testDir)) {
    std::cout << "\"" << testDir.string() << "\" already exists\n";
}
```

### Creating Regular Files

Then we create a new file /tmp/test/data.txt with some contents:

```
auto testFile = testDir / "data.txt";
std::ofstream dataFile{testFile};
if (!dataFile) {
    std::cerr << "OOPS, can't open \"" << testFile.string() << "\"\n";
    std::exit(EXIT_FAILURE);  // exit program with failure
}
dataFile << "The answer is 42\n";
```

Here, we use operator / to extend a path, which we then pass as an argument to the constructor of a file stream. As you can see, the creation of a regular file can still only be done with the existing I/O streams library. However, a new overload for the constructors is provided to allow us to directly pass a filesystem path (this also applies to functions such as open()).

Note that you should still always check whether the creation/opening of the file was successful. A lot of things can go wrong here (see below).

### Creating Symbolic Links

The next statement tries to create a symbolic link tmp/slink that refers to directory tmp/test:

```
create_directory_symlink("test", testDir.parent_path() / "slink");
```

Note that the first argument defines the path from the view of the link created. Thus, you have to pass "test" instead of "tmp/test" to effectively link from tmp/slink to tmp/test. If you called:

```
std::filesystem::create_directory_symlink("tmp/test", "tmp/slink");
```

you would effectively create tmp/slink as a symbolic link to tmp/tmp/test.

Note that often, calling create_symlink() instead of create_directory_symlink() also works. However, some operating systems have special handling for symbolic links to directories or perform better when they know that a file is a directory, which means that you should use create_directory_symlink() if you know that the symbolic link refers to a directory.

Finally, note that this call might fail on Windows systems and cause error handling, because you might need administrator rights to create a symbolic link there.

### Recursive Directory Iteration

Finally, we recursively list our current directory:

```
auto iterOpts = fs::directory_options::follow_directory_symlink;
for (auto& e : fs::recursive_directory_iterator(".", iterOpts)) {
    std::cout << "   " << e.path().lexically_normal().string() << '\n';
}
```

Note that we use a recursive directory iterator and pass the option follow_directory_symlink to also follow symbolic links. Therefore, we should get an output like the following on POSIX-based systems:

/home/nico:
...
tmp
tmp/slink
tmp/slink/data.txt
tmp/test
tmp/test/data.txt
...

and an output like the following on Windows systems:

C:\Users\nico:
...
tmp
tmp\slink
tmp\slink\data.txt
tmp\test
tmp\test\data.txt
...

Note that we use lexically_normal() when we print the path of all directory entries. If we skip that, the path of the directory entries would contain a prefix with the directory the iterator was initialized with. Thus, printing just the paths inside the loop:

```
auto iterOpts = fs::directory_options::follow_directory_symlink;
```

```
for (auto& e : fs::recursive_directory_iterator(".", iterOpts)) {
    std::cout << "   " << e.path() << '\n';
}
```

would output the following on POSIX-based systems:

all files:
...
"./testdir"
"./testdir/data.txt"
"./tmp"
"./tmp/test"
"./tmp/test/data.txt"

And on Windows, the output would be:

all files:
...
".\\testdir"
".\\testdir\\data.txt"
".\\tmp"
".\\tmp\\test"
".\\tmp\\test\\data.txt"

Thus, by calling lexically_normal() we yield the normalized path, which removes the leading dot for the current directory. Furthermore, as written before, by calling string() we avoid each path being written quoted, which would be OK for POSIX-based systems (just having the name in double quotes), but would look very surprising on Windows systems (because each backslash is escaped by another backslash).

### Error Handling

Filesystems are a source of trouble. You might not be able to perform operations due to using invalid characters for file names, not having necessary permissions, or other processes might modify the filesystem while you are dealing with it. Thus, depending on the platform and permissions, a couple of things can go wrong in this program.

For those cases not covered by return values (such as the case where the directory already exists), we catch the corresponding exception and print the general message and the first path in it:

```
try {
    ...
}
catch (const fs::filesystem_error& e) {
    std::cerr << "EXCEPTION: " << e.what() << '\n';
    std::cerr << "      path1: \"" << e.path1().string() << "\"\n";
}
```

For example, if we cannot create the directory, a message such as the following might be printed:

```
EXCEPTION: filesystem error: cannot create directory: [tmp/test]
    path1: "tmp/test"
```
