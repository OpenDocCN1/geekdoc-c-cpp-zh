classes. Using standard accessors will keep the data private to the system and be more compliant to object-oriented development rules. The accessors will be expected to have a standardized form, namely `T Get()` for getters and `void Set( T Value )` for setters.

With that in mind, the templatized property can define typedefs (as was shown in the previous code) for the accessor function callbacks which will use to access its associated data. Pointers to the function pointers are stored in the property object itself.

Getting or setting a value via the property will call relevant function callbacks.

```
template <class T>
T CProperty <OwnerType, T>::GetValue( CBaseObject* pOwner )
{
    return pOwner->*m_Getter();
}

template <class T>
void CProperty<T>::SetValue(CBaseObject * pOwner, T Value )
{
    if ( !m_Setter )
    {
        assert( false ) // Cannot write to a read-only property
        return;
    }
    pOwner->*m_Setter( Value );
}
```

You can see here that the ->* C++ pointer-to-member operator is used. This is necessary as we are calling a function that is a member of a class object.

The property structure now has everything necessary to wrap the data type and access it through standard getters and setters. The property structure can be used and embedded in objects themselves.

# Storing Properties

Properties are associated with a particular class type. It will be natural to extend our class's RTTI information to include a list of its properties. A global properties manager will also be needed to manage the overall allocation and deletion of properties.

This gem's implementation puts the properties in a C++ Standard Template Library (STL) list, organized as illustrated in Figure 1.4.2.

The global property list system manager will manage a global list of properties that will contain all property objects. Properties are registered and added to the list sequentially, i.e., all properties that belong to the same class type will be contiguous in the list. Each class's RTTI structure also contains a list of its associated property objects.