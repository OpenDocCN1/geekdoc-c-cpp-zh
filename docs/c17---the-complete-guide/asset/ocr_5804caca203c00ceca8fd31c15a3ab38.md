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

# Namespace fs

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