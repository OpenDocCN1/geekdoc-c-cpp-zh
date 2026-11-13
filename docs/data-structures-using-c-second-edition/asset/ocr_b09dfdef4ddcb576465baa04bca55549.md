```
        }
    }
if (flag == 0)
{
    for (i = 0; i < key;i++)
    {
        if (ht[i] == val)
        {
            flag = 1;
            key = i;
            break;
        }
    }
}
if (flag == 1)
{
    found=1;
    printf("\nThe item searched was found at position %d ", key + 1 );
}
else
{
    key = -1;
    printf( "\nThe item searched was not found in the hash table" );
}
}
void delete_val()
{
    search_val();
    if (found==1)
    {
        if ( key != -1 )
        {
            printf( "\nThe element deleted is %d ", ht[ key ] );
            ht[ key ] = -1;
        }
    }
}
Output
MENU
1. Insert
2. Search
3. Delete
4. Display
5. Exit
Enter your option: 1
Enter the element to be inserted :1
Enter your option: 4
1 -1 -1 -1 -1 -1 -1 -1 -1
Enter your option: 5
```

# 15.5.2 Collision Resolution by Chaining

In chaining, each location in a hash table stores a pointer to a linked list that contains all the key values that were hashed to that location. That is, location 1 in the hash table points to the head of the linked list of all the key values that hashed to 1. However, if no key value hashes to 1, then location 1 in the hash table contains null. Figure 15.5 shows how the key values are mapped to a location in the hash table and stored in a linked list that corresponds to that location.