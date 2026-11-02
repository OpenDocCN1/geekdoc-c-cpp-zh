

离开事件不仅要记住离开时间，还要记住顾客要从哪位柜员那里离开。要处理一个离开事件，我们就把该顾客从对应的柜员处移除。

```cpp
class Departure : public Event
{
public:
    Departure(double time, int teller);
    virtual void process(Simulation& sim) const;
private:
    int teller;
};
```

```cpp
Departure::Departure(double time, int teller) : Event(time)
{
    this->teller = teller;
}
```

```cpp
void Departure::process(Simulation& sim) const
{
    BankSimulation& bank = dynamic_cast<BankSimulation&>(sim);
    bank.remove(teller);
}
```

## 运行模拟

要运行模拟，我们首先要构造一个包含五名柜员的 `BankSimulation` 对象。设置模拟时最重要的任务是让事件流运转起来。初始时，事件队列为空。我们要在开始时间（上午 9 点）安排一名顾客到达。由于到达事件的处理过程会安排下一个到达事件，因此为第一位顾客插入到达事件，就能顺带生成后续所有到达事件。顾客到达银行后，会被分配到柜员处，并产生离开事件。

下面是 `main` 函数：

```cpp
int main()
{
    const double START_TIME = 9 * 60; // 9 a.m.
    const double END_TIME = 17 * 60; // 5 p.m.

    const int NTELLERS = 5;

    BankSimulation sim(NTELLERS);
    sim.add_event(new Arrival(START_TIME));
    sim.run(START_TIME, END_TIME);
}
```

下面是一次典型的程序运行结果。开始时所有柜员均为空，顾客陆续到达：

```text
....<
C....<
CC...<
CCC..<
CCCC.<
C.CC<
CCCC.<
CCCCCC<
CCCCC<C
CCCCCC<
C.CCC<
```

由于顾客到达时间和业务处理时间的随机波动，队伍有时会排得很长：

```text
cccccc<cccccccc
ccccc<cccccccccc
ccccc<cccccccccccc
ccccc<ccccccccccc

cccccc<cccccccccc
ccccc<ccccccccccc
ccccc<cccccccccccccc
ccccc<cccccccccccccc
ccccc<cccccccccccc
```

另外一些时候，银行又会重新空下来：

```text
ccc..c<
ccc...<
cc...c<
c....<
c....<
c....<
```

这次特定的模拟运行最终得到如下统计结果：

457 位顾客。平均时间 15.28 分钟。

如果你就是银行经理，这个结果会令人相当沮丧。你雇的柜员数量本应足以照顾到所有顾客。（平均每小时需要服务 60 位顾客。每位顾客的交易平均耗时 5 分钟，也就是总共 300 柜员分钟，即 5 个柜员工时。因此，雇用五名柜员本该刚刚好。）然而，顾客平均要在队伍中等待超过 10 分钟，是他们办理业务时间的两倍。这只是一个平均值，所以有些顾客等待的时间还要更长。如果不满的顾客会损害你的业务，你可能就必须雇用更多柜员，并为他们在部分时间里的空闲付钱。

以下是完整的银行模拟程序：

## worked_example_1/banksim.cpp

