done by a central thread and other threads are blocked.

+   - NR.6. Not: Put all cleanup actions at the end of a function and use goto exit.

This technique applies to C, but no longer to C++ the presence of RAII. If you don't use RAII, use gsl::finally.

+   - NR.7. Not: Make all data fields protected. Either a field is public or it is private. If you make something protected, then you have no control over who manipulates this data field, bypassing all access mechanisms, because someone can derive from your class. And thus the supposedly protected data field is as good as public. The nonguideline that a data field should definitely be private and only accessible via a getter and setter also applies here. Don't do that in C++. Don't write a trivial getter and setter just to make a public field private. Instead, simply make the field public.