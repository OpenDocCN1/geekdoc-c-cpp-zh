
2. Write a program that displays the following text:

In Objective-C, lowercase letters are significant.
main is where program execution begins.
Open and closed braces enclose program statements in a routine.
All program statements must be terminated by a semicolon.

3. What output would you expect from the following program?

```objc
#import <Foundation/Foundation.h>
int main (int argc, const char * argv[]) {
  @autoreleasepool {
    int i;
    int i = 1;
    NSLog("@...Testing...");
    NSLog("@...%i", i);
    NSLog("@...%i", i + 1);
    NSLog("@..%i", i + 2);
  }
  return 0;
}
```

4. Write a program that subtracts the value 15 from 87 and displays the result, together with an appropriate message.

5. Identify the syntactic errors in the following program. Then type in and run the corrected program to make sure you have identified all the mistakes.

```objc
#import <Foundation/Foundation.h>
int main (int argc, const char * argv[])
(
```

```objc
@autoreleasepool {
INT sum;
  /* COMPUTE RESULT //
sum = 25 + 37 - 19
  / DISPLAY RESULTS /
  NSLog('@The answer is %i' sum);
}
  return 0;
}
```

# 6. What output would you expect from the following program?

```objc
#import <Foundation/Foundation.h>

int main (int argc, const char *argv[])
{
  @autoreleasepool {
    int answer, result;

    answer = 100;
    result = answer - 10;

    NSLog ("@The result is %i\n", result + 5);
  }
  return 0;
}
```

# 3. Classes, Objects, and Methods

In this chapter, you'll learn about some key concepts in object-oriented programming and start working with classes in Objective-C. You'll need to learn a little bit of terminology, but we keep it fairly informal. We also cover only of the basic terms here because you can easily get overwhelmed. Refer to Appendix A, "Glossary," at the end of this book, for more precise definitions of these terms.

## What Is an Object, Anyway?

An object is a thing. Think about object-oriented programming as a thing and something you want to do to that. This is in contrast to a programming language such as C, known as a procedural programming language. In C, you typically think about what you want to do first and then you worry about the objects, almost the opposite of object orientation.

Consider an example from everyday life. Let's assume that you own a car, which is obviously an object, and one that you own. You don't have just any car; you have a particular car that was manufactured in a factory, maybe in Detroit, maybe in Japan, or maybe somewhere else. Your car has a vehicle identification number (VIN) that uniquely identifies that here in the United States.

In object-oriented parlance, your particular car is an instance of a car. Continuing with the terminology, car is the name of the class from which this instance was created. Each time a new car is manufactured, a new instance from the class of cars is created, and each instance of the car is referred to as an object.

Your car might be silver, have a black interior, be a convertible or hardtop, and so on. Additionally, you perform certain actions with your car. For example, you drive your car, fill it with gas, (hopefully) wash it, take it in for service, and so on. Table 3.1 depicts this.

### Table 3.1. Actions on Objects

| Object | What You Do with It |
|---|---|
| Your car | Drive it |
| | Fill it with gas |
| | Wash it |
| | Service it |

The actions listed in Table 3.1 can be done with your car, and they can be done with other cars as well. For example, your sister drives her car, washes it, fills it with gas, and so on.

## Instances and Methods

A unique occurrence of a class is an instance, and the actions that are performed on the instance are called methods. In some cases, a method can be applied to an instance of the class or to the class itself. For example, washing your car applies to an instance (in fact, all the methods listed in Table 3.1 can be considered instance methods). Finding out how many types of cars a manufacturer makes would apply to the class, so it would be a class method.

Suppose you have two cars that came off the assembly line and are seemingly identical: They both have the same interior, same paint color, and so on. They start out the same, but as each car is used by its respective owner, its unique characteristics or properties change. For example, one car might end up with a scratch on it the other might have more miles on it. Each instance or object contains not information about its initial characteristics acquired from the factory, but also its current characteristics. Those characteristics can change dynamically. As you drive your car, the gas tank becomes dirtier, and the tires get a little more worn.

Applying a method to an object can affect the state of that object. If your method is to “fill up my car with gas,” after that method is performed, your car’s gas tank will be full. The method then will have affected the state of that.
