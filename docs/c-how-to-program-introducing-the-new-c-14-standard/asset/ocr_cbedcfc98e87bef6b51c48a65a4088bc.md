```
```cpp
// set minute value
Time& Time::setMinute(int m) {  // note Time& return
    if (m >= 0 && m < 60) {
        minute = m;
    }
    else {
        throw invalid_argument("minute must be 0-59");
    }
    return *this; // enables cascading
}

// set second value
Time& Time::setSecond(int s) {  // note Time& return
    if (s >= 0 && s < 60) {
        second = s;
    }
    else {
        throw invalid_argument("second must be 0-59");
    }
    return *this; // enables cascading
}

// get hour value
unsigned int Time::getHour() const { return hour; }

// get minute value
unsigned int Time::getMinute() const { return minute; }

// get second value
unsigned int Time::getSecond() const { return second; }

// return Time as a string in universal-time format (HH:MM:SS)
string Time::toUniversalString() const {
    ostringstream output;
    output << setfill('0') << setw(2) << getHour() << ":"
           << setw(2) << getMinute() << ":" << setw(2) << getSecond();
    return output.str();
}

// return Time as string in standard-time format (HH:MM:SS AM or PM)
string Time::toStandardString() const {
    ostringstream output;
    output << ((getHour() == 0 || getHour() == 12) ? 12 : getHour() % 12)
           << ":" << setfill('0') << setw(2) << getMinute() << ":" << setw(2)
           << getSecond() << (hour < 12 ? " AM" : " PM");
    return output.str();
}
```
```