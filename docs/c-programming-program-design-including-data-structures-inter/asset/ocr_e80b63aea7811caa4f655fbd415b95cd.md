![](bbox=[0.255, 0.104, 0.813, 0.218])

FIGURE 10-6  Object myClock and parameter otherClock

The member variables hr, min, and sec of otherClock have the values 14, 25, and 54, respectively. In other words, when the body of the function equalTime executes, the value of otherClock.hr is 14, the value of otherClock.min is 25, and the value of otherClock.sec is 54. The function equalTime is a member of myClock. When the function equalTime executes, the member variables hr, min, and sec in the body of the function equalTime are the member variables of the object myClock. Therefore, the member hr of myClock is compared with otherClock.hr, the member min of myClock is compared with otherClock.min, and the member sec of myClock is compared with otherClock.sec.

Once again, from the definition of the function equalTime, it is clear why it has only one parameter.

Let us again take a look at the definition of the function equalTime. Notice that within the definition of this function, the object otherClock accesses the member variables hr, min, and sec. However, these member variables are private. So is there any violation? The answer is no. The function equalTime is a member of the class clockType, and hr, min, and sec are the member variables. Moreover, otherClock is an object of type clockType. Therefore, the object otherClock can access its private member variables within the definition of the function equalTime.

The same is true for any member function of a class. In general, when you write the definition of a member function, say, dummyFunction, of a class, say, dummyClass, and the function uses an object, dummyObject of the class dummyClass, then within the definition of dummyFunction, the object dummyObject can access its private member variables (in fact, any private member of the class).

Once a class is properly defined and implemented, it can be used in a program. A program or software that uses and manipulates the objects of a class is called a client of that class.

When you declare objects of the class clockType, every object has its own copy of the member variables hr, min, and sec. In object-oriented terminology, variables such as hr, min, and sec are called instance variables of the class because every object has its own instance of the data.