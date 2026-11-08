```
friend ostream& operator<<(ostream& os, const Calendar& c) {
    return os << format("{:04}-{:02}-{:02}", c.y_, c.m_, c.d_);
}
void advance() { // +1 day
    auto maxd = mlens_[m_-1];   // 0-based vector
    if(m_ == 2 && leapyear())
        maxd += 1;              // February in a leap year
    if(d_ >= maxd) {
        d_ = 1;
        if(m_ >= 12) { m_ = 1; y_ += 1; }
        else { m_ += 1; }
    } else { d_ += 1; }
}
};
const std::vector<int> Calendar::mlens_ = {31,28,31,30,31,30,31,31,30,31,30,31};
```

**Listing 18.14** A simple calendar class.

With advance, you can proceed to the next valid date. Note that here I let both the day and the date start at one (making it output-friendly), not at zero like some other APIs. Let's briefly test the calendar:

```
int main() {
    Calendar cal(2024, 2, 28);
    std::cout << cal << '\n'; // Output: 2024-02-28
    cal.advance();
    std::cout << cal << '\n'; // Output: 2024-02-29
    cal.advance();
    std::cout << cal << '\n'; // Output: 2024-03-01
}
```

Now we have two practical—but separate—classes. A calendar clock now contains both.

```
// https://godbolt.org/z/zh5cPG7TK
class CalendarClock : public Clock, public Calendar {
public:
    CalendarClock(int y, int m, int d, int hh, int mm, int ss)
    : Calendar{y,m,d}, Clock{hh,mm,ss} {}
    void tick() {     // +1 second
        auto prev_h = h_;
        Clock::tick();    // Call base class method
        if(h_ < prev_h) { // if new day
            advance();    // ... advance calendar
        }
    }
};
```