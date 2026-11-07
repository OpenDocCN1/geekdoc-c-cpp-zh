If a class has pointer member variables:

+   - During object declaration, the initialization of one object using the value of another object will lead to a shallow copying of the data if the default member-wise copying of data is allowed.
+   - If, as a parameter, an object is passed by value and the default member-wise copying of data is allowed, it will lead to a shallow copying of the data.

In both cases, to force each object to have its own copy of the data, we must override the definition of the copy constructor provided by the compiler; that is, we must provide our own definition of the copy constructor. This is usually done by putting a statement that includes the copy constructor in the definition of the class and then writing the definition of the copy constructor. Then, whenever the copy constructor needs to be executed, the system would execute the definition provided by us, not the one provided by the compiler. Therefore, for the class `ptrMemberVarType`, we can overcome this shallow copying problem by including the copy constructor in the class `ptrMemberVarType`. Example 12-8 illustrates this.

The copy constructor automatically executes in the following three situations (the first two were described previously):

+   - When an object is declared and initialized by using the value of another object
+   - When, as a parameter, an object is passed by value
+   - When the return value of a function is an object

Therefore, once the copy constructor is properly defined for the class `ptrMemberVarType`, both `objectOne.p` and `objectThree.p` will have their own copies of the data. Similarly, `objectOne.p` and `paramObject.p` will have their own copies of the data, as shown in Figure 12-21.

![](bbox=[0.1816, 0.6899, 0.9079, 0.8861])

FIGURE 12-21  Pointer member variables of objects `objectOne` and `paramObject` with their own data