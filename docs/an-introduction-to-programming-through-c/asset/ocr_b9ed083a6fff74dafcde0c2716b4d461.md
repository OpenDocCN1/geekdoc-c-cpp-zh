```
void makefriends(Person &p, Person &q){ // add an undirected edge in the graph
    p.friends.push_back(&q);
    q.friends.push_back(&p);
}
```

This can be called to add the required friendship edge, and others too.

```
makefriends(persons[0], persons[1]);
makefriends(persons[2], persons[1]);
makefriends(persons[0], persons[2]);
makefriends(persons[3], persons[4]);
```

Now if we want to print the friends of Hermione (stored in persons[1]), we merely write:

```
for(unsigned i=0; i<persons[1].friends.size(); i++)
    cout << persons[1].friends[i]->name << endl;
```

# 21.1.2 Extensions

Each person need not have links only to his/her friends. Suppose we also want to have links to enemies. In that case we merely add another data member enemies of type vector<Person*> to the Person class. Suppose that some of the persons have a favourite friend. Representing this is even simpler. Since we know that there is at most one favourite, we just add a data member favourite of type Person*. Thus our definition now becomes:

```
struct Person{
    string name;
    vector<Person*> friends, enemies;
    Person* favourite;
}
```

Given our preceding definitions, we can make Ron be Harry's favourite friend by writing

```
persons[0].favourite = &persons[2];
```

On the other hand, if we wanted to indicate that Harry has no favourite we write

```
persons[0].favourite = NULL;
```

As you might remember, NULL is a special value, which indicates that no real pointer is intended.

# 21.1.3 Array indices rather than pointers

If we know that all the entities in our network will belong to a single array, e.g. the array persons as above, then an alternate representation is possible. Instead of storing a pointer to an object, we can store the index of the object in the array. Thus our definition of person would change as: