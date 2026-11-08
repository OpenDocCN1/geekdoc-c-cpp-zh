```
```cpp
House(char *myName)
{
    cout<<"House::constructor_c\n";
    name_p = new char(sizeof(strlen(myName)));
    name_p = myName;
    Room::initialList(roomsList);
    Room* myRoom;
    Room::createRoom(myRoom, this, "Kitchen");
    roomsList[0] = myRoom;
    Room::createRoom(myRoom, this, "BedRoom");
    roomsList[1] = myRoom;
    Room::createRoom(myRoom, this, "Drawing Room");
    roomsList[2] = myRoom;
}
~House()
{
    cout<<"House::destructor_d\n";
    unsigned int i;
    cout<<"Delete all the Rooms ...\n";
    for(i=0; i<3; ++i)
    {
        if(roomsList[i] != NULL)
        {
            delete (roomsList[i]);
        }
    }
    delete [] roomsList;
    delete (name_p);
}
void disp()
{
    cout<<"\n\nName of the House :"<<name_p;
    if(roomsList != NULL)
    {
        unsigned int i;
        cout<<"\n\nRooms details...\n";
        for(i=0; i<3; ++i)
        {
            if(NULL != roomsList[i])
            {
                roomsList[i]->disp();
            }
        }
        cout<<"\n\n";
    }
}
private:
    char* name_p;
    Room* roomsList[3];
};
int main()
{
    cout<<"\nExample of Composition Relationship\n";
    cout<<"----------------------------------------\n\n";
    House hse("Shanti Aashram");
    cout<<"\n\nHouse details...\n";
}
```
```