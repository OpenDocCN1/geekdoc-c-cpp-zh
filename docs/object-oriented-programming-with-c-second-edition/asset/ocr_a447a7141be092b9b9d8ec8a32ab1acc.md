# Object-Oriented Programming with C++

```
{
map<string, int> chessbase;
typedef pair<string, int> Player; //should be of the kasparov("Kasparov",1795); //same type as map
Player fischer("Fischer",2162);
Player karpovov("Karpov",1525);

```

```
chessbase.insert(kasparov); //inserting a record
chessbase.insert(fischer); //inserting another record
chessbase.insert(karpov); //inserting another record
```

//The first member of each record is treated as the key.
//The second member is the value and can be
retrieved as follows:

```
cout<<"Number of games of Kasparov: "
<<chessbase["Kasparov"]<<endl;
cout<<"Number of occurrences of Kasparov: "
<<chessbase.count("Kasparov")<<endl;
```

//Using the subscript operator to query the value for a
//key as above inserts in the map;
Number of occurrences of Anand is:

```
cout<<"Number of occurrences of Anand: "
<<chessbase.count("Anand")<<endl; //returns zero
out<<"Number of games of Anand: "
//returns zero - but a
//record got added with
//key as "Anand" and
//value as zero because
//value is of integer
//type and order is taken
//as default value for
//integers.
```

```
cout<<"Number of occurrences of Anand is: "
<<chessbase.count("Anand")<<endl; //return 1!!
```

//An iterator can also be used. The iterator points at a
//pair rather than a single value. The pair is returned
//by the function.

```
map<string, int>::iterator iter;
iter=chessbase.find("Tulkar");
out<<"Number of occurrences of Tendulkar is: "
<<chessbase.count("Tulkar")<<endl; //return 0
if(iter!=chessbase.end() {
out<<"Number of games of ""<<iter->first<<"" is: "
<<iter->second<<endl;
}
else
out<<iter->first<<" not found\n"
out<<"Number of occurrences of Tendulkar is: "
<<chessbase.count("Tendulkar")<<endl; //return 0 ...
//no new
//record
//inserted
```

```
}
/*End of map.cpp*/
```

Output
Number of games of Kasparov is: 1795
Number of occurrences of Kasparov is: 1