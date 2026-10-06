This makes it possible to define hundreds of classes, located in as many header files, as part of a single namespace. Using this trick, the Standard C++ library puts all its identifiers in std namespace. In Qt, namespaces are used for global-like identifiers such as Qt::AlignBottom Qt::yellow. For historical reasons, Qt classes do not belong to any namespace but are prefixed with the letter 'Q'.

To refer to an identifier declared in a namespace from outside the namespace, we prefix it with the name of the namespace (and ::). Alternatively, we can use one of the following three mechanisms, which are aimed at reducing the number of keystrokes we must type.

+   * **We can define a namespace alias**

```
namespace ElPuebloDeReinaDeLosAngeles
{
    void beverHills();
    void culverCity();
    void malibu();
    void santaMonica();
}
```

namespace LA = ElPuebloDeReinaDeLosAngeles;

After the alias definition, the aliases can be used instead of the original name.

+   * **We can import a single identifier from a namespace:**

```
int main()
{
    using ElPuebloDeReinaDeLosAngeles::beverHills();
    beverHills();
    ...
}
```

The using declaration allows us to access a given identifier from a namespace without having to prefix it with the name of the namespace.

+   * **We can import an entire namespace with a single directive:**

```
int main()
{
    using namespace ElPuebloDeReinaDeLosAngeles;
```