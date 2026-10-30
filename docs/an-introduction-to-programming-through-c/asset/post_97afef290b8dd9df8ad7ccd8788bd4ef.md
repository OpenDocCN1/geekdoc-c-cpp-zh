
### 25.4.1 Dijkstra's algorithm as a simulation

The first question, of course, is how to represent our network of roads. The network is a graph, in which the cities are the vertices and the roads are the edges. So we use the representation as given in Section 21.1.4. This is shown in Figure 25.4.

The entire road network is held inside the class `RoadNetwork`. It contains a vector, `cities`, the ith element of which is an object of class `City` containing information about the ith city. Thus we must assign a number to each city in our map. For our map of Figure 25.3, we assign the numbers 0 to 5 to the cities Kolhapur, Mumbai, Pune, Nashik, Nagpur, Satara respectively. The member `arrivalT` in each `City` object is meant for storing the time at which the first cyclist arrives into that city. Each `City` object also contains a vector `roads` which stores information about the roads leaving that city. Suppose `G` is a `RoadNetwork`. Then `G.cities[i].roads[j]` is an object of type `Road` which stores information about the jth road leaving city i. Specifically the object stores the following: (a) a pointer `toPtr` to the city that this road leads to, (b) a `double` `length` giving the length of this road.

The constructor for the class `RoadNetwork` reads in the road network from the file whose name is given as an argument. Figure 25.5 shows a sample input file. This file represents the road network of Figure 25.3. The first number in the file gives the number of cities. On reading this the constructor resizes the vector `cities` to this number. This will cause elements of the vector `cities` to be created. Thus a `City` object is created for each city in the network. Note the constructor for `City`: it sets `arrivalT` to `HUGE_VAL`, which represents ∞. We use this to denote that as of now, no cyclist has arrived into the city. Next, the constructor of `RoadNetwork` reads information about the roads in the graph. This consists of triples c1, c2, dist, where c1, c2 give the cities at the two ends of a road, and dist gives the length of the road. We must store the information about this road in the structure `cities[c1]` which stores information related to city c1, as well as in `cities[c2]` which stores information related to city c2. That is done in the two statements in the loop. When the loop finishes, the road network will have been constructed.

The class `City` also contains the `arrive` member function, which we will discuss later.

The main program creates the graph, and starts off the simulation of the movement of the cyclists, as shown below.

```cpp
int main(int argc, char** argv){
    RoadNetwork G(argv[1]);            // create road network from file
    int origin;                        // city from which distances are needed
    stringstream(argv[2]) >> origin;

    // cause the fictitious cyclist to arrive.
    sim::post(0, [&G,origin](){G.cities[origin].arrive();});
    sim::processAll();

    for(unsigned i=0; i<G.cities.size(); i++)
        cout << G.cities[i].arrivalT << " "; // arrivalT = distance from origin
    cout << endl;
}
```

```cpp
struct City;      // forward declaration, not definition.

struct Road{
    City* toPtr;    // Where the road leads to
    double length;
    Road(City* ptr, double d){toPtr = ptr; length = d;}
};

struct City{
    vector<Road> roads;
    double arrivalT;                // arrival time of first cyclist
    City(){arrivalT = HUGE_VAL;}    // not arrived yet.
    void arrive(){
        if(arrivalT > sim::getTime()){
            arrivalT = sim::getTime();
            for(unsigned int i=0; i<roads.size(); i++){
                sim::post(roads[i].length, [this,i](){roads[i].toPtr->arrive();});
            }
        }
    }
};

struct RoadNetwork{
    vector<City> cities;
    RoadNetwork(char* infilename) {
        ifstream infile(infilename);
        int n;
        infile >> n;
        cities.resize(n);
        double dist;
        int end1, end2;
        while(infile >> end1){
            infile >> end2 >> dist;
            cities[end1].roads.push_back(Road(&cities[end2],dist));
            cities[end2].roads.push_back(Road(&cities[end1],dist));
        }
    }
};
```

| File content | Explanation |
|---|---|
| 6 | Number of cities |
| 0 1 450 | Kolhapur Mumbai distance |
| 0 5 300 | Kolhapur Satara distance |
| 1 2 160 | Mumbai Pune distance |
| 1 3 200 | Mumbai Nashik distance |
| 2 3 220 | Pune Nashik distance |
| 3 4 500 | Nashik Nagpur distance |
| 5 2 50 | Satara Pune distance |

