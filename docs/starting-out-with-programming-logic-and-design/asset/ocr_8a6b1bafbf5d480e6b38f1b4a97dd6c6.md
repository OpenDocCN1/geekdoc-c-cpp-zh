# Class Listing 14-11

```
1 Class Dog Extends Animal
2 // showSpecies method
3 Public Module showSpecies()
4 Display "I'm a dog."
5 End Module
6 
7 // makeSound method
8 Public Module makeSound()
9 Display "Woof! Woof!"
10 End Module
11 End Class
```

Even though the Dog class inherits the showSpecies and makeSound methods that are in the Animal class, those methods are not adequate for the Dog class. The Dog class has its own showSpecies and makeSound methods, which display messages that are more appropriate for a Dog. We say that the Dog class override the showSpecies and makeSound methods in the Animal class. Here is an example of pseudocode that creates an instance of the Dog class and calls the methods:

```
Declare myDog
Set myDog = New Dog()
Call myDog.showSpecies()
Call myDog.makeSound()
```

If this were actual code, it would display the following:

I'm a dog.
Woof! Woof!

Class Listing 14-12 shows pseudocode for the Cat class, which is also a subclass of the Animal class.

# Class Listing 14-12

```
1 Class Cat Extends Animal
2 // showSpecies method
3 Public Module showSpecies()
4 Display "I'm a cat."
5 End Module
6 
7 // makeSound method
8 Public Module makeSound()
9 Display "Meow"
10 End Module
11 End Class
```

The Cat class also has methods named showSpecies and makeSound. Here is an example of pseudocode that creates an instance of the Cat class and calls the methods: