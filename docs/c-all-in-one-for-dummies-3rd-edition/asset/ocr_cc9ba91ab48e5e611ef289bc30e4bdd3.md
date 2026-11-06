# # Parsing Strings Using RegEx

Regular expressions are an important part of today’s computing environment. You use them to perform *pattern matching*, where the application finds a series of matching characters in a string. For example, if you want the user to enter values from 0 through 9 and nothing else, you can create a pattern that prevents the user from entering anything else. Using patterns in the form of regular expressions serves a number of important purposes:

+   - Ensures that your application receives precisely the right kind of input
+   - Enforces a particular data input format (such as the way you input a telephone number)
+   - Reduces security risks (for example, a user can't input a script in place of the data you wanted)

![](bbox=[0.16, 0.42, 0.24, 0.49])

Some developers make the mistake of thinking that a regular expression can prevent every sort of data input error. However, regular expressions are only one tool in an arsenal you must build against errant input. For example, a regular expression can't perform range checking. If you want values between 101 and 250, a regular expression will ensure that the user enters three digits; however, you must use range checking to prevent the user from entering a value of 100.

| Defining the pattern | |
|---|---|
| The RegEx library provides a number of methods for creating a pattern. For example, if you want the user to input only lowercase letters, you can create a range by using [a-z]. The example in this chapter shows how to create a simple three-digit numeric input. However, you can create a pattern for nearly any use. For example, a telephone number pattern might appear as ([0-9] [0-9] [0-9] [0-9] [0-9] [0-9] [0-9] [0-9] [0-9] [0-9], where a telephone number of 555 555-5555 is acceptable, but a telephone number of 555-555-5555 isn't. The RegEx library reference appears at http://www.boost.org/doc/libs/1_55_0/libs/regex/doc/html/index.html.<br><br>This chapter doesn't provide you with a full explanation of all the patterns you can create. | The best place to start discovering the basics of patterns is at http://www.boost.org/doc/libs/1_55_0/libs/regex/doc/html/boost_regex/syntax.html. It's important to note that older versions of Boost only supported the Perl syntax—newer versions support POSIX basic and POSIX extended syntax as well. Boost provides a wealth of pattern types.<br><br>How you use the pattern is just as important as how you create the pattern. For example, you can use RegEx_match to obtain a precise match. However, if you want to only search for a value, you use RegEx_search instead. The usage reference appears at http://www.boost.org/doc/libs/1_55_0/libs/regex/doc/html/boost_regex/ref.html. |