```
cout<<"To show function overriding"<<endl;
cout<<"Please enter your information "<<endl;
e.display();
e.check();
return 0;
}
```

# Output:

To show function overriding
Please enter your information
Enter your Undergraduate Year
2023
Sorry you can not appear for Comman Admission Test 2022

# Code Debriefing

+   - This code shows that the display function of our class exists in multiple forms.
+   - This type of polymorphism is implemented using function overriding of the display method.
+   - It is overridden in the child class, as it is inherited from the base class.
+   - The functions all have the same name but different signatures. That is, they have different combinations and numbers of parameters.
+   - While calling the display function, keep in mind which signature calls which function.

# 7.5 Friend and Generic Functions

# 7.5.1 Friend Functions

The friend function is a non-member function of a class that has access as a normal function but is declared with the keyword friend.

# Features of friend functions

+   - Declared with the friend keyword only once, either with a global scope or in another class.
+   - It can have any type of access in a class: public, private, or protected.
+   - Friend functions are called upon without any object or dot operator.
+   - Objects can be passed as arguments.