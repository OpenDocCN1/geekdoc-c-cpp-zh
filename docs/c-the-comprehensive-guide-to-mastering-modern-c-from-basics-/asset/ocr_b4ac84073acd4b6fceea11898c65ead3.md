```
m = 0;
if(h_ >= 23) h_ = 0;
else { h_ += 1; }
} else { m += 1; }
} else { s_ += 1; }
}
;
```

**Listing 18.13** The clock and calendar combination results in a clock with a calendar.

# Using this clock is very simple:

```
int main() {
  clock(23, 59, 59);
  std::cout << clock << '\n'; // Output: 23:59:59
  clock.tick();
  std::cout << clock << '\n'; // Output: 00:00:00
}
```

# The calendar is just as simple:

```
// https://godbolt.org/z/56Ec35Tf
// includes and usings
struct Calendar {
  int y_, m_, d_;
  static const std::vector<int> mlens;
  bool leapyear() const {
    if(y_ % 4 != 0) return false;
    if(y_ % 100 != 0) return true;
    if(y_ % 400 == 0) return false;
    return true;
  }
public:
  Calendar(int year, int month, int day)
    : y_(year), m_(month), d_(day) {}
  void setCalendar(int year, int month, int day) {
    y_ = year; m_ = month; d_ = day;
  }
  friend ostream& operator<<(std::ostream& os, const Calendar& c) {
    return os << format("{:04}-{:02}-{:02}", c.y_, c.m_, c.d_);
  }
  void advance() { // +1 day
  auto maxd = mlens_[-1]; // 0-based vector
  if(m_ == 2 && leapyear()) // February in a leap year
  maxd += 1;
};
```