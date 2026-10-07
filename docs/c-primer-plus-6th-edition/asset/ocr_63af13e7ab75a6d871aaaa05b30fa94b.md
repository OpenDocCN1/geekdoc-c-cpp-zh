# 356 Chapter 7 Functions: C++'s Programming Modules

```
const int Seasons = 4;
const std::array<std::string, Seasons> Snames = 
{"Spring", "Summer", "Fall", "Winter"};
```

```
// function to modify array object
void fill(std::array<double, Seasons> * pa);
// function that uses array object without modifying it
void show(std::array<double, Seasons> da);
```

```
int main() {
    std::array<double, Seasons> expenses;
    fill(expenses);
    show(expenses);
    return 0;
}
```

```
void fill(std::array<double, Seasons> * pa) {
    using namespace std;
    for (int i = 0; i < Seasons; i++) {
        cout << "Enter " << Snames[i] << " * expenses: *";
        cin >> (*pa)[i];
    }
}
```

```
void show(std::array<double, Seasons> da) {
    using namespace std;
    double total = 0.0;
    cout << "\nEXPENSES\n";
    for (int i = 0; i < Seasons; i++) {
        cout << Snames[i] << " : $\
```

Here's a sample run:

Enter Spring expenses: 212
Enter Summer expenses: 256
Enter Fall expenses: 208
Enter Winter expenses: 344