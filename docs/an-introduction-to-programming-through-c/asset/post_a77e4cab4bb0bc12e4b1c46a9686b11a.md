
The natural way to write this program is to use a structure in which to read the roll number and marks. We would then use a vector of structures. In order to be able to sort a vector of structures, we simply define a member function operator<, which decide which structure is to be considered smaller given two structures. Since we want to order by roll number, we must consider the structure which contains the smaller number to be the smaller structure. That is what the definition of operator< does, in the code below. Note an important point: the sort function requires that the function operator< be defined, with both the receiver and the argument being const.

```
struct student{
    int rollno;
    float marks;
    bool operator<(const student& rhs) const{ // used by the sort function
        return rollno < rhs.rollno;             // note the two const keywords
    }
};

int main(){
    vector<student> svec;

    student s;
    while(cin >> s.rollno){
        cin >> s.marks;
        svec.push_back(s);
    }

    sort(svec.begin(), svec.end());             // will use operator< internally

    for(int i=0; i<svec.size(); i++)
        cout << svec[i].rollno << " " << svec[i].marks << endl;
}
```

## 20.4.3 Marks display variation 3

Suppose now that our input is as in Section 20.4.2, however, we want two printouts: one sorted by roll number, and another by marks. Defining operator< in the student class will not suffice now, we could define it to sort by roll number, or by marks, but not by both.

So in this case we first define a comparison function. For example we might define:

```
bool compareMarksFunction(const student &a, const student &b){
    return a.marks < b.marks;
}
```

We will shortly see how this can be used to sort by marks. Note that we could have used a function object instead of a function. So for the sake of variety, we will use a function object to sort by roll numbers. So we first define a struct from which to create the function object.

```
struct compareRollnoStruct{
    bool operator() (const student& a, const student& b){
        return a.rollno < b.rollno;
    }
};
```

Now the main program can be written.

```
int main(){
    // code to define svec and read into it as before
    sort(svec.begin(), svec.end(), compareMarksFunction);    // by marks
    for(unsigned i=0; i<svec.size(); i++)
        cout << svec[i].rollno << " " << svec[i].marks << endl;
    sort(svec.begin(), svec.end(), compareRollnoStruct());    // by roll no
    for(unsigned i=0; i<svec.size(); i++)
        cout << svec[i].rollno << " " << svec[i].marks << endl;
}
```

In this code an extra argument has been passed to both calls to sort, specifying how the sorting must happen. The argument in the first call is really a function pointer, but the & operator is not written out since it can be dropped (Section 11.7.1). In the second call, the last argument is compareRollnoStruct(). This is a call to the constructor, so what is passed is an object of the class compareRollnoStruct. This is used to decide the sorting order.

As you can see, passing a function or a function object to sort is more flexible than defining operator< in the class – you can sort according to different orders by passing different functions or function objects.

## 20.5 The map template class

The simplest way to think of the map class is as a generalization of an array or a vector. In an array or a vector, the index is required to be an integer between 0 and the n − 1 if the length of the array is n. In a map, this condition is severely relaxed: you are allowed to use any value as the index, it need not even be numerical! As in an array, the value of the index determines which element of the map is being referred to.

To use the map template class you need to include the header <map>. Next, you declare the map you want.

```
map<indexType,valueType> mapname;
```

This causes a map named mapname to be created. It stores elements of type valueType, which can be accessed by supplying indices of type indexType. It is required that the operator

operator< be defined for the type indexType. Of course, if the operator is not originally defined, you can define it. However the definition should have the usual properties expected of a comparison operator, i.e. it should be transitive and asymmetric.

Let us take a simple example. Suppose we want to store the population of different countries. Then we can create a map named Population, which will store the population value (numeric). Say we store the population in billions as a unit, so our valueType is double. We would like to use the name of the country to access the element corresponding to each country, so our indexType could be string. So we can define our map as follows.

```
map<string,double> Population;
```

Next we insert the information we want into the map, i.e. we specify the population of different countries.

```
Population["India"] = 1.21; // population of India is 1.21 billion
Population["China"] = 1.35;
Population["United States"] = 0.31;
Population["Indonesia"] = 0.24;
Population["Brazil"] = 0.19;
```

The first line, for example, creates an element whose value is 1.21, and whose index is "India". You use an array access like syntax also to refer to the created elements. For example, the following

```
cout << Population["Indonesia"] << endl;
```

will print 0.24, which is the value stored in the element whose index is "Indonesia".

You have to realize that while the statements look like array accesses superficially, their implementation will of course be very different. Effectively, what gets stored when you write Population["India"] = 1.21; is the pair ("India",1.21). The name Population really refers to a collection of such pairs. Subsequently, when we write Population["India"] we are effectively saying: refer to the second element of the pair whose first element is "India". So some code will have to execute to find this element (Section 20.5.2). So a lot is happening behind the scenes when you use maps.

What if you write two assignments for the same index, e.g.

```
Population["India"] = 1.21;
Population["India"] = 1.22;
```

This will have the effect you expect: the element created the first time around will be modified so that the value stored in it will change from 1.21 to 1.22.

An important operation you might want to perform on a map is to check if the map contains an element with a given index. Suppose you have read in the name of a country into a string variable country. Say you want to print out the population of that country if it is present in the map; else you want to print out a message saying that the population of that country is not known to the program. You can write this as follows

```
cout << "Give the name of the country: ";
string country;
cin >> country;
if (Population.count(country)>0)
    cout << Population[country] << endl;
else cout << country << " not found.\n";
```

This code should immediately follow the code given above for defining the map Population and specifying the population of the various countries.

In this code the member function count takes as argument an index value, and returns 1 if an element with that index is present in the given map. Thus suppose the user typed in "India", in response to our request to give the name of a country. Then Population.count(country) would return 1 because we did enter the population of "India" into the map earlier. So in this case the final value entered, 1.22, will get printed. On the other hand, if the country typed in was "Britain", then Population.count(country) would return 0, and hence the message "Britain not found." would be printed. Another way of determining whether a map contains a certain entry is discussed in Section 20.6.1.

You may wonder what would happen if we anyway execute

```
cout << Population["Britain"] << endl;
```

without assigning a value to Population["Britain"] earlier in the code. The execution of this statement is somewhat unintuitive. In general suppose we have defined a map

```
map<X,Y> m;
```

and suppose x is a value of type X. Then if we access m[x] without first assigning it a value, then implicitly this first causes the statement m[x]=Y(); to be executed, i.e. an element is created for the index x, and the element stores the value Y() obtained by calling the default constructor of class Y. After that the value of m[x] is returned. Thus in the case of the statement cout << Population["Britain"] << endl;, the statement Population["Britain"]=double(); is first executed. The constructor for the type double unfortunately does not initialize the value. So the map will now contain an element of unknown value but having the index "Britain". Hence this unknown value would get printed.

## 20.5.1 Marks display variation 4

In this, we will have the teacher enter the names of the student instead of the roll numbers. We will consider the original problem, i.e. students walk up to the computer and want to know their marks. But this time they type in their name rather than the roll number. Clearly, we can use strings to represent student names, and a map to store marks of students.

To make the problem more interesting, we will assume that for each student we have the marks in Mathematics, Physics, and Sanskrit. Further assume that the names are given in a file with lines such as the following.

```
A. A. Fair, 85, 95, 80
Vibhavari Shirurkar, 80, 90, 90
Nicolas Bourbaki, 95, 99, 75
```
