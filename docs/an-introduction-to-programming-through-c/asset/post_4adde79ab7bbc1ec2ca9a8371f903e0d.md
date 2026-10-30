
```
B(){z = new int;}
~B(){
    cout << "~B.\n";
    delete z;
}
};
```

If we do not declare the destructor of A to be virtual, then after the operation `delete aptr;` in the main program, the memory allocated for `z` will not be freed. However, since we have declared the destructor of A to be virtual, the destructor of B will be called when `delete aptr;` is executed, instead of the destructor of A. Thus the operation `delete z;` will take place. Of course, as always the destructor of A will also be called, since our rule is that the destructor of the superclass will be called after the destructor of the subclass. Do compile and execute this code, you will see from the message what is called. Remove the keyword `virtual` and execute again, you will see that only the destructor of A is called.

## 23.4 Program to print past tense

Suppose you wish to write a program that takes as input a verb from the English language, and prints out its past tense. Thus, given "play", the program must print "played", given "write", the program must print "wrote", and so on. A simple implementation would be to store every verb and its past tense as strings in memory. Given the verb, we can then print out the corresponding past tense.

But you will perhaps observe that for most verbs, the past tense is obtained simply by adding a suffix "ed", as is the case for the verbs "play", "walk", "look". We may consider these verbs to be regular. Verbs such as "be", "speak", "eat" which do not follow this rule could be considered irregular. Thus it makes sense to store the past tense form explicitly only for irregular verbs; for regular verbs we could simply attach "ed" when asked. This can be programmed quite nicely using inheritance.

We define a class verb that represents all verbs; it consists of subclasses regular and irregular respectively. The definition of verb contains information which is common to all verbs. The definition of regular adds in the extra information needed for regular verbs, and similarly the definition of irregular.

```
class verb{
protected:
    string root;
public:
    string getRoot(){return root;}
    virtual string past_tense(){return "";}
};
```

The member root will store the verb itself. We have defined the member function past_tense to be virtual. For now it returns the empty string. But this is not important, since we expect to override it in the subclasses.

The subclasses regular and irregular are as you might expect.

```
class regular : public verb{
public:
    regular(string rt){
        root = rt;
    }
    string past_tense(){return root + "ed";}
};
```

```
class irregular : public verb{
    string pt; // past tense of the verb
public:
    irregular(string rt, string p){
        root = rt;
        pt = p;
    }
    string past_tense(){return pt;}
};
```

Thus, to create an instance v1 that represents the verb "play" we would just write

```
regular v1("play");
```

After this if we wrote v1.past_tense(), we would get the string "played" as the result. Similarly

```
irregular v2("be","was");
```

would create an instance v2 to represent the verb "be". And of course v2.past_tense() would return "was".

We now see how the above definitions can be used to write a main program that returns the past tense of verbs. Clearly, we will need to somehow store the information about verbs. For this, we use a vector. We cannot have a single vector storing both regular and irregular verbs. However, we can define a vector of pointers to verb in which we can store pointers to irregular as well as regular objects. Thus the program is as follows.

```
int main(){
    vector<verb*> V;
    V.push_back(new regular("watch"));
    V.push_back(new regular("play"));
    V.push_back(new irregular("go","went"));
    V.push_back(new irregular("be","was"));

    string query;
    while(cin >> query){
        size_t i;
        for(i=0; i<V.size(); i++)
            if ((V[i])->getRoot() == query){
                cout << V[i]->past_tense() << endl;
                break;
            }
        if(i == V.size()) cout << "Not found.\n";
    }
}
```

We begin by creating the vector V. We then create instances of regular and irregular verbs on the heap, and store pointers to them in consecutive elements of V. Finally, we enter a loop in which we read in a query from the user, check if it is present in our vector V. If so, we print its past tense. Note that if the for loop ends with i taking the value V.size(), it must be the case that no entry in V had its root equal to the query. In this case we print "Not found." As you know, the while loop will terminate when cin ends, e.g. if the user types control-d.

A number of points are to be noted regarding the use of inheritance in this example.

- Our need was to represent the category of verbs which consisted of mutually disjoint sub-categories of irregular and regular verbs. This is a very standard situation in which inheritance can be used.
- The vector V is polymorphic: it can contain pointers to objects of type irregular as well as of type regular. We can invoke the operation past_tense on objects pointed to by elements of V, without worrying about whether the objects are of type regular or irregular. Because past_tense is virtual, the correct code gets executed.

## 23.5 Abstract Classes

You will note that we return the empty string in the past_tense function in verb. Returning an empty string does not make sense, but we did this because we expected that the verb class would never be used directly; only its subclasses would be used in which the function would get overridden. This idea works, but it is not aesthetically pleasing that we should need to supply an implementation of past_tense in verb expecting fully well that it will not get used.

One possibility is to only declare the member function past_tense in verb, and not supply any implementation at all. Unfortunately, whenever an implementation is not supplied, the compiler expects to find it somewhere, in some other file perhaps. If such an implementation is not given, the compiler or the linker will produce an error message.

What we need is a way to tell the compiler that we do not at all intend to supply an implementation of past_tense for the verb class. This is done by suffixing the phrase "= 0" following the declaration. Thus we would write

```
class verb{
...
public:
    virtual string past_tense() = 0;
...
};
```

Writing "= 0" following the declaration of a member function tells the compiler that we do not intend to at all supply an implementation for the function. You may think of 0 as representing the NULL pointer, and hence effectively indicating that there is no implementation.

There is an important consequence to assigning a function to 0. Suppose a class A contains a member function f assigned to 0. Then we cannot create an instance of A! This is because for that instance we would not know how to apply the function f. In C++, classes which cannot be instantiated are said to be abstract. Indeed, the only way of making a class abstract is to assign one of its member functions to 0.

So in our case, if we assign past_tense to 0 in verb, then the class verb would become abstract. We would not be able to create instances of it. But this is fine, we indeed would not like users to instantiate verb, instead we expect them to instantiate either regular or irregular.

## 23.6 Multiple inheritance

Sometimes, an object can be thought of as a specialization of not one, but two other objects. For example, we might have an Automobile class and a SolarPoweredDevice class.

```
class Automobile{
    double mileage;
};
class SolarPoweredDevice{
    double cellEfficiency;
};
```

Suppose we also need to represent solar powered automobiles, they would need to have features of both the Automobile class as well as SolarPoweredDevice class. We can get this by constructing a class SolarPoweredAutomobile which inherits from both!

```
class SolarPoweredAutomobile : public Automobile,
                               public SolarPoweredDevice {};
```

> 1 If we make the constructor of a class private and there are no member functions that use the constructor, then effectively we have ensured that the class cannot be instantiated. But technically such classes are not considered to be abstract.
