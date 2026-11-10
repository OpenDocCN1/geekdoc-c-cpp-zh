```
~~~
update=[1 2 3 4 5 6 ];
for i=1:6

    Compute the net input according to the formula
    Y_i(t+1)=X_i+∑_j Y_i W_ji

    yin(update(i))=t(update(i))+y*w(1:6,update(i));
    if(yin(update(i))>0)
        y(update(i))=1;
    end
end
if y = = x
    disp('Convergence has reached);
    stop=0;
    disp(y)
end
~~~
```

**Output**
Convergence has reached
The converged output is
    y = 1 1 1 0 1 1

# ### 4.3.3 Boltzmann Machine

Boltzmann machine is like the Hopfield network functionally and operation wise. The only difference is that simulated annealing technique is used in Boltzmann machine while finding the original pattern. Simulated annealing is used to search the pattern layer's state space to find a global minimum. Therefore the machine is able to span to an improved set of values over time as data iterates through the system.

The Boltzmann learning rule was first proposed by Ackley, Hinton, and Sejnowski in 1985. Similar to Hopfield network, the Boltzmann machine has an associated state space energy based upon the connection weights in the pattern layer. The processes of learning a training set involve the minimization of this state space energy.

The simulated annealing schedule is added to the learning process. This technique is done similar to physical annealing, temperatures start at higher values and decrease over time. This high value of temperature adds a noise factor into each processing element in the pattern layer and a low value of temperature tries to settle the oscillations of the network. An optimal solution can be determined while adding more iterations at lower temperatures.

Therefore the learning process at high temperatures is a random pro-