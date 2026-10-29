```
void showObject();
void getItems(){return;} // inline do-nothing methods
void getTime(){return;} // will be used in Program 12.5
};

// class implementation section
Checkout::Checkout() // constructor
{
    cout << "\n**** A new Customer object has been created ****\n";
    numItems = 5;
    arrivalTime = 2.5;
}

void Checkout::showObject()
{
    cout << "  For this object:\n";
    cout << "      numItems = " << numItems
         << "      arrivalTime = " << arrivalTime << endl;
    return;
}

int main()
{
    Checkout *anotherTrans; // pointer to a Checkout object
    int i, howMany;

    cout << "Enter the number of transactions to be created: ";
    cin >> howMany;

    for(i = 1; i <= howMany; i++)
    {
        anotherTrans = new Checkout; // create a new Checkout object

        // display the address of the created object
        cout << "The memory address of this object is: " << anotherTrans << endl;
        anotherTrans->showObject(); // display contents of this object
        delete anotherTrans;  // delete the object
    }

    return 0;
}
```