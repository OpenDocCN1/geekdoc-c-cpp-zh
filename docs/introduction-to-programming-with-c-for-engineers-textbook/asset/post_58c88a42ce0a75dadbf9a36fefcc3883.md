
The problem arises on line [37] when we try to copy an integer point `ip2` to the real `rp1`. This should be possible — the integer coordinates can be stored with the real representation. Nevertheless, although the compiler knows how to copy coordinates of the same type — we have not explicitly provided an implementation of the assignment operator, but the assignment on line [34] still works — it fails to copy the objects on line [37] when it encounters the `IntPoint` and `RealPoint` objects of different classes. The same type of issue is encountered on line [40], although this time there is a problem with the copy constructor. To remedy these issues, we need to provide definitions for the copy constructor and the assignment operator for `TPointFor`, but with different instantiation types. Since these can be `TPointFor` objects, instantiated with any other type, we can use the copy constructor and the assignment operator, implemented with *template member functions* as shown in Listing 4.21.

On lines [50-51], the copy constructor template member is defined. That is, an object to be copied from can be another `TPointFor`, but instantiated with any type identified with the `U` template parameter. `T` and `U` may be the same: in such a case, we would operate inside one class definition, so we could also freely access all private data members. But since in general `U` and `T` can be different, then to access the `fx` and `fy` coordinates, we have to use `Get_x` and `Get_y` from the public interface of object `pt`. Initializing `fx` with `pt.Get_x()`, and `fy` with `pt.Get_y()`, on line [51], entails a type conversion from `U` to `T`. This conversion must be known to the compiler; otherwise there is no problem with converting `int` to `double`, so the entire process goes smoothly and quietly.

**Listing 4.21** Additional template member copy constructor, and the assignment operator for the `TPointFor` class. Because these special member functions were explicitly added to the class, we are also forced to add the definition of the default constructor since its automatic generation is suppressed (in `CppBookCode`, `PointFor.h`).

```cpp
public:

    // A template member copy constructor to initialize
    // from a point with different coordinate types.
    // To be general must call Get_x and Get_y
    // Direct access must be possible only if T == U
    template < typename U >
    TPointFor( const TPointFor< U > & pt ) : fx( pt.Get_x() ), fy( pt.Get_y() ) {}

    // A template member assignment operator to initialize
    // from a point with different coordinate types.
    template < typename U >
    TPointFor< T > & operator = ( const TPointFor< U > & pt )
    {
        //fx = pt.fx;    these two work only
        //fy = pt.fy;    if T == U
        fx = pt.Get_x();    // allow conversion
        fy = pt.Get_y();
        return * this;
    }

    // A default constructor needs to be explicitly coded
    // since the copy constructor and the assignment were added
    // (otherwise could be skipped).
    TPointFor( void ) = default;
```

## Table 4.4 Fundamental relations between classes expressed with UML class diagrams

| Class relation | Description | UML diagram | Examples |
|---|---|---|---|
| The class | The UML class diagram is composed of three compartments: class name, class attributes (data), and class operations (functions). Attributes and operations can have a public (`+`), protected (`#`), or private (`-`) access type. In the case of a template class, the template arguments are shown in a box in the upper-right corner. | `ClassName`<br>`Template arguments`<br>`+ Public attribute`<br>`# Protected attribute : data type = val`<br>`- Private attribute : data type`<br>`+ Public operation( arg list ) : result`<br>`# Protected operation( arg list ) : result`<br>`- Private operation( arg list ) : result` | <pre><code>// Interface to on-board flash memory programming<br>class Am29_FlashProgrammer<br>{<br>public:<br>    enum EFlashBitMask {<br>        k_DQ7_Mask = 0x01,<br>        k_DQ6_Mask = 0x02<br>    };<br>    using SystemAddress = uint32_t; // 32-bit address bus<br>    using DataLen = uint32_t; // data length<br>    using DataWordType = uint16_t; // 16-bit data bus<br>private:<br>    const SystemAddress flashBaseAddress;<br>protected:<br>    // Checks whether a given bit toggles<br>    bool ToggleBit_PaseControl(EFlashBitMask mask, SystemAddress offsetAddress = 0);<br>public:<br>    // Class constructor<br>    Am29_FlashProgrammer(SystemAddress flashBaseAddress);<br>    // This function ERASES the ENTIRE device<br>    bool ChipErase(void);<br>    // This function programs a block of the memory<br>    bool ProgramBlock(SystemAddress addressInFlash, DataWordType * bufAddr, DataLen datalen);<br>};</code></pre> |
| Association (knows) | `Class_A` "knows" about `Class_B`, so `Class_A` can call members of `Class_B`. This relation is indicated by an arrow from `Class_A` to `Class_B`. "Knows" relations can be either one- or bi-directional (bi-directional arrows). Optionally, the ends of the connections can contain quantities. Objects of these classes do not depend on each other, but changing the interface of one can affect the other. | ![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_310_0.png) | The classes have a loose, one-directional relation. `PlotServer` is a class that facilitates printing services (`Class_B`). `PartialEquationSolver` (`Class_A`) knows and calls for services from `PlotServer` to print out some of its results. But the two classes are not bound. An object of `Class_B` needs to be alive when called by an object of `Class_A`, which is fulfilled here since `gPlotServer` is a static object. |
| Aggregation association (has-a) | An object of `Class_A` aggregates an object of `Class_B`. Aggregation association is also known as a "whole-part" or "has-a" relationship. This is a looser version of the whole-part relation in which there is no lifetime dependency between an object of `Class_A` (whole) and object(s) of `Class_B` (part). For example, the `FacultyRegistry` class aggregates objects of the `Student` class. However, both can exist without the other. `Class_B` can belong to one or more objects—thus its multiplicity can be `1..*` (denoted as `1..*`). But a whole, `Class_A`, can aggregate 0 or more parts (denoted as `0..*`). | UML association diagram showing `Class_A` aggregating `Class_B`, labeled "has a" relation (aggregation), with multiplicities `0..*` near `Class_A` and `1..*` near `Class_B`.<br>![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_311_0.png) | <pre><code>class Student             // class_B (part)<br>{<br>private:<br>    string fName, fSurname;<br>    // ...<br>public:<br>    // Student code here ...<br>};<br><br>class SchoolClassRegistry  // class_A (whole)<br>{<br>private:<br>    // registry aggregates students<br>    vector&lt;Student *&gt; studentGroup;<br>public:<br>    // FacultyRegistry code here<br>    // A Student can be added to a class<br>    void AddStudent(const Student &amp;);<br>    // but also removed from a class<br>    void RemoveStudent(const Student &amp;);<br>};</code></pre><br>One `SchoolClassRegistry` class (`Class_A`) can aggregate zero or more `Student` (`Class_B`) objects. But the aggregated `Student` objects can be detached from the `SchoolClassRegistry` object. That is, if the `SchoolClassRegistry` object is destroyed, the `Student` objects are left untouched since they can be aggregated in other "organizations" as well. |
