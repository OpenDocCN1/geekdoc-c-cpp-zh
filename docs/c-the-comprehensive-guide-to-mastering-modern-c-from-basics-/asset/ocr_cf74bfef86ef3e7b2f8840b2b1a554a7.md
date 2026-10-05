that you prefer one inherited color over the other—or perhaps you want to mix both. So far, so good.

In many situations, however, this is not what you want. For example, if you inherit name as a data field and the getName() and setName() methods from both sides, you expect the object to have only one name, not two different ones.

For this purpose, there is virtual inheritance. The class that would appear multiple times is marked with an additional virtual when specifying the ancestor. This ensures that the members are not entirely within the derived class if necessary, but are stored outside—linked with a virtual connection. When multiple such base classes come together, only the virtual connection