*Figure 25.5: Input file for graph of Figure 25.3*

The program uses command line arguments. The first command line argument `argv[1]` gives the name of the file which contains data to build the road network. We supply this file name to a constructor of the class `RoadNetwork` which builds the object `G` for us. The second command line argument, `argv[2]` is expected to be an integer, and it gives the index of the origin city. For this we first convert the string `argv[2]` to a `stringstream` (Appendix F), and then read from it. Then we start off the simulation.

There is only one kind of event in the simulation: the arrival of a cyclist into a city. The actions to be taken during the event are placed in the member function `arrive`. To check if the arriving cyclist is the first cyclist to arrive into the city, we examine member `arrivalT` in `City`. If `arrivalT` is not `HUGE_VAL`, then it has changed since the city was created, i.e. the cyclist is not the first to arrive. In this case, we do nothing. On the other hand, if `arrivalT` is still `HUGE_VAL`, then this cyclist is the first to arrive, and the following actions must be performed.

- 1. Record the correct arrival time into `arrivalT`. Note that after this it will no longer be `HUGE_VAL`.
- 2. Cyclists must be flagged off to leave the city on each outgoing road i. The cyclist will reach the corresponding city, pointed to by `roads[i].toPtr`, after covering the distance `roads[i].length`, i.e. after that much time. Hence, we post an arrival event for that city with that much latency.

So this is what the function `arrive` does.

To start off the simulation, we must flag off the cyclists in the origin city. For this we post an arrival event at time 0 for the origin city. After that, `main` merely waits for all events to be processed, i.e. for all cyclists to finish their journey. At the end the earliest time to reach each city i from the city origin can be found in `G.cities[i].arrivalT`. But that is also the distance, and so it is printed.

## 25.5 Concluding Remarks

Discrete event simulation is a powerful paradigm. Using the classes developed in this chapter, you should be able to easily build some modest size simulations. We will see such an example in the next chapter.

The basic ideas in discrete event simulation are as follows. Whatever system you wish to simulate must first be viewed as a collection of interacting entities. The interactions constitute the events. Each event can cause the state of an entity to change, or cause additional future events to be posted. We express each event as a lambda expression. When the event happens, the associated lambda expression executes, and in this execution we must change the state of the entities in the system or post additional events. Note that the code for doing all this could be placed textually inside the lambda expression, as was the case in the restaurant and coffee shop simulations. Or inside the lambda expressions we can just place a call to a function which causes the state changes or posting of additional events, as was the case in the shortest path algorithm simulation.

The coding style for posting events and acquiring resources is slightly tricky. Normally, when we wish to perform one action after another, we write the second action following the first. However, if event A causes event B which in turn causes event C, then we would write the lambda expression of C inside the lambda expression of B which in turn could be in the lambda expression of A. Thus although the events happen in succession, in the code they will appear nested. This needs some getting used to.

Note that lambda expressions make it convenient to express event posting and resource acquisition. You should make sure that you understand lambda expressions well, especially variable capture.

## Exercises

- 1. Modify the restaurant simulation to report how many customers left disappointed, how long after the closing time did the customers stay around, the number of customers in the restaurant on the average.
- 2. Generalize the coffee shop problem so that there are several servers. This is also like adding a waiting room to the restaurant. You will need to modify `resource`. Generalize the class so that at most some k clients can be using the resource simultaneously. You may find it easier to do this if you do not keep track of which clients are using the resource, but just keep track of how many clients are using the resource.
- 3. Suppose every minute a customer enters a store with a probability p. Suppose that on the average each customer spends t minutes in the store. Then on the average, how many customers will you expect to see in the store? Little’s law from queueing theory says that this number will be pt. Modify the coffee shop simulation and verify Little’s law experimentally. The law requires that no customers are turned away, and that the average is taken over a long (really infinite) time. So you should remove the capacity checks, and run the simulation for relatively long durations to check. More code will be needed to make all the measurements.
- 4. Write a simulation of a restaurant in which customers can arrive in a group, rather than individually. Suppose a group can have up to 5 members, all sizes equally likely. Suppose further that tables in the restaurant can accommodate 4 customers, so if a party of 5 arrives, then two adjacent tables must be allocated. Thus, the party must wait if two adjacent free tables are not available. Write a simulation of such a
