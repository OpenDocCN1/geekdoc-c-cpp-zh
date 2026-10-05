representation, where Monday is 1.
%U is replaced by the week number, using the locale's alternative numeric symbols.
%V is replaced by the ISO 8601 week number, using the locale's alternative numeric symbols.

%Ow is replaced by the weekday as a number, using the locale's alternative numeric symbols.
%OW is replaced by the week number of the year, using the locale's alternative numeric symbols.

%Oy is replaced by the last 2 digits of the year, using the locale's alternative numeric symbols.

5 %G, and %V give values according to the ISO 8601 week-based year. In this system, weeks begin on a Monday and 1 of the year is the week that includes January 4th, which is also the week that includes the first Thursday of the year, and is also the first week that contains at least four days in the year. If the first Monday of January is the 2nd, 3rd, or 4th, the preceding days are part of the last week of the preceding year; thus, for Saturday 2nd January 1999, %G is replaced by 1998 and %V is replaced by 53. If December 29th, 30th, or 31st is a Monday, and any days are part of week 1 of the following year. Thus, for Tuesday 30th December 1997, %G is replaced by 1998 and %V is replaced by 01.

6 If a conversion specifier is not one of the above, the behavior is undefined.

7 In the "C" locale, the E and O modifiers are ignored and the replacement strings for the following specifications:
%a the first three characters of %A.
%A one of "Sunday", "Monday", ..., "Saturday"
%b the first three characters of %B.
%B one of "January", "February", ..., "December"
%c equivalent to %a %b %e %T %Y
%p one of "AM" or "PM"
%r equivalent to %I:%M:%S %p
%x equivalent to %m/%d/%y
%X equivalent to %T.
%Z implementation-defined.

Returns
If the total number of resulting characters including the terminating null character is not more than maxsize, the strftime function returns the number of characters placed into the array pointed to by s not including the terminating null character. Otherwise, zero is returned and the contents of the array are indeterminate.