+   2. The main loop:

```
~~~
for (clock = 1; clock <= simulationTime; clock++)
{
~~~
```

+   2.1. Update the server list to decrement the transaction time of each busy server by one time unit.
+   2.2. If the customer's queue is nonempty, increment the waiting time of each customer by one time unit.
+   2.3. If a customer arrives, increment the number of customers by 1 and add the new customer to the queue.
+   2.4. If a server is free and the customer's queue is nonempty, remove a customer from the front of the queue and send the customer to the free server.

```
~~~
}
~~~
```

+   3. Print the appropriate results. Your results must include the number of customers left in the queue, the number of customers still with servers, the number of customers arrived, and the number of customers who actually completed a transaction.

Once you have designed the function runSimulation, the definition of the function main is simple and straightforward because the function main calls only the function runSimulation.

When we tested our version of the simulation program, we generated the following results. (The program was executed two times.) We assumed that the average transaction time is five minutes and that, on average, a customer arrives every four minutes, and we used a random number generator to generate a number between 0 and 1 to decide whether a customer arrived at a given time unit.

# **Sample Runs:**

# **Sample Run 1:**

```
~~~
Customer number 1 arrived at time unit 4
Customer number 2 arrived at time unit 8
From server number 1 customer number 1
    departed at time unit 9
Customer number 3 arrived at time unit 9
Customer number 4 arrived at time unit 12
From server number 1 customer number 2
    departed at time unit 14
From server number 2 customer number 3
    departed at time unit 19
Customer number 5 arrived at time unit 21
From server number 1 customer number 4
    departed at time unit 24
From server number 1 customer number 5
    departed at time unit 29
~~~
```