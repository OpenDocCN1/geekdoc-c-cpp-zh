
![](img/fe10f87cc5d3cff29b178c4d9a6e3012_984_0.png)

**FIGURE 30.1**  Agent lifecycle

- *choice*: selects a message from a set of sources.
- *join*: waits for more than one source before proceeding.
- *multitype_join*: same as join, except that inputs may have multiple message types.
- *timer*: produces messages based on time intervals.

There is more functionality in this library than described here and unfortunately a discussion outside the scope of the current book. We focus on a number of examples to motivate how to use the library. In Chapter 32 we shall use the library in a Monte Carlo simulation for option pricing.

## 30.6.2  Initial Examples and Essential Syntax

In this section we give some examples of using message block types. We take the simple case of sending and receiving three characters that we conventionally encapsulate in a number of functions to reduce code duplication:

```
```cpp
template <typename Buffer>
void Send(Buffer& buffer)
{
    concurrency::send(buffer, 'a');
    concurrency::send(buffer, 'b');
    concurrency::send(buffer, 'c');
}

template <typename Buffer>
void Receive(Buffer& buffer)
{
    std::cout << concurrency::receive(buffer) << ',';
    std::cout << concurrency::receive(buffer) << ',';
    std::cout << concurrency::receive(buffer) << '\n';
}
```
```

```
template <typename Buffer>
void SendAndReceive(Buffer& buffer)
{
    Send(buffer);
    Receive(buffer);
}
```

We now show the use of the three most common message block types:

```
// A message buffer that is shared by the agents.
concurrency::unbounded_buffer<char> buffer1;
concurrency::overwrite_buffer<char> buffer2;
concurrency::single_assignment<char> buffer3;

SendAndReceive<concurrency::unbounded_buffer<char>>(buffer1);
// a,b,c

SendAndReceive<concurrency::overwrite_buffer<char>>(buffer2);
// c,c,c

SendAndReceive<concurrency::single_assignment<char>>(buffer3);
// a,a,a
```

The next example is to show how to create a callback using the call class. The callback is executed when an event fires:

```
// 'call' class. Perform a work function when data is received
// 'event' is a synchronisation object for flow of execution
concurrency::event receivedAll;

int receiveCount = 0; int maxReceiveCount = 3;
concurrency::call<char> callback = [&] (char c)
{
    std::cout << c << ",";
    if (++receiveCount == maxReceiveCount)
    {
        receivedAll.set(); // set event to signalled state
    }
};

Send(callback);      // Notice that callback is a message buffer
// Wait for call object to process all items
receivedAll.wait();  // a,b,c
```

The next example shows how to transform input to output (using the transformer class, the input and output can be of different types; in this case input is char and output is int):

```
// Transformer on different input and output types
std::cout << '\n';
concurrency::transformer<char,int> converter = [] (char c)
```

```
{
    return int(c); // simple test
};

SendAndReceive(converter);        // Converter is a message buffer

long relation (long n)
{
    if (n < 2) return n;

    return relation(n - 1) + relation(n - 2);
}
```

We conclude this section by introducing the choice and join classes. Both options are concerned with the processing of a set of messages. In the first case the first function to finish is selected (select among competing tasks) while in the second case all functions are selected:

```
// Choice: select the first available messages from a set of sources
concurrency::overwrite_buffer<long> rel1;
concurrency::overwrite_buffer<long> rel2;
concurrency::single_assignment<long> rel3;

auto selectOne = concurrency::make_choice(&rel1, &rel2, &rel3);

concurrency::parallel_invoke(
    [&rel1] {concurrency::send(rel1, relation(22)); },
    [&rel2] {concurrency::send(rel2, relation(14)); },
    [&rel3] {concurrency::send(rel3, relation(13)); }
);

// See who responds first
switch (concurrency::receive(selectOne))
{
case 0:
    std::cout << "rel1 " << concurrency::receive(rel1) << '\n';
    break;
case 1:
    std::cout << "rel2 " << concurrency::receive(rel2) << '\n';
    break;
case 2:
    std::cout << "rel3 " << concurrency::receive(rel3) << '\n';
    break;
default:
    std::cout << "oops\n";
    break;
}
```

```
// Run multiple tasks
concurrency::single_assignment<long> relA;
concurrency::single_assignment<long> relB;
concurrency::single_assignment<long> relC;

auto joinAll = concurrency::make_join(&relA, &relB, &relC);
```

