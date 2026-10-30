```
struct Person{
    string name;
    vector<int> friends;
};
```

Adding an edge between Harry and Hermione would have to be done as:

```
persons[0].friends.push_back(1);    persons[1].friends.push_back(0);
```

And the names of friends of persons[1] could be printed as

```
for(unsigned i=0; i<persons[1].friends.size(); i++)
    cout << persons[persons[1].friends[i]].name << endl;
```

You may recall that we have used a similar idea in Section ??.

# 21.1.4 Edges represented explicitly

Suppose we wish to represent the network of roads between cities in a country.. The cities will be the vertices in this network, and the roads themselves will be the edges. Since intercity roads are typically two way, we will use two edges for each road, one in each direction. We could make roads be pointers from one intersection to another; but we might also want to store the names of roads, and their lengths. So it is convenient to have objects to represent roads too.

A class for representing intersections could be defines as follows.

```
struct Road; // forward declaration so that we can write Road* below.
struct City{
    vector<Road*> roads;
}
```

A road object must store the intersection it leads to; optionally also the intersection it starts from, and say its name and length.

```
struct Road{
    string name;
    City* from, to;
    double length;
}
```

We will see this idea developed in Section 25.4.

# 21.2 Adjacency matrix representation

Graphs can also be represented using a so called adjacency matrix. If the graph has n vertices, an n × n matrix A is used, with entry Aij giving information about the edge from vertex i to vertex j, if any. For example, we might set Aij = 1 to indicate that an edge