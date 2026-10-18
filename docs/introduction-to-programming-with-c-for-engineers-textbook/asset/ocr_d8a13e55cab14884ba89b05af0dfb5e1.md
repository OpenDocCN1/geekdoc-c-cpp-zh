# Table 8.3 Common OpenMP constructs, clauses, and functions with examples.

| OpenMP directive | Description | Examples |
|---|---|---|
| `#pragma omp parallel for [clause[(,)] clause]` | Fork for loop operations to parallel threads. | In this example, a minimum value and its index are found in a vector. `omp parallel` starts a team of threads; `firstprivate` declares `loc_val` and `loc_offset` to be private for each thread and, at first, initialized exactly as in their definitions; and `shared` declares the objects to be co-used by all threads. `omp for nowait` says to execute the following for loop in parallel and not wait for other sub-loops, but to immediately proceed to `omp critical`. This is a guard for the critical section and can be entered by only one thread at a time. ```cpp
std::tuple<int, int> FindMin(const std::vector<int> & v)
{
    const auto data_num = v.size();
    if (data_num == 0)
        return std::make_tuple(-1, -1);

    const auto * src_data_ptr = v[0];
    auto sh_val = *src_data_ptr;
    auto sh_offset = 0;

    // Take an upper limit to find the lowest value
    auto loc_val = (std::numeric_limits<int>::max)();
    auto loc_offset = -1;

    // Use firstprivate to convey the initial values of loc_val and loc_offset.
    // Shared objects are listed in the shared clause.
    #pragma omp parallel default(none) \
        firstprivate(loc_val, loc_offset) \
        shared(sh_val, sh_offset, src_data_ptr, data_num)
}
``` |
| `#pragma omp parallel` | Starts independent units of work. |  |
| `#pragma omp single` | Ensures that exactly a single thread executes a block of code. |  |
| `#pragma omp critical` | Construction for mutual exclusion: at any instant only one thread can perform the block encompassed by `critical`. |  |
| `#pragma omp parallel sections` | Creates a team of threads, and starts independent sections. Sections execute in parallel to each other. |  |
| `#pragma omp section` | Starts independent units of work in a section. |  |
| `private(list)` | Declares a variable as private. Each thread contains its own uninitialized copy (for initialization, use `firstprivate`). |  |
| `firstprivate(list)` | Initializes a private variable with the value of the variable with the same name before entering the thread. |  |
| `lastprivate(list)` | Makes the last value of a private variable available after termination of a thread. |  |

```
std::tuple<int, int> FindMin(const std::vector<int> & v)
{
    const auto data_num = v.size();
    if (data_num == 0)
        return std::make_tuple(-1, -1);

    const auto * src_data_ptr = v[0];
    auto sh_val = *src_data_ptr;
    auto sh_offset = 0;

    // Take an upper limit to find the lowest value
    auto loc_val = (std::numeric_limits<int>::max)();
    auto loc_offset = -1;

    // Use firstprivate to convey the initial values of loc_val and loc_offset.
    // Shared objects are listed in the shared clause.
    #pragma omp parallel default(none) \
        firstprivate(loc_val, loc_offset) \
        shared(sh_val, sh_offset, src_data_ptr, data_num)
}
```