```
class Report { ...};

int report_rendering(int, int, Report&);  // input parameters..
int report_fileIO(int, int, int, Report&); // then in-out parameter

std::pair<Report, int> collect_report(const char* title) {
    auto report = Report(title);
    int item_count =  report_rendering(1, 2, report);
    item_count += report_fileIO(0, 0, 1024, report);
    return {report, item_count};
}
```