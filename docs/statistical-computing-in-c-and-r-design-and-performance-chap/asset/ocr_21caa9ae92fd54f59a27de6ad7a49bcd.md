# QUEUES

This function goes through the Server objects and returns the index of the first available object. It returns –1 to indicate that all the objects are in use. When an available Server object is found, its index in the PS pointer is returned. At that point, update generates a value for serviceTime for Server object and changes its Busy member to true. Service is immediate with the consequence that there is no reason to generate a Custom object for the chosen Server object.

After all the available Server objects (should any exist) have been assigned a Customer object, it becomes necessary to push any new Customer objects onto the queue using the priority_queue push method. These customers count in the sense that they have to wait and, hence, numberCustomer variable must be increased by the number of objects that have been added to the queue. The actual Customer objects have been initialized with the current time and a value for their Gold member determined by

```
bool MMqueue::isGold() {
double u = 0;
Rng.ranUnif(1, &u);
if(u < goldProb)
return true;
return false;
}
```

This function uses the MMqueue object's ran member to simulate a Bernoulli random variable with probability goldProb.

The final step in update is to see if any Server objects have become available that can be assigned to the elements in the queue with the highest priority. The freeServer method is used to search for an available Server object, if found, its Busy value is set to true and a value for its serviceTime is generated from an exponential distribution with parameter lambdaExp. For each available Server object, a Customer object is removed from the queue in two steps. First, the priority_queue method is used to find the arrival time for the member at the top of the queue. The difference between this value and the current time is the length of the Customer object waited and this value is added to the waiting time totalTime. Next, the same highest priority element is removed from the queue with the pop method.

A program that tries out our MMqueue class is given below.

```
int main() {
MMqueue bsim(10, 4, 3, 3, .1, 123);
cout << bsim.runSimulation() << endl;
}
```

An MMqueue object is created and to start the simulation with its runSimulation method. The particular choices that have been made for the simulation parameters entail that it will run for 10 units with four Server objects. The average number of arrivals for the Poisson process is three per unit and the average service time is hours. The proportion of Customer objects with a true value for their Gold member is chosen to be .1 and the Seed for the ranGen object is set at 123.

Some enhanced output that was produced by our simulation program is given below.

```
For time = 0
number of new customers 3
queue size = 0

For time = 1
number of new customers 2
New waiting customer has Arrival time = 1 Gold = false
```