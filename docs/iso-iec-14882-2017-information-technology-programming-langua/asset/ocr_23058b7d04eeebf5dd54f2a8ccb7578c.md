# ISO/IEC 14882:2017(E)

+   12 Effects: As a formatted input member (as described in 30.7.4.2.1) of in. If a sentry
object is constructed from it, if in is also valued, and stored in c. Otherwise,
function calls setstate(failbit).

+   13 Returns: in.

+   14 Effects: As an unformatted input function (30.7.4.3). If sb is null, calls setstate(fail-
bit), which may throw ios_base::failure(30.5.5.4). After a sentry object is constructed, extracts
characters from* and inserts them into the output sequence controlled by sb. Characters
extracted and inserted until the end of input

+   (14.1) end-of-file sequence

+   (14.2) inserting into the output sequence fails (in case the character to be inserted is not extracted)

+   (14.3) an exception occurs (in case the exception is caught).

If the function cannot, it calls setstate(failbit), which may throw ios_base::
failure (30.5.5.4) if it cannot extract because it catches an exception while throwing
characters from*this and failbit is turned on*310 in *this error state. (Exceptions from basic_ios<>::clear())
not caught or rethrown). If (exceptions()&badbit) != 0 then the exception is rethrown. It counts
the number of characters extracted. If no exception has been thrown it ends by storing the count in a
object and returning the value. In any case the sentry is destroyed before leaving the
unformatted input function.

+   16 Returns: this.

# 30.7.4 Unformatted input functions

1 Each unformatted input begins execution by constructing an object of sentry with return, when converted to a
type bool, the constructor proceeds to obtain the requested input. If the sentry object returns true, when converted. Otherwise, if the sentry constructor exists
by throwing an exception if the sentry object returns fails, converted to a value of type bool,
function returns without invalidating any input. In either case the number of characters extracted is
set to the value of the input function taking the maximum size as an argument. If it reads a
ull character (char*) in the first location of or. If an exception occurs during input then
ios::badbit is turned on310 in this error state. (Exceptions from basic_ios<>::clear())
not caught or rethrown). If (exceptions()&badbit) != 0 then the exception is rethrown. It counts
the number of characters extracted. If no exception has been thrown it ends by storing the count in a
object and returning the value. In any case the sentry is destroyed before leaving the
unformatted input function.

+   2 Effects: None. This member function does not behave as an unformatted input function (as described
above).

+   3 Returns: The number of characters extracted by the last unformatted input member function called
the object.

```
int_type get();
```

+   4 Effects: As an unformatted input function (as described above). After constructing a sentry
object, extracts a character c, if one is available. Otherwise, the function calls setstate(failbit),
which may throw ios_base::failure(30.5.5.4).

> 310) This does not throw without causing an ios::failbit to be thrown

§ 30.7.4 ©ISO/IEC 2017 - All rights reserved 1192