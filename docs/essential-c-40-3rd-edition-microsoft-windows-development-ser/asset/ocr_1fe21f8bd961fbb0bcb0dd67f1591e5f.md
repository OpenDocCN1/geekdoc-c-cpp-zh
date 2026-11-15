The important factor is that programmers with classes that implement ISettingsProvider can choose to upgrade the implementation to include IDistributedSettingsProvider, or they can ignore it.

If instead of creating a new interface, the machine-related methods are added to ISettingsProvider, then classes implementing this interface will no longer successfully compile with the new interface definition, and instead a version-breaking change will occur.

Changing interfaces during the development phase is obviously acceptable, although perhaps laborious if implemented extensively. However, once an interface is released, it should not be changed. Instead, a second interface should be created, possibly deriving from the original interface.

(Listing 7.12 includes XML comments describing the interface members, as discussed further in Chapter 9.)

# Interfaces Compared with Classes

Interfaces introduce another category of data types. (They are one of the few categories of types that don’t extend System.Object.) Unlike classes, however, interfaces can never be instantiated. An interface instance is accessible only via a reference to an object that implements the interface. It is not possible to use the new operator with an interface; therefore, interfaces cannot contain any constructors or finalizers. Furthermore, static members are not allowed on interfaces.

Interfaces are closer to abstract classes, sharing such features as the lack of instantiation capability. Table 7.1 lists additional comparisons.

# TABLE 7.1: Comparing Abstract Classes and Interfaces

| Abstract Classes | Interfaces |
| :--- | :--- |
| Cannot be instantiated independently from their derived classes. Abstract class constructors are called only by their derived classes. | Cannot be instantiated. |

2. The others being pointer types and type parameter types.