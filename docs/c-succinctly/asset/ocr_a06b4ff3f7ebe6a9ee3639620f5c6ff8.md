```
~~~cpp
            vC.VirtId() << endl <<
            vC.B2::Id() << endl <<
            vC.B2::VirtId() << endl <<
            vC.B1::Id() << endl <<
            vC.B1::VirtId() << endl <<
            vC.A::Id() << endl <<
            vC.A::VirtId() << endl <<
            // This is ambiguous between B1 and B2
            //vC.Conflict() << endl <<
            // But we can solve that ambiguity.
            vC.B2::Conflict() << endl <<
            vC.B1::Conflict() << endl <<
            // There's no ambiguity here because of virtual inheritance.
            vC.GetSomeInt() << endl <<
            endl <<

            typeid(vCB2).name() << endl <<
            vCB2.Id() << endl <<
            vCB2.VirtId() << endl <<
            vCB2.Conflict() << endl <<
            endl <<

            typeid(vCB1).name() << endl <<
            vCB1.Id() << endl <<
            vCB1.VirtId() << endl <<
            vCB1.GetSomeInt() << endl <<
            vCB1.Conflict() << endl <<
            endl <<

            typeid(vCA).name() << endl <<
            vCA.Id() << endl <<
            vCA.VirtId() << endl <<
            vCA.GetSomeInt() << endl <<
            endl;
}

int _pmain(int /*argc*/, _pchar* /*argv*/[])
{
    DemonstrateNonVirtualInheritance();
    DemonstrateVirtualInheritance();
    return 0;
}
~~~
```

***Note:*** *Many of the member functions in the previous sample are declared as const by including the const keyword after the parameter list in the declaration. This notation is part of the concept of const-correctness, which we will discuss elsewhere. The only thing that the const-member-function notation means is that the member function is not changing any member data of the class; you do not need to worry about side effects when calling it in a multi-threading scenario. The compiler enforces this notation so you can be sure a function you mark as const really is const.*

The previous sample demonstrates the difference between virtual member functions and non-virtual member functions. The Id function in class A is non-virtual while the VirtId function is virtual. The result is that when creating a base class reference to NonVirtualClass and call Id, we receive the base class' version of Id, whereas when we call VirtId, we receive NonVirtualClass's version of VirtId.