432 DATA STRUCTURES IN C++

The parameters for the simulation are

+   - runTime: the length of time the simulation will be allowed to run.
- nServers: the number of servers for the system.
- lambdaC: the means for the Poisson customer arrival distribution and the exponential service time distribution.
- goldProb: the presence or absence of Gold "status" for a Customer object is modeled as a Bernoulli random variable with goldProb evaluating the probability of Gold evaluating as true.
- Seed: the generation of random numbers from the Poisson, exponential and Bernoulli distributions requires a random number generator of some sort. The one that will be used is the ranUn method from the randGen class in Appendix E. The value of Seed provides the seed that will initialize the generator.

The class constructor defines these parameters through an initializer list. The constructor also creates an array of Server objects and initializes the randGen object for generating uniform random deviates.
 are various methods that could be used to assess the performance of our customer system for its values. Our attention will be directed toward customer waiting prior to service. For this purpose the waiting time total is accumulated as well as the total number of customers that had to waitCustomers. These variables are initialized to 0 in the constructor. At the end of the simulation will allow us to determine the average waiting time. The use of additional performance measures is considered in Exercise 10.14.
The private members of MMQueue class are

+   - the priority_queue object Q with template parameter Customer that will hold the Customer objects that are waiting for service,
- a pointer to Server, pS, that will be used to hold and manage the system's Server objects
- the randGen object for producing uniform random numbers.

There are also several utility functions that have been designated as private. The rPoisson, rExp and iGold are for generating Poisson, exponential and Bernoulli random deviates, respectively. The update method is used to update the system at each new time unit. In it, it uses updateServers and freeServer to update the elements in the array and to check for the availability of a server to serve the next customer object in the queue. These functions will be discussed in more detail shortly.
The MMQueue uses dynamic memory allocation for its Server component, an explicit destructor is used as a copy constructor and assignment operator should be defined for those that would use internal manipulation of MMQueue object. This will not be a feature of our example and we have chosen to forgo the specification of these methods.
The method that starts the simulation is runSimulation whose definition is

```
double MMQueue::runSimulation(){
for(int t = 0; t < runTime; t++){
	cout << " time = " << t << " end" << endl;
	update(t);
	cout << " queue size " << Q.size() << endl;
	endl;
}

while(!Q.empty()){//may be some people still in the queue
	totalTime += runTime - Q.top().Arrive();
```