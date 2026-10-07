

## C++ 中的 430 数据结构

本节的剩余部分将重点在离散事件模拟的背景下介绍 `priority_queue` 容器。在这种模拟中，物理系统的活动通过在指定时间范围内按顺序发生的一系列事件进行建模。我们将使用的设定是 M/M/n 队列，即具有 $n$ 个服务器的队列，其中客户以速率参数 $\lambda$ 遵循泊松分布到达，且服务时间服从均值为 $\lambda$ 的独立指数分布。假设服务器和客户也是独立运行的。在练习 10.15 中将探索使用 `queue` 类进行类似的开发。

模型的基本元素是客户和服务器，每个元素都需要以类的形式进行开发。首先处理客户类。其声明如下：

```cpp
struct Customer{
    int Arrive;
     bool Gold;
    Customer(int t = 0, bool gold = 0) : Arrive(t), Gold(gold) {}

    bool operator<(const Customer& x) const;
};
```

它有两个成员：客户的到达时间 `Arrival` 和一个布尔变量 `Gold`。`Arrival` 是 `Customer` 对象进入模拟的成员。为了简化问题，时间将以离散（即一分钟）的间隔演进，且 `Arrival` 只取整数值。`Gold` 类代表与租车、航空公司等相关的“金牌”状态的存在或否，频繁的往来可能会导致客户获得优先的“金牌”级别服务。`Gold` 的使用方式是在 `<` 运算符的定义中，该运算符接收：

```cpp
bool Customer::operator<(const Customer& x) const {
    if (Gold == 0 && x.Gold == 0 ||
        Gold == 1 && x.Gold == 1)
        if (Arrive < x.Arrive)); // 到达越早优先级越高
            return false;
    else
        return true;

    if (Gold == 0 && x.Gold == 1)
        return true;
    if (Gold == 1 && x.Gold == 0)
        return false;
}
```

STL `queue` 是一个最大队列，即元素根据 `<` 运算符确定的降序部分排序。在其他条件相同的情况下，我们重载的该运算符的效果是到达越早的客户获得更高的优先级，反之，较晚到达的客户优先级较低。另一方面，具有 `Gold` 值的客户总是比（即 `>=`）`Gold` 值为 `false` 的客户更优的。

输出允许我们跟踪模拟的进度，它是通过一个适用于 `Customer` 对象的重载插入运算符创建的。其形式如下：

```cpp
std::ostream& operator<<(const std::ostream& out, const Customer& x){
    out << "Arrival time = " << x.Arrive << " Gold = " <<
        std::boolalpha << x.Gold << std::endl;
    return out;
}
```

## 队列

我们对 `Server` 定义如下：

```cpp
struct Server{
    bool Busy;
    int serviceTime;
    Server(){
        Busy = 0; serviceTime = 0;
    }
};
```

特定的 `Server` 对象可能正忙于一个 `Customer` 对象，在这种情况下，其布尔成员 `Busy` 将取值为 `true`。否则，`Server` 对象将可以分配给队列中的下一个对象。`Server` 结构体的另一个成员是 `serviceTime`。结合到达时间一起，这将在离散间隔内测量。

有了 `Customer` 和 `Server` 类可用，现在可以在列表 10.6 中定义模拟类。

列表 10.6 MMNQueue.h

```cpp
class MMNQueue{
    std::priority_queue<Customer> Q;
    Server* pS; // 服务器数组
    ranRng Rng; // 随机数生成器
    void update(int t);
    int rPoisson();
    double Exp(double lambda);
    bool isGold();
    void updateServers();
    int freeServer();

    // 模拟参数
    int runTime, nServers;
    double lambdaC, lambdaT, goldProb;
    unsigned long Seed;

    // 统计数据
    int totalTime, numberCustomers;
public:
    MMNQueue(int runtime, int nServers, double lambac,
        double lambdat, double goldProb, unsigned long seed) :
        runTime(runtime), nServers(nServers), lambdaC(lambac),
        lambdaT(lambdat), goldProb(goldProb), Seed(seed){
        totalTime = 0; numberCustomers = 0;
        pS = new Server[nServers];
        Rng = ranRng();
        Rng.setSeed(Seed);
    }
    ~MMNQueue(){
        delete[] pS;
    }
    double runSimulation();
};
```

模拟的参数为：

- runTime: 允许模拟运行的时间长度。
- nServers: 系统服务器的数量。
- lambdaC: 泊松客户到达分布和指数服务时间分布的均值。
- goldProb: `Customer` 对象中“金牌”状态的存在或否，被建模为一个伯努利随机变量，其中 `goldProb` 是 `Gold` 值为 `true` 的概率。
- Seed: 从泊松、指数和伯努利分布生成随机数需要某种随机数生成器。将使用附录 E 中 `randGen` 类中的 `ranUn` 方法。`Seed` 的值提供了初始化生成器的种子。

类构造函数通过初始化列表定义了这些参数。构造函数还创建了服务器数组并对其初始化。

```cpp
double MMNQueue::runSimulation(){
for(int t = 0; t < runTime; t++){
    cout << "time = " << t << endl;
    update(t);
    cout << "queue size " << Q.size() << endl;
}
while(!Q.empty()){ // 队列中剩余的人
    totalTime += runTime - Q.top().Arrive;
    Q.pop(); // 移除客户
}
return ((double)totalTime/numberCustomers);
}
```

```cpp
void MMNQueue::update(int t) {
    updateServers();
    int serverIndex = 0;
    // 上分钟到达的新客户数量
    int numberNew = rPoisson();
    cout << "number of new customers " << numberNew << endl;
    // 尽可能立即服务
    while(freeServer() != -1 && Q.empty() && numberNew > 0){
        serverIndex = freeServer();
        pS[serverIndex].Busy = 1;
        pS[serverIndex].serviceTime = ceil(rExp(lambdaT));
        numberNew--;
    }
    Customer temp;
    if(numberNew > 0){//加入队列
        for(int i = 0; i < numberNew; i++){
            temp = Customer(t,isGold());
            cout << "Waiting customer has " << temp;
            Q.push(temp);
        }
        numberCustomers += numberNew;
    }
    while(freeServer() != -1 && !Q.empty()){
        serverIndex = freeServer();
        pS[serverIndex].Busy = 1;
        pS[serverIndex].serviceTime = ceil(rExp(lambdaT)); 
        totalTime += t - Q.top().Arrive;
        cout << "Customer being served has " << Q.top();
        Q.pop();
    }
}
```

```cpp
void MMNQueue::updateServers() {
    for(int i = 0; i < nServers; i++){
        if(pS[i].serviceTime > 0)
            pS[i].serviceTime--;
        else
            pS[i].Busy = 0;
    }
}
```

