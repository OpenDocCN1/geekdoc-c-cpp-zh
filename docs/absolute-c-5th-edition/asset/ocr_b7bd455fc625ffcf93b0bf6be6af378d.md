# Self-Test Exercises (continued)

```
message( );

return 0;
}

void message( )
{
    cout << "Global message.\n"
}

namespace Hello
{
    void message( )
{
        cout << "Hello.\n"
    }
}

namespace Goodbye
{
    void message( )
{
        cout << "Good-Bye.\n"
    }
}
```

+   9. Write the declaration (prototype) for a void function named wow. The function wow has two parameters, the first of type speed as defined in the speedway namespace and the second of type speed as defined in the indy500 namespace.

> TIP: Choosing a Name for a Namespace

It is a good idea to include your last name or some other string in the names of your namespaces so to reduce the chance that somebody else will use the same namespace name as you do. With multiple programmers writing code for the same project, it is important that namespaces that are meant to be distinct really have distinct names. Otherwise, you can easily have multiple definitions of the same names in the same scope. That is why we included the name Savitch in the namespace DtimeSavitch in Display 11.9.