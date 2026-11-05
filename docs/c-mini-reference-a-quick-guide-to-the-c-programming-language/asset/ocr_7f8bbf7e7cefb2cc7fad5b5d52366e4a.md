# 4.3.3. The using alias directive

A using alias directive introduces an identifier, or an alias, for a namespace or type within the innermost containing namespace (or, within the compilation unit). The identifiers introduced by the using alias directive can be used to reference the given namespace or type.

```
using IDENTIFIER = NAMESPACE_OR_TYPE_NAME ;
```

For instance,

```
namespace Europe.Ukraine {
    public class Citizen ()
}
namespace World {
    using Person = Europe.Ukraine.Citizen;
    class Farmer: Person ()
}
```