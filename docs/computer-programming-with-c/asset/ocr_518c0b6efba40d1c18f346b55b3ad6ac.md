![](bbox=[0.125, 0.109, 0.849, 0.368])

**Figure 16.15:** Example: map storing students data

Once created, you can insert entries in map using the following syntax:

```
mapName[key] =Value;
```

Following statements create three entries in the map for three different students.

```
students[10]="John"; /* creates an entry with key=10 and
    value=John*/
students[22]="Jack"; /* creates an entry with key=22 and
    value=Jack*/
students[55]="Jill"; /* creates an entry with key=55 and value=Jill*/
```

The data stored in map students is as shown in the
Figure 16.16.

| Key | Value |
|---:|---|
| 10 | John |
| 22 | Jack |
| 55 | Jill |

**Figure 16.16:** Map named students

It is possible to iterate through map in the same way as that of other collections by creating an iterator object. The following statement creates an iterator named as temp to iterate through map storing an int type key and char* type value

```
map<int,char*>::iterator temp;
```

The for loop that iterates through each entry of the map is as shown below:

```
for (temp = students.begin();temp != students.end() ; temp++)
        {
            cout<<"Key="<<(*temp).first<<" Value = "<<(*temp).second<<endl;
        }
```

The iterator temp progresses through each entry of the map, step by step in each iteration of the for loop. The key of the entry pointed by temp is accessed as (*temp).first and the data value of the entry is accessed as (*temp).second.