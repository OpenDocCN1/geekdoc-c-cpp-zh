```
cpy(fin,fout); // read American English, write French // ...
fin2.imbue(locale{"fr_FR.UTF-8"}); // French
fout2.imbue(locale{"en_US.UTF-8"}); // American English
cpy(fin2,fout2); // read French, write American English // ...
}
```

Given these streams:

```
Apr 12, 1999 1000.3
Apr 13, 1999 345.45
Apr 14, 1999 9688.321
...
3 juillet 1950 10,3
3 juillet 1951 134,45
3 juillet 1952 67,9
...
```

this program would produce:

```
12 avril 1999 1000,3
13 avril 1999 345,45
14 avril 1999 9688,321
...
July 3, 1950 10.3
July 3, 1951 134.45
July 3, 1952 67.9
...
```

Much of the rest of this chapter is devoted to describing the mechanisms that make this possible and explaining how to use them. However, most programmers will have little reason to deal with the details of locales and will never explicitly manipulate a locale. At most, they will simply retrieve a standard locale and imbue a stream with it (§38.4.5.1).

+   The concept of localization (internationalization) is simple. However, practical constraints make the design and implementation of locale quite intricate:
+   
+   [1] A locale encapsulates cultural conventions, such as the appearance of a date. Such conventions vary in many subtle and unsystematic ways. These conventions have nothing to do with programming languages, so a programming language cannot standardize them.
+   
+   [2] The concept of a locale must be extensible, because it is not possible to enumerate every cultural convention that is important to every C++ user.
+   
+   [3] A locale is used in operations (e.g., I/O and sorting) from which people demand run-time efficiency.
+   
+   [4] A locale must be invisible to the majority of programmers who want to benefit from facilities “doing the right thing” without having to know exactly what “the right thing” is or how it is achieved.
+   
+   [5] A locale must be available to designers of facilities that deal with culture-sensitive information beyond the scope of the standard.

The mechanisms provided to compose those locales and to make them trivial to use constitute a little programming language of their own.