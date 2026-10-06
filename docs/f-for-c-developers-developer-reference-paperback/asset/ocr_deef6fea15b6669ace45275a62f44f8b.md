```
channelFactory.Endpoint.Behaviors.Add(sharedSecretServiceBusCredential);\n
let channel = channelFactory.CreateChannel();
channel.Open();

Console.WriteLine("Enter text to echo (or [Enter] to exit):");
let mutable input = Console.ReadLine();
while (input < String.Empty) do
    try
        Console.WriteLine("Server echoed: {0}", channel.Echo(input));
    with
    as e->
        Console.WriteLine("Error: " + e.Message);
    input <- Console.ReadLine();

nannel.Close();
channelFactory.Close();

0
```

This simple communication mechanism is used to implement the cloud GA sample, which exchanges the best individuals among populations. The cloud GA sample is shown in next section.

# Genetic Algorithms in the Cloud

When talking about how to parallelize the GA in the cloud, there are two choices. One is to make the parallel work on the chromosome level, and the other is to make it work on the population level. Because the communication cost in the cloud environment cannot be ignored, implementation takes the population-level option, which means each virtual host on the cloud runs a population. The best chromosome in one population is selected and injected into another population or populations. After several iterations, all of the populations are supposed to converge at the same area and, we hope, that is the optimal solution is located.

For the real implementation, cloud queue storage is used to store the best chromosomes from different populations. The population randomly enqueues its best chromosome and deque one to replace the worst chromosome, if the queue is not empty. If the queue is empty, the population will continue its evaluation, hoping that it can get some external information next time. There is another monitoring component that is used to make sure that the queue length does not grow too fast. It deletes three items at once, to keep the queue length in control. The monitor component also hosts a service bus, which enables the client application to get the best result by querying the service bus service. Keep in mind that all the queue operations are randomly performed. It seems everything is in a chaos, but the fitness function, which is also the problem to solve, will guide the populations to the right spot. The architecture is shown in Figure 8-41.