```
concurrency::parallel_invoke(
    [&relA] {concurrency::send(relA, relation(6)); },
    [&relB] {concurrency::send(relB, relation(7)); },
    [&relC] {concurrency::send(relC, relation(10)); }
);

auto result = concurrency::receive(joinAll);

std::cout << "relA " << std::get<0>(result)
    << ", relB " << std::get<1>(result)
    << ", relC " << std::get<2>(result) << '\n';
```

The output from the complete code in this section is:

```
a,b,c
c,c,c
a,a,a
a,b,c,
97,98,99
rel3 233
relA 8, relB 13, relC 55
```

## 30.6.3 Simulating Stock Quotes Work Flow

The Agents library can be used to implement the Producer–Consumer pattern more easily than is possible by using threads in combination with synchronising queues (see Demming and Duffy, 2010). In the current case we do not have to worry about locking shared data (because there is no shared data) and agents communicate solely using message passing. Agents’ state is said to be isolated.

The following example simulates a stock quotes application. Stock values are read from an external device and each item in the array is sent to a consumer to be displayed, for example in Excel, on the console or some other output device. Both agent classes are derived from the abstract base class concurrency::agent having the pure virtual member function run(). Derived classes must implement this function, of course. We use ITarget and ISource to denote the communication endpoints for producer and consumer, respectively. The producer class is:

```
class Producer : public concurrency::agent
{
private:
    // The target buffer to write to.
    concurrency::ITarget<double>& _target;
public:
    explicit Producer(concurrency::ITarget<double>& target)
        : _target(target) {}

    void run()
    {
        // For illustration, create a predefined array of stock quotes.
        // A real-world application reads these quotes from an external
        // source,
```

```
```cpp
// such as a network connection or a database.
std::array<double, 6> quotes =
                         { 24.44, 24.65, 24.99, 23.76, 22.30, 25.89 };

// Send each quote to the target buffer.
std::for_each(begin(quotes), end(quotes), [&](double quote)
{
    send(_target, quote);

    // Pause before sending the next quote.
    concurrency::wait(20);
});
// Send a negative (sentinel) value to indicate the end of
// processing.
concurrency::send(_target, -1.0);

// Set the agent to the finished state.
done();
}
};
```
```

The consumer class is:

```
```cpp
class Consumer : public concurrency::agent
{
private:
    // The source buffer to read from.
    concurrency::ISource<double>& _source;
public:
    explicit Consumer(concurrency::ISource<double>& source)
        : _source(source){}

    void run()
    {
        // Read quotes from the source buffer until we receive
        // a negative value.
        double quote;

        // Poll to see if any new values have arrrived
        while ((quote = concurrency::receive(_source)) >= 0.0)
        {
            // Print the quote.
            std::cout.setf(std::ios::fixed);
            std::cout.precision(2);
            std::cout << "Current quote is " << quote << '\n';

            // Pause before reading the next quote.
            concurrency::wait(10);
        }
    }
}
```
```

```
// Set the agent to the finished state.
done();
}
```

```
};
```

Finally, the test program is:

```
int main()
{
    // A message buffer that is shared by the agents.
    concurrency::overwrite_buffer<double> buffer;

    // Create and start the producer and consumer agents.
    Producer producer(buffer);
    Consumer consumer(buffer);
    producer.start();
    consumer.start();

    // Wait for the agents to finish.
    concurrency::agent::wait(&producer);
    concurrency::agent::wait(&consumer);
}
```

Notice the presence of the sentinel value in the producer.

## 30.6.4 Monte Carlo Option Pricing Using Agents

This is an example that we shall discuss in Chapter 32. It is a producer–consumer application in which the producer is a path evolver based on the Euler finite difference method while the consumers are one or more option pricers.

## 30.6.5 Conclusions and Epilogue

We decided to introduce the Agents library as it fills a gap in the design landscape. In this case we are interested in event-based distributed systems. From the examples already given we can see that the design philosophy is not incompatible with the design approach taken in Chapter 9 and we shall show why in Chapter 32. The library can be used in applications that apply the traditional and rigid Observer pattern or the more flexible Boost signals2 library. The major difference is that we do not call object methods; agents send and receive data using message passing.

We conclude this section with a list of features to take into account when programming with agents and tips to improve efficiency:

- Asynchronous agents are effective because they isolate their internal state from other agents. This helps reduce contention on shared memory. State isolation reduces the chance of deadlock and race conditions because components do not have to synchronise access to shared data.
