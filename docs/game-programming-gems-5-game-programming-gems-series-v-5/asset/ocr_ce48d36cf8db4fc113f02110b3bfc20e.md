```
template <class T, class BaseClass, ClassID CLID>
T* CSupportsRTTI<T, BaseClass, CLID>::Create()
{
    return new T();
}

template <class T, class BaseClass, ClassID CLID>
void CSupportsRTTI<T, BaseClass, CLID>::RegisterReflection()
{
}
```

The RTTI info structure is put in as a static member in the template. Each template instance (we have one unique template instance per class type in our application) will spawn its own instance of the static member, which is exactly what we want. GetRTTI() is the virtual function that will return the correct RTTI information depending on the type of polymorphic objects.

GetClassRTTI() is a function that can be used to query the RTTI information of a specific class, as in CCassType::GetClassRTTI(). Note that static member functions hide static member functions in ancestor classes, which again is exactly what we need here. CCassType::GetClassRTTI() will hide CBaseClassType::GetClassRTTI().

The Create() function is our class factory function. Its simple implementation allocates a new instance of the instantiated template type. T::Create() will resolve to CSupportsRTTI<T, BaseClass, CLID>::Create(), which is T's base class.

The lines that declare the static RTTI structure merit our attention. Here, the RTTI structure is statically constructed, and all relevant RTTI constructor parameters are passed in to the RTTI unique structure:

+   - CLID is the 32-bit unique class identifier. This is a template parameter.
+   - TypeId(T).name() is the class's name string. It may appear that we are cheating here: we are not using the C++ runtime type info system to build our own system on top of it, which pretty much defeats the purpose of writing our own! Not really: TypeId(T) here will be resolved by the compiler at compile time, so we are not really using the C++ dynamic RTTI structure. In fact, you will find that the code works even with the C++ runtime type info system turned off. In effect, this snippet of code will simply cause the compiler to create and fill the type_info structure for T and return the associated string, which does not require any runtime polymorphic checks.
+   - BaseClass::GetClassRTTI() is the base class's RTTI structure. BaseClass is a template parameter.
+   - CSupportsRTTI<T, BaseClass, CLID>::Create() provides the pointer to our factory class function, which was automatically instantiated by the template. It's useful to create instances of classes when only knowing the class ID or class name as a string.

When the static variable is initialized at application startup, all RTTI structures can be added to a global RTTI manager. Care must be taken to avoid dependencies