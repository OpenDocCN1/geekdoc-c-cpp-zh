```
// check and see if the input statement succeeded
if (cin.good() == false) {
    cout << "That was not an integer." << endl;
    return -1;
}

// print the value we got from the user
cout << x << endl;
    return 0;
}
```

cin can also be used to input an apstring:

apstring name:

```
cout << "What is your name? ";
cin >> name;
cout << name << endl;
```

Unfortunately, this statement only takes the first word of input, and leaves the rest for the next input. So, if you run this program and type your full name, it will only output your first name.

Because of these problems (inability to handle errors and funny behavior), avoid using the >> operator altogether, unless I am reading data from a source that is known to be error-free.

Instead, I use a function in the apstring called getline.

apstring name:

```
cout << "What is your name? ";
getline(cin, name);
cout << name << endl;
```

The first argument to getline is cin, which is where the input is coming from. The second argument is the name of the apstring where you want the result to be stored.

getline reads the entire line until the user hits Return or Enter. This is useful for inputting strings that contain spaces.

In fact, getline is generally useful for getting input of any kind. For example, if you wanted to type an integer, you could input a string and then check if it is a valid integer. If so, you can convert it to an integer value. If not, you can print an error message and ask the user to try again.

To convert a string to an integer you can use the atoi function defined in the header file stdlib.h. We will get to that in Section 15.4.