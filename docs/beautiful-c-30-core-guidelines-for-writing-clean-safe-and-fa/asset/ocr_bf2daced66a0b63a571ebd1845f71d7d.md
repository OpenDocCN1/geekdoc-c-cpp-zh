```
```cpp
title) {
    auto report = Report(title);
    int item_count = report_rendering(1, 2, report);
    item_count += report_fileIO(0, 0, 1024, report);
    return {report, item_count};
}
```
```

If we were to return the output values as a single object, we would have to change the file signatures to:

Click here to view code image

```
```cpp
std::pair <Report, int> report_rendering(int, int, Report&);
std::pair <Report, int> report_fileIO(int, int, int, Report&);
```
```

This would have a slightly unpleasant effect on the code:

Click here to view code image

```
```cpp
std::pair<Report, int> collect_report(const char* title) {
    auto report = Report(title);
    int item_count = report_rendering(1, 2, report).second;
    item_count += report_fileIO(0, 0, 1024, report).second;
    return {report, item_count};
}
```
```

The trailing .second is ugly, and the first item in the pair is being discarded. The caller already has the object, since they passed it in, so why return it?

In fact, if we restore the function prototype return types, and move the in-out parameter to the position before the input parameters, we get this: