```
}
```

Let us define the *setData* and *displayData* functions which sets and displays the values of *Manufacturer*, *Model* and *Displacement* respectively. These data members are actually *private* but *displayData* and *setData* functions being members of the same class can access these values and these functions being private can be accessed from anywhere:

```
 //setData accepts three parameters
 void Car :: setData (const char *manufacturer, const
 char *model, int displacement )
 {
     //Assign the value of received parameters
     //To the data members of the class
     Displacement = displacement ;
     //Using strcpy as assignment operator cannot be
     used for string assignment
     strcpy ( Manufacturer, manufacturer );
     strcpy ( Model, model );
 }

 void Car :: displayData ( )
 {
     cout << endl << endl
     << "Manufacturer: " << Manufacturer << endl
     << "Model: " << Model << endl
     << "Displacement: " << Displacement << endl ;
 }
```

This is just a definition and no operations on the data are performed so far. We need to declare an object of the Car class which will be an instantiation of the class and that object will