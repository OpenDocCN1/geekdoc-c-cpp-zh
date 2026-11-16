```
C++ program:

#include "boost/date_time/gregorian/gregorian.hpp"
#include "boost/date_time/posix_time/posix_time.hpp"
#include <iostream>
using namespace std;
namespace posix = gregorian;
using namespace boost::posix_time;

void ex_date_time(){
    boost::gregorian::date d(2014,4,1); // creating a date
    cout << " date: " << d << endl;
    cout << std::endl;

    boost::posix_time::ptime dt;
    stringstream ss("2014-mar-01 10:01:01.01");
    ss >> dt;
    cout << " date time just created: " << dt << endl;

    ptime now = second_clock::local_time(); //get the current time from the clock
    date today = now.date(); //Get the date part out of the time
    cout << " today: " << today << endl;
    date tomorrow = today + days(1); // add one date
    ptime tomorrow_start(tomorrow); //midnight
    time_duration remaining = tomorrow_start - now;
    cout<< "Time left till midnight: " << to_simple_string(remaining) << std::endl;
}
Output from C++ program:

date: 2014-Apr-01
date time just created: 2014-Mar-01 10:01:01.010000
today: 2014-Jun-30
Time left till midnight: 10:19:33
```

# 27.1 References

The Boost homepage is at http://www.boost.org/