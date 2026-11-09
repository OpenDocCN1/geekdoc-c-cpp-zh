# Events and Visual Basic

I fired the event in the previous example using the vtable. Visual Basic generates automation code only for its event sinks and does not generate any vtable code to capture event notifications. That means I must call the `IDispatch::Invoke` method in order to fire the event in a Visual Basic client.

# Black Hole of Events

This is one of the big black holes in Microsoft's object-oriented architecture.
How is the programmer supposed to know which interface to fire the event with, the dispatch or the vtable interface? It is simply not possible without imposing limits on the model.
You could impose a rule on COM servers that they must call both the vtable and dispatch interface, but this would result in additional client code to ensure that an event was not received twice.
The only rule that works is to limit everyone to using the dispatch interface when invoking event sink methods. This removes any advantage of using the vtable and increases the learning curve by requiring developers to understand automation in order to use events.

Listing 6.14 shows the necessary code to call the `IDispatch::Invoke` method in order to invoke events using the dispatch interface.

# **LISTING 6.14**   Call Event Handler Through IDispatch Interface

```
VARIANTARG* pvars = new VARIANTARG[1];
for (int i = 0; i < 1; i++)
{
    VariantInit(&pvars[i]);
}
IUnknown** pp = m_vec.begin();
while (pp < m_vec.end())
{
    if (*pp != NULL)
    {
        pvars[0].vt = VT_I4;
        pvars[0].lVal = lFlags;
        DISPPARAMS disp = { pvars, NULL, 1, 0 };
        IDispatch* pDispatch = reinterpret_cast<IDispatch*>(*pp);
        pDispatch->Invoke(0x1, IID_NULL, LOCALE_USER_DEFAULT,
                          DISPATCH_METHOD, &disp, NULL, NULL, NULL);
    }
}
```