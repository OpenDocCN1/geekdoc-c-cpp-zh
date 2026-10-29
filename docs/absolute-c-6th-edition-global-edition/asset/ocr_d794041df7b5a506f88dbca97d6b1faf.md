There are two differences between a using declaration, such as

```
using std::cout;
```

and a using directive, such as

```
using namespace std;
```

The differences are as follows:

+   1. A using declaration makes only one name in the namespace available to your code, while a using directive makes all the names in a namespace available.

+   2. A using declaration introduces a name (like cout) into your code so no other use of the name can be made. However, a using directive only potentially introduces the names in the namespace.

Point 1 is pretty obvious. Point 2 has some subtleties. For example, suppose the namespaces NS1 and NS2 both provide definitions for myFunction, but have no other name conflicts. Then the following will produce no problems provided that (within the scope of these directives) the conflicting name myFunction is never used in your code:

```
using namespace NS1;
```

```
using namespace NS2;
```

On the other hand, the following is illegal, even if the function myFunction is never used:

```
using NS1::myFunction;
```

```
using NS2::myFunction;
```

Sometimes this subtle point can be important, but it does not impinge on most routine code. So, we will often use the term using directive loosely to mean either a using directive or a using declaration.

# Qualifying Names

This section introduces a way to qualify names that we have not discussed before. Suppose that you intend to use the name fun1 as defined in the namespace NS1, but you only intend to use it one time (or a small number of times). You can name the function (or other item) using the name of the namespace and the scope resolution operator as follows:

```
NS1::fun1();
```

This form is often used when specifying a parameter type. For example, consider

```
int getInput(std::istream inputStream)
```