
to be ordered or unordered. It is also customary to say that an edge (u, v) is incident on vertices u, v. It is also common to use the term node instead of the term vertex.

As you might guess, vertices correspond to the entities in our network, and edges to the connections between them. Vertices and edges may be associated with additional attributes, e.g. the vertices may have names corresponding to the names of entities, edges may have weights, reflecting say, the strength of the connection between the entities. Undirected edges are used to represent symmetric relationships, e.g. friendship. Directed edges represent asymmetric relationships, e.g. X is a follower of Y.

Most commonly, vertices are represented by objects in C++. Often, a network contains entities of only a single type, in which case the corresponding vertices will be represented by objects of a single class. But it is possible to have different types of entities. For example you may have a network in which the entities are authors and books, with links between books and their authors. For this, you will have vertices of class author and also vertices of class book in your graph.

Edges may also be represented by objects, or they may be represented more simply.

### 21.1.1 Adjacency lists

In the simplest case, edges are represented using pointers. Thus if there is a directed edge from a vertex u to a vertex v, the object corresponding to u will contain a pointer to the object corresponding to v. If an edge (u, v) is undirected, then we will have a pointer to v in object u, as well as a pointer to u in object v. In general, each vertex will have many edges. In this case the associated pointers will be stored in a list, hence the name adjacency list. In C++, it is most natural to use vectors to build lists.

As an example, we show how a network of friends may be represented.

```
struct Person{
    string name;
    vector<Person*> friends;
};
```

The entities/vertices will be objects of class Person. We can create persons by writing:

```
Person persons[5];
```

Their names can be filled in as follows.

```
persons[0].name = "Harry";
persons[1].name = "Hermione";
persons[2].name = "Ron";
persons[3].name = "Draco";
persons[4].name = "Crabbe";
```

Now to make Harry and Hermione friends of each other, we merely have to add an undirected edge. As we have said, an undirected edge corresponds to pointers between the corresponding entities. Thus we must add a pointer to persons[1] in persons[0].friends, and vice versa. For this we will write a function.

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

### 21.1.2 Extensions

Each person need not have links only to his/her friends. Suppose we also want to have links to enemies. In that case we merely add another data member enemies of type vector<Person*> to the Person class. Suppose that some of the persons have a favourite friend. Representing this is even simpler. Since we know that there is at most one favourite, we just add a data member favourite of type Person*. Thus our definition now becomes:

```
struct Person{
    string name;
    vector<Person*> friends, enemies;
    Person* favourite;
};
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

### 21.1.3 Array indices rather than pointers

If we know that all the entities in our network will belong to a single array, e.g. the array persons as above, then an alternate representation is possible. Instead of storing a pointer to an object, we can store the index of the object in the array. Thus our definition of person would change as:

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

### 21.1.4 Edges represented explicitly

Suppose we wish to represent the network of roads between cities in a country. The cities will be the vertices in this network, and the roads themselves will be the edges. Since intercity roads are typically two way, we will use two edges for each road, one in each direction. We could make roads be pointers from one intersection to another; but we might also want to store the names of roads, and their lengths. So it is convenient to have objects to represent roads too.

A class for representing intersections could be defined as follows.

```
struct Road; // forward declaration so that we can write Road* below.
struct City{
    vector<Road*> roads;
};
```

A road object must store the intersection it leads to; optionally also the intersection it starts from, and say its name and length.

```
struct Road{
    string name;
    City* from, to;
    double length;
};
```

We will see this idea developed in Section 25.4.

## 21.2 Adjacency matrix representation

Graphs can also be represented using a so called adjacency matrix. If the graph has n vertices, an n × n matrix A is used, with entry Aij giving information about the edge from vertex i to vertex j, if any. For example, we might set Aij = 1 to indicate that an edge is present, and A_ij = 0 to indicate that there is no edge. Other values can also be used, depending upon the context, as we will see later.

The main drawback of the adjacency matrix representation is the large memory required. An adjacency matrix has n² elements, and thus memory for them will be needed no matter how many actual edges there are. If we use an adjacency list representation, then in each vertex object we will use just the memory needed to represent the edges incident on that vertex. Thus the total memory used for edge representation is proportional to the number of edges. If a graph has only a few edges, then the adjacency list representation saves on memory.

However, there are advantages too for adjacency matrices. The most obvious advantage is that we can very easily check whether an edge from vertex i to vertex j exists: we simply examine the value of A_ij. Also, as we will see shortly, in many applications, the adjacency matrix can be directly used in operations such as matrix multiplication, solving a system of equations, and so on. So in such applications, the adjacency matrix representation is very convenient.

In the exercises, you are asked to develop a sparse matrix representation: a class that behaves like a matrix but uses a smaller amount of storage. With this you can sometimes get the best of both worlds.

In the following sections we will see examples of the adjacency matrix representation.

## 21.3 Surfing on the internet

We consider the following scenario. Suppose I start surfing the net from a certain webpage. After a little while, I get bored and I click one of the links on that page; say I choose the link at random. Then I go to that page and read it for some random amount of time. Then I again click a random link on that page. I continue in this manner. The question is, after a long enough time has passed, what is the probability that I am reading a certain page on the net?

This question might seem rather contrived or even improperly posed, but it turns out to be of great importance! This is because of several reasons. First, although web browsing does not happen entirely in a random manner, it turns out that the random model described above is a good approximation for how actual web browsing happens. Second, it turns out that under reasonable conditions (say if it is possible to go from any page to any page by clicking possibly several times), the probability of being at a certain page after n clicks does tend to a fixed value, as n tends to infinity. Thus with this interpretation, the problem of finding the probability is indeed well defined. And the third and the most important reason is:

Page rank: The probability of being at a given page is an indication of the importance/"rank" of that page.

This is a rather deep observation, attributed to the founders of the search engine Google. An informal justification is: if the probability of being at a page is high, then presumably it has many incoming links, and perhaps it has many links because many people consider it to