```cpp
#include <cmath>
#include <cstdlib>
#include <iostream>
#include <queue>
#include <string>

using namespace std;

class Simulation;

class Event
{
public:
    Event(double event_time);
    virtual void process(Simulation& sim) const;
    double get_time() const;
    virtual ~Event() {}
private:
    double time;
};
// Redefine < for Event* pointers
namespace std
{
template<>
class less<Event*>
{
public:
    bool operator()(Event* a, Event* b)
    {
        return a->get_time() > b->get_time();
    }
};
}

class Simulation
{
public:
    /**
     Constructs a discrete event simulation.
     */
    Simulation();

    double get_current_time() const;

    /**
     Compute exponentially distributed random numbers.
     @param mean the mean of the number sequence
     @return a random number
     */
    double expdist(double mean) const;

    /**
     Adds an event to the event queue.
     @param evt the event to add
     */
    void add_event(Event* evt);

    /**
     Displays intermediate results after each event.
     */
    virtual void print() const;

    /**
     Displays summary results after the end of the simulation.
     */
    virtual void print_summary() const;

    /**
     Runs this simulation for a given time interval.
     @param start_time the start time
     @param end_time the end time
     */
    void run(double start_time, double end_time);
    virtual ~Simulation() {}
private:
    priority_queue<Event*> event_queue;
    double current_time;
};

class Arrival : public Event
{
public:
    /**
     @param time the arrival time
     */
    Arrival(double time);
    virtual void process(Simulation& sim) const;
};

class Departure : public Event
{
public:
    /**
     @param time the departure time
     @param teller the teller holding the customer
     */
    Departure(double time, int teller);
    virtual void process(Simulation& sim) const;
private:
    int teller;
};

class Customer
{
public:
    /**
     Constructs a customer.
     @param the time at which the customer entered the bank
     */
    Customer(double time);
    /**
     Gets the time at which the customer entered the bank.
     @return the arrival time
     */
    double get_arrival_time() const;
private:
    double arrival_time;
};


class BankSimulation : public Simulation
{
public:
    /**
     Constructs a bank simulation.
     @param number_of_tellers the number of tellers
     */
    BankSimulation(int number_of_tellers);
    /**
     Adds a customer to the simulation.
     @param c the customer
     */
    void add(Customer* c);
    /**
     Removes a customer from a teller.
     @param i teller position
     */
    void remove(int i);
    virtual void print() const;
    virtual void print_summary() const;
private:
    /**
     Adds a customer to a teller and schedules the departure event.
     @param i the teller number
     @param c the customer
     */
    void add_to_teller(int i, Customer* c);
    vector<Customer*> tellers;
    queue<Customer*> customer_queue;
    int total_customers;
    double total_time;

    const double INTERARRIVAL = 1;
    // average of 1 minute between customer arrivals
    const double PROCESSING = 5;
    // average of 5 minutes processing time per customer
};

Simulation::Simulation() {}

double Simulation::get_current_time() const { return current_time; }

double Simulation::expdist(double mean) const
{
    return -mean * log(1 - rand() * 1.0 / RAND_MAX);
}

void Simulation::add_event(Event* evt)
{
    event_queue.push(evt);
}

void Simulation::print() const {}

void Simulation::print_summary() const {}

void Simulation::run(double start_time, double end_time)
{
    current_time = start_time;

    while (event_queue.size() > 0 && current_time <= end_time)
    {
        Event* event = event_queue.top();
        event_queue.pop();
        current_time = event->get_time();
        event->process(*this);
        delete event;
        print();
    }
    print_summary();
}

Event::Event(double event_time)
{
    time = event_time;
}

void Event::process(Simulation& sim) const {}

double Event::get_time() const { return time; }

Arrival::Arrival(double time) : Event(time) {}

void Arrival::process(Simulation& sim) const
{
    double now = sim.get_current_time();
    BankSimulation& bank = dynamic_cast<BankSimulation&>(sim);
    Customer* c = new Customer(now);
    bank.add(c);
}

Departure::Departure(double time, int teller) : Event(time)
{
    this->teller = teller;
}

void Departure::process(Simulation& sim) const
{
    BankSimulation& bank = dynamic_cast<BankSimulation&>(sim);
    bank.remove(teller);
}

Customer::Customer(double time) { arrival_time = time; }

double Customer::get_arrival_time() const { return arrival_time; }

BankSimulation::BankSimulation(int number_of_tellers)
{
    for (int i = 0; i < number_of_tellers; i++)
    {
        tellers.push_back(nullptr);
    }
    total_customers = 0;
    total_time = 0;
}

void BankSimulation::add(Customer* c)
{
    bool added_to_teller = false;
    for (int i = 0; !added_to_teller && i < tellers.size(); i++)
    {
        if (tellers[i] == nullptr)
        {
            add_to_teller(i, c);
            added_to_teller = true;
        }
    }
    if (!added_to_teller) { customer_queue.push(c); }
    add_event(new Arrival(get_current_time() + expdist(INTERARRIVAL)));
}

void BankSimulation::add_to_teller(int i, Customer* c)
{
    tellers[i] = c;
    add_event(new Departure(get_current_time() + expdist(PROCESSING), i));
}

void BankSimulation::remove(int i)
{
```

