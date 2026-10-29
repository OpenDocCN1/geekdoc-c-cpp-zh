```
cout << "Enter the number of simulations to be created: ";
cin >> howMany;

srand(time(NULL));
for(i = 1; i <= howMany; i++)
{
    // create a new Checkout object
    anotherTrans = new Checkout;

    // use the pointer to access the member methods
    cout << "The arrival time is " << anotherTrans->getTime() << endl;
    cout << "The number of items is "<< anotherTrans->getItems() << endl;

    // delete the object
    delete anotherTrans;
}

return 0;
}
```

Following is a sample output produced by Program 12.5. The main difference between this output and that of Program 12.4 is that the arrival of customers to the checkout counter and the number of items to be checked out are determined randomly.

```
Enter the number of simulations to be created: 4

**** A new Customer has arrived ****
The arrival time is 2.23121
The number of items is 7
!!!! This Customer object has been deleted !!!!

**** A new Customer has arrived ****
The arrival time is 4.78301
The number of items is 14
!!!! This Customer object has been deleted !!!!

**** A new Customer has arrived ****
The arrival time is 2.94565
The number of items is 9
!!!! This Customer object has been deleted !!!!

**** A new Customer has arrived ****
The arrival time is 1.3329
The number of items is 3
!!!! This Customer object has been deleted !!!!
```