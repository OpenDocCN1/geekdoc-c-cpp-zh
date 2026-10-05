# Description

The gmtime function converts the calendar time pointed to by timer into a broken-down time, expressed as UTC.

# Returns

The gmtime function returns a pointer to the broken-down time, or a null pointer if the specified time cannot be converted to UTC.

# 7.27.3.4 The localtime function

# Synopsis

```
#include <time.h>
struct tm *localtime(const time_t *timer);
```

# Description

The localtime function converts the calendar time pointed to by timer into a broken-down time, expressed as local time.

# Returns

The localtime function returns a pointer to the broken-down time, or a null pointer if the specified time cannot be converted to local time.

# 7.27.3.5 The strftime function

# Synopsis

```
#include <time.h>
size_t strftime(char * restrict s,
size_t maxsize,
const char * restrict format,
const struct tm * restrict timeptr);
```

# Description

The strftime function places characters into the array pointed to by s as controlled by the string pointed to by format. The format shall be a multibyte character sequence, beginning and ending in its initial state. The format string consists of zero or more conversion specifiers and ordinary multibyte characters. A conversion specifier consists of a % character, possibly followed by an E or O modifier character (described below), followed by a character that determines the behavior of the conversion specified. All multibyte characters (including the terminating null character) are copied unchanged into the array. If copying takes place between objects that overlap, the behavior is undefined. No more than maxsize characters are placed into the array.

Each conversion specifier is replaced by appropriate characters as described in the following list. The appropriate characters are determined using the LC_TIME category