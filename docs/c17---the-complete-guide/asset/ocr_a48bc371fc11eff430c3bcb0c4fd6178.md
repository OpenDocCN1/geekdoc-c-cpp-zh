First, we recursively collect all filesystem paths in the directory given as command-line argument:

```
std::filesystem::path root{argv[1]};

std::vector<std::filesystem::path> paths;
std::filesystem::recursive_directory_iterator dirpos{root};
std::copy(begin(dirpos), end(dirpos),
    std::back_inserter(paths));
```

Note that because we might pass an invalid path, possible (filesystem) exceptions are caught.

Then, we iterate over a collection of the filesystem paths to accumulate their sizes if they are regular files:

```
auto sz = std::transform_reduce(
    std::execution::par,                 // parallel execution
    paths.cbegin(), paths.cend(),        // range
    std::uintmax_t{0},                   // initial value
    std::plus<>(),                       // accumulate ...
    [](const std::filesystem::path& p) { // file size if regular file
        return is_regular_file(p) ? file_size(p)
            : std::uintmax_t{0};
    });
```

The new standard algorithm transform_reduce() operates as follows:

+   - The last argument is applied to each element. Here, the passed lambda is called for each path element and queries its size if it is a regular file.
+   - The second to last argument is the operation that combines all the sizes. Because we want to accumulate the sizes, we use the standard function object std::plus<>.
+   - The third to last argument is the initial value for the operation that combines all the sizes. The type of this value is the return type of the function. We convert 0 to the type of the return value of file_size(), std::uintmax_t. Otherwise, if we simply passed 0, we would narrow the result to int. Thus, if the list of paths is empty, the whole call returns 0.

Note that asking for the size of a file is a pretty expensive operation because it requires an operating system call. Therefore, using an algorithm that calls this transformation (from path to size) in parallel with multiple threads in any order and computes the sum pays off quite quickly. First measurements demonstrate a clear win (up to doubling the speed of the program).

Note also that you cannot pass the paths the directory iterator iterates over directly to the parallel algorithm, because directory iterators are input iterators, while the parallel algorithms require forward iterators.

Finally, note that transform_reduce() is defined in the header file <numeric> instead of <algorithm> (just like accumulate(), it counts as a numeric algorithm).

# 22.7 Afternotes

Parallelizing the STL algorithms was first proposed in 2012 by Jared Hoberock, Michael Garland, Olivier Giroux, Vinod Grover, Ujval Kapasi, and Jaydeep Marathe in http://wg21.link/n3408. It became a