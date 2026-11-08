```
```cpp
// debugging options when you run it from Visual Studio.
set_terminate(&TerminateHandler);

try
{
    ContainStuffClass csc;
    wcout << csc.GetString() << endl;

    ThrowClass tC(false);
    wcout << L"tC should throw? " << tC.GetShouldThrow() << endl;

    tC = ThrowClass(true);
    wcout << L"tC should throw? " << tC.GetShouldThrow() << endl;
}
// One downside to using templates for exceptions is that you need a
// catch handler for each specialization, unless you have a base
// class they all inherit from, that is. To avoid catching
// other std::invalid_argument exceptions, we created an abstract
// class called InvalidArgumentExceptionBase, which serves solely to
// act as the base class for all specializations of
// InvalidArgumentException<T>. Now we can catch them all, if desired,
// without needing a catch handler for each. If you wanted to, however,
// you could still have a handler for a particular specialization.
catch (InvalidArgumentExceptionBase& e)
{
    wcout << L"Caught '" << typeid(e).name() << L"'." << endl <<
        L"Message: " << e.what() << endl;
}
// Catch anything derived from std::exception that doesn't already
// have a specialized handler. Since you don't know what this is, you
// should catch it, log it, and re-throw it.
catch (std::exception& e)
{
    wcout << L"Caught '" << typeid(e).name() << L"'." << endl <<
        L"Message: " << e.what() << endl;
    // Just a plain throw statement like this is a re-throw.
    throw;
}
// This next catch catches everything, regardless of type. Like
// catching System.Exception, you should only catch this to
// re-throw it.
catch (...)
{
    wcout << L"Caught unknown exception type." << endl;
    throw;
}

// This will cause our custom terminate handler to run.
wcout << L"tC should throw? " <<
    ThrowClass(true).GetShouldThrow() << endl;

return 0;
}
```
```