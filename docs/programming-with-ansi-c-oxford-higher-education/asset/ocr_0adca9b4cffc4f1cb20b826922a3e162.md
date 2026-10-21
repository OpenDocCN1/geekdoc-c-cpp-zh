```
class Derived2 : public Base2
{
};
```

In this case, ProtectedGB will be available to Derived1 (as protected) but not to Derived2; this is because Base2 is privately derived from GrandpaBase.

# 9.7 ACCESS CONTROL

The member functions of the class and of the derived class, friends, and objects can access the different parts of the class. The access for public, private, and protected members is different for all these entities. Access control describes who can access what and in which form. Figure 9.5 shows the access control.

![](bbox=[0.15, 0.52, 0.85, 0.72])

Available or accessible entities can be determined by the access control. The three entities available for access are as follows:

+   1. Public
+   2. Private
+   3. Protected members

The three types of entities that access them are as follows:

+   1. The member functions of the class and the friends of the class
+   2. The member functions of the derived class
+   3. The objects of the class as well as the derived class

# 9.8 ACCESS DECLARATION

As mentioned earlier, if a class is derived in a private way, then it is not possible to access the data members of the base class using the derived class objects. In contrast, if the class is derived in a public way, then all the members can be accessed as public. If one wants to derive a class and wants only a few and not all the public members to be available to the objects of the derived class, then one has to provide access declaration. Using access declaration, it is possible to provide public access to some of the base class members even after deriving them as private. Consider Program 9.5 to understand the concept better.