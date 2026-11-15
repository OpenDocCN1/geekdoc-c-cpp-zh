+   char* strrchr(const char *s, int c);
+   returns a pointer to the last occurrence of the character c in the string pointed to by s
+   
+   size_t strspn(const char *s, const char *t);
+   returns the length of the initial segment of the string pointed to by s that consists entirely of characters in the string pointed to by t
+   
+   char* strstr(const char *s, const char *t);
+   returns a pointer to the start of the string pointed to by t within the string pointed to by s

# <ctime>

The header file <ctime> defines two macros, four types, and several functions for representing and manipulating calendar time and local time. The types clock_t and time_t are arithmetic types capable of representing times, and the structure tm contains a calendar time broken into seconds (tm_sec), minutes (tm_min), hours (tm_hour), day of the month (tm_mday), months since January (tm_mon), years since 1900 (tm_year), days since Sunday (tm_wday), days since January 1 (tm_yday), and a daylight saving time flag (tm_isdst); the order of the values in the structure is system dependent. The related macros are the following:

+   CLOCKS_PER_SEC
+   number per second of the value returned by the clock function
+   
+   NULL
+   an integer representing binary zero

Function prototypes and brief descriptions of their related computations follow:

+   char* asctime(const struct tm *timeptr);
+   returns a pointer to the string containing a converted time
+   
+   clock_t clock(void);
+   returns the current processor time
+   
+   char* ctime(const time_t *time);
+   returns a pointer to a string containing a converted time
+   
+   double difftime(time_t time1, time_t time0);
+   computes the difference between two calendar times
+   
+   struct tm *gmtime(const time_t *timer);
+   returns a pointer to a time expressed in Coordinated Universal Time
+   
+   struct tm *localtime(const time_t *timer);
+   returns a pointer to a time converted from calendar time
+   
+   time_t mktime(struct tm *timeptr);
+   converts the broken-down time to a calendar time value
+   
+   time_t time(time_t *timer);
+   returns the current calendar time
+   
+   size_t strftime(char *s, size_t maxsize, const char *format, const struct tm *timeptr);
+   converts time into a formatted multibyte character sequence