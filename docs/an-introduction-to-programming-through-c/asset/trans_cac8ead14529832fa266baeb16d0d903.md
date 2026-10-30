

```cpp
class sim{
    typedef std::function<void()> Event;
    typedef pair<Event,double> ETpair;
    struct compareETpair{
        bool operator()(ETpair p, ETpair q){return p.second > q.second;}
    };
    static double time;    // time to which the system has been simulated
    static priority_queue< ETpair, vector<ETpair>, compareETpair> pq;

public:
    static void post(double latency, Event e){
        pq.push(make_pair(e, time + latency));
    }

    static double getTime(){return time;}

    static void processAll(double tmax=1000){
        while(!pq.empty() && time < tmax){
            ETpair ETp = pq.top();
            time = ETp.second;
            pq.pop();
            ETp.first();
        }
    }

    static ostream & log(){
        cout << time << ") ";
        return cout;
    }
};

// Initialization of the static elements.

double sim::time = 0;
priority_queue< sim::ETpair, vector<sim::ETpair>, sim::compareETpair> sim::pq;
```

图 25.2：主要的仿真类

当你执行时，前两条语句会使事件 A、B 被发布，分别在当前时间后 15 和 5 个时间单位发生。仿真从时间 0 开始，因此这些事件将分别在时间 15 和 5 发生。程序中的第三条语句将导致系统被演进，即队列中的所有事件都将被处理，按它们预期发生的时间顺序处理。因此，安排在时间 5 的事件 B 将首先被处理，即其 lambda 表达式将被调用。这将导致消息 "Event B." 被打印，并在前面加上仿真时间，这是由于对 sim::log 的调用。之后事件 A 将被处理。因此你会得到以下输出。

5) Event B.
15) Event A.

需要注意的是，在程序中事件 A 的创建发生在事件 B 的创建之前。然而，A 的时间 15 大于 B 的时间 5。因此在执行期间 B 先于 A 发生。

正如我们在第 25.1.1 节中所讨论的，在离散时间系统中，事件通常会导致某些实体的状态发生变化，并导致新事件的创建（发布）。我们现在将考虑一个事件同时执行这两项操作的例子。这个例子将包含所有未来仿真中使用的核心惯用法。

在下面的程序中，我们有 4 个事件 A、B、C、D。我们还有一个变量 count。我们将看到事件会访问这个变量（“仿真状态”），事实上事件 D 将在事件 C 发生期间被发布。

```
int main(){
    int count=0;
    sim::post(15, [&](){sim::log() << "A. count: "<< count++ <<endl;}); //A
    sim::post(5, [&](){sim::log() << "B. count: "<< count++ <<endl;});   //B
    sim::post(10, [&](){
        sim::log() << "C. count "<< count++ <<endl;
        sim::post(100, [&](){sim::log() << "D. count: " <<
                            count++ << endl;});
    });
    sim::processAll();
}
```

程序首先将 count 设置为 0，然后为时间 15、5、10 分别发布事件 A、B、C。然后 sim::processAll 导致已发布的事件被处理。

发布的最早时间是事件 B，因此它首先被处理。这将导致打印 B 的发生时间以及 count 的值。请注意 count 是通过引用捕获到事件中的，因此在事件发生时该值将被打印。因此我们将看到以下输出。

5) B. count: 0

请注意在打印时，count 也被递增。由于 count 是通过引用捕获的，递增将影响程序第一行中定义的变量 count。因此它将变为 1。

发布下一个最早时间 10 的事件是事件 C，随后被处理。处理首先通过打印消息和 count 的值开始。请注意在事件 C 中变量 count 也是通过引用捕获的。因此以下消息将被打印

```
10) C. count: 1
```

并且 count 将被递增。但是事件 C 的处理在打印消息后并未停止。打印后，调用 sim::post 被执行，这导致事件 D 作为事件 C 发生的一部分而被创建。事件 D 应在当前时间之后 100 步发生，即 10。因此事件 D 被发布到时间 110。因此当 C 的处理结束时，队列中有两个事件 A、D，并且 count 的值为 2。

再次，最早的事件将被处理，即事件 A。这将打印一条消息：

```
15) A. count: 2
```

并将 count 递增到 3。

之后事件 D 将被处理。这将打印一条消息：

```
110) D. count: 3
```

并导致 count 递增到 4。请注意消息中的时间——sim::log 确实会打印 110，即我们期望事件发生的时间。

## 25.2 餐厅仿真

我们现在展示如何编程餐厅仿真。它由若干参数表征，餐厅容量（即桌子数量）、餐厅开放的持续时间（以分钟计）、下一分钟顾客到达的概率，以及顾客用餐时间的最小值和最大值。餐厅状态由被占用的桌子数量组成。

在餐厅开放的每一分钟，顾客可能以指定概率到达。我们将每次到达建模为一个事件。到达时，顾客会检查是否有空闲桌子，如果没有，顾客就会离开，我们应该打印一条相应消息。如果有空闲桌子，则顾客占用一张桌子并坐下用餐。然后随机选择一个用餐时长，顾客必须在该时长后离开餐厅。我们也将离开建模为一个事件。因此顾客的到达事件必须执行上述操作，包括创建离开事件。所有这些都进入到达事件的 lambda 表达式中。在离开时，只需要减少被占用桌子的数量。因此递减代码必须放在离开事件的 lambda 表达式中。

因此代码如下。

```
int main(){
const int capacity=5;                // number of tables
const int duration=180;              // minutes open
double arrivalP=0.1, eatMin=21, eatMax=40;

int nOccupied = 0 ;
int id = 0;

for(int t=0; t<duration; t++){
    if(randuv(0,1) <= arrivalP){        // with probability arrivalP
        id++;
        sim::post(t, [=,&nOccupied](){
            if(nOccupied >= capacity)        // if no table available
                sim::log()<< " Customer " << id << " disappointed.\n";
            else{                            // if a table is available
                ++nOccupied;
                int eatTime = randuv(eatMin, eatMax);
                sim::log()<<" Customer " << id << " will eat for "<<eatTime<<"\n";
                sim::post(eatTime, [=,&nOccupied](){
                    sim::log()<< " Customer " << id << " finishes.\n";
                    --nOccupied;
                });
            }
        });
    }
}
sim::processAll();
}
```

## 25.3 资源

许多现实生活系统包含稀缺的资源。例如，同一台机器可能需要处理多个作业，而它在任何瞬间只能处理其中一个。在这种情况下，作业必须等待以获得对机器的独占访问。

作为一个例子，考虑一个由单个服务员管理的路边咖啡店。假设商店提供饮料和食物，所有这些都需要服务员付出一定的努力和时间。如果顾客到达时服务员正忙于之前的顾客，那么新顾客必须等待。因此在受欢迎的咖啡店可能会形成等待顾客的队伍。给定顾客到达的概率和服务时间的概率分布，我们能否预测商店的业务量以及队伍有多长？

我们将开发一个 Resource 类，这将使编写此类仿真变得容易。

### 25.3.1 一个 Resource 类

到目前为止，我们已经说过事件可以被创建并发布以在未来的某个时间发生。我们将扩展这一概念，允许事件被发布以在某个资源可用时发生。如果资源立即可用，则事件将立即发生。否则，它将被放入与该资源关联的队列中。当资源因其他事件释放而变得可用时，等待的事件将被取出队列并发布以立即执行。

