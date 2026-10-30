```
B(){z = new int;}
~B(){
    cout <<"~B.\n";
    delete z;
}
};

int main(){
    A* aptr;
    aptr = new B;
    delete aptr;
}
```

If we do not declare the destructor of A to be virtual, then after the operation delete aptr; in the main program, the memory allocated for z will not be freed. However, since we have declared the destructor of A to be virtual, the destructor of B will be called when delete aptr; is executed, instead of the destructor of A. Thus the the operation delete z; will take place. Of course, as always the destructor of A will also be called, since our rule is that the destructor of the superclass will be called after the destructor of the subclass. Do compile and execute this code, you will see from the message what is called. Remove the keyword virtual and execute again, you will see that only the destructor of A is called.

# 23.4 Program to print past tense

Suppose you wish to write a program that takes as input a verb from the English language, and prints out its past tense. Thus, given "play", the program must print "played", given "write", the program must print "wrote", and so on. A simple implementation would be to store every verb and its past tense as strings in memory. Given the verb, we can then print out the corresponding past tense.

But you will perhaps observe that for most verbs, the past tense is obtained simply by adding a suffix "ed", as is the case for the verbs "play", "walk", "look". We may consider these verbs to be regular. Verbs such as "be", "speak", "eat" which do not follow this rule could be considered irregular. Thus it makes sense to store the past tense form explicitly only for irregular verbs; for regular verbs we could simply attach "ed" when asked. This can be programmed quite nicely using inheritance.

We define a class verb that represents all verbs; it consists of subclasses regular and irregular respectively. The definition of verb contains information which is common to all verbs. The definition of regular adds in the extra information needed for regular verbs, and similarly the definition of irregular.

```
class verb{
protected:
    string root;
public:
    string getRoot(){return root;}
```