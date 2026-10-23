

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_1046_0.png)

数据流
控制流（开始/停止）

## FIGURE 32.3 消息传递用于蒙特卡洛

```
private:
    // The target buffer to write to.
    concurrency::ITarget<double>& _target;
    // The sentinel value
    concurrency::ITarget<bool>& _stop;

    // MIS
    concurrency::ITarget<std::size_t>& _mis;

    int NT;
    int NSIM;

    std::shared_ptr<Sde> sde;
    double S0;

    // ...
};

class OptionPricer : public concurrency::agent
{
private:
    // The source buffer to read from.
    concurrency::ISource<double>& _source;

    // Send sentinel value to target
    concurrency::ISource<bool>& _stop;

    // ...
};
```

类 PathEvolver 启动并停止应用程序。其他代理就像从它那里接收指令一样。我们可以通过检查它们的 run() 方法来了解代理如何通信：

```
void run()
{
    // Path Evolver
    ThreadSafePrint("Starting producer");
    concurrency::send(_stop, false);
    std::default_random_engine dre;
    std::random_device rd;
    dre.seed(rd());
    std::normal_distribution<double> nor(0.0, 1.0);

    double k = sde->expiration() / static_cast<double>(NT);
    double sqrk = std::sqrt(k);
    double v;

    for (std::size_t n = 0; n < NSIM; ++n)
    {
        concurrency::send(_mis, n);

        double VOld = S0; double VNew;
        double x = 0.0;

        for (long index = 0; index < NT; ++index)
        {
            v = nor(dre);
            // FDM (explicit Euler), equation (9.2) from the text
            VNew = VOld + (k * sde->drift(x, VOld))
                + (sqrk * sde->diffusion(x, VOld) * v);

            VOld = VNew;
            x += k;
        }
        concurrency::send(_target, VNew);
    }
    concurrency::send(_stop, true);

    // Set the agent to the finished state.
    done();
    ThreadSafePrint("Exit producer");
}
```

和

```
// Option Pricer
void run()
{
```

```
double payoffT;
double avgPayoffT = 0.0;
double squaredPayoff = 0.0;
double sumPriceT = 0.0;
int NSIM = 0;
double VNew;

bool stop;
while ((stop = concurrency::receive(_stop)) == false)
{
    // Assemble quantities (postprocessing)
    VNew = concurrency::receive(_source);
    payoffT = myOption.myPayOffFunction(VNew);

    sumPriceT += payoffT;
    avgPayoffT += payoffT / NSIM;
    avgPayoffT *= avgPayoffT;

    squaredPayoff += (payoffT*payoffT);
    NSIM++;
}

// Finally, discounting the average price

price = std::exp(-myOption.r * myOption.T) * sumPriceT
        / static_cast<double>(NSIM);

done();
ThreadSafePrint("Exit consumer");
}
```

管理系统从路径演化器接收进度信息：

```
class MIS : public concurrency::agent
{
private:
    concurrency::ISource<std::size_t>& _mis;
    // Send sentinel value to target
    concurrency::ISource<bool>& _stop;

    std::size_t freq;

public:
    explicit MIS(concurrency::ISource<std::size_t>& mis,
    concurrency::ISource<bool>& stop,std::size_t frequency)
        : _mis(mis), _stop(stop), freq(frequency) {}

    void run()
{
```

```
bool stop;
std::size_t f;
while ((stop = concurrency::receive(_stop)) == false)
{
    f = concurrency::receive(_mis);
    if (((f/freq)*freq == f))
    {
        std::cout << f << ",";
    }
}

done();
ThreadSafePrint("Exit MIS");
};
```

为完整起见，我们展示了以线程安全方式在控制台打印文本的实用函数：

```
void ThreadSafePrint(const std::string& s)
{ // Function to avoid garbled output on the console

    std::mutex my_mutex;
    std::lock_guard<std::mutex> guard(my_mutex);
    std::cout << s << '\n';
}
```

我们现在讨论根据 Actor 模型配置蒙特卡洛期权计算器所需的步骤。该模型基于设计决策，即路径演化器将数据传递给多个定价代理，并且还可以向多个管理和看守系统发送进度信息。我们在图 32.4 中用 UML 图表示这些需求。换句话说，该图提供了如何配置应用程序的见解。特别是，我们注意到代理之间的 1:N 多重性关系。我们讨论一个示例。首先，我们创建消息缓冲区和期权相关数据：

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_1049_0.png)

FIGURE 32.4 UML 类图（带多重性）

// A message buffer that is shared by the agents.
concurrency::overwrite_buffer<double> buffer;
concurrency::overwrite_buffer<bool> sentinel;

// Communication with MIS agent (draw count)
concurrency::overwrite_buffer<std::size_t> misCount;

// Create and start the producer and consumer agents.
OptionData myOption((
    OptionParams::strike = 65.0, OptionParams::expiration = 0.25,
    OptionParams::volatility = 0.3, OptionParams::dividend = 0.0,
    OptionParams::optionType = 1,OptionParams::interestRate = 0.08));

OptionData myOption2((
    OptionParams::strike = 65.0, OptionParams::expiration = 0.25,
    OptionParams::volatility = 0.3, OptionParams::dividend = 0.0,
    OptionParams::optionType = -1,OptionParams::interestRate= 0.08));

// ATM
OptionData myOption3((
    OptionParams::strike = 60.0, OptionParams::expiration = 0.25,
    OptionParams::volatility = 0.3, OptionParams::dividend = 0.0,
    OptionParams::optionType = -1,OptionParams::interestRate= 0.08));

我们现在创建一个路径演化器和四个定价器（它们是路径信息的消费者）：

```
int NT = 500;
int NSIM = 1'000'000;

StopWatch<> sw;
sw.Start();

// Create SDE
auto sde1 = std::shared_ptr<Sde>(new Sde(myOption));
double S0 = 60.0;
PathEvolver producer(buffer, sentinel, misCount, NT, NSIM, sde1, S0);

// Define pricers
OptionPricer consumer(buffer, sentinel,myOption);
OptionPricer consumer2(buffer, sentinel, myOption2);
OptionPricer consumer3(buffer, sentinel, myOption);
OptionPricer consumer4(buffer, sentinel, myOption3);
MIS mis(misCount, sentinel, 100'000);
```

最后，我们启动代理，等待它们完成，然后计算期权价格：

```
producer.start();
consumer.start();
```

```
consumer2.start();
consumer3.start();
consumer4.start();
mis.start();

// Wait for the agents to finish.
concurrency::agent::wait(&producer);
concurrency::agent::wait(&consumer);
concurrency::agent::wait(&consumer2);
concurrency::agent::wait(&consumer3);
concurrency::agent::wait(&consumer4);
concurrency::agent::wait(&mis);

sw.Stop();
std::cout << "Elapsed time, Raw creation: " << sw.GetTime() << '\n';

std::cout << '\n' << consumer.Price() << '\n';
std::cout << '\n' << consumer2.Price() << '\n';
std::cout << '\n' << consumer3.Price() << '\n';
std::cout << '\n' << consumer4.Price() << '\n';
```

此示例展示了使用 Agents 库在蒙特卡洛期权定价模拟器中使用时需要采取的基本步骤。

## 32.6 SUMMARY AND CONCLUSIONS

### 32.6.1 Appendix: C++ for Closed-Form Solution of CEV Option Prices

我们将有限差分格式对 CEV 期权价格的近似与公式 (32.13) 中的闭式解进行了测试。我们讨论了如何对这些后者公式进行编码。我们在斜率参数 β 小于一和大于一的情况下计算看跌期权和看涨期权价格。当它恒等于一时，我们得到 Black–Scholes 价格，并且当前公式不应使用，因为我们会得到除以零异常。

因此，我们有四个公式来计算 CEV 期权价格，我们根据公式 (32.13) 描述了代码的结构。首先，主函数是：

```
std::tuple<double, double> CEV(const OptionData& opt, double S, int beta)
{ // Main function to compute exact CEV puts and calls.

    if (beta < 1)
    {
        return CEV_I(opt, S, beta);
    }
    else
    {
        return CEV_II(opt, S, beta);
    }
}
```

```
```cpp
double c = 1.0 / (1.0 - beta);
double w = 0.5*sig*sig*
(std::exp(2.0*(r - q)*(beta - 1.0)*T) - 1.0)/((r - q)*(beta - 1.0));
double b = std::pow(K*std::exp(-(r - q)*T), 2.0*(1.0 - beta)) * c * c/w;
double d = std::sqrt(S, 2.0*(1.0 - beta)) * c * c / w;

boost::math::non_central_chi_squared_distribution<double> dist1(c, b);
val1 = boost::math::cdf(dist1, d);
boost::math::non_central_chi_squared_distribution<double>
                                      dist2(c+2, d);

val2 = boost::math::cdf(dist2, b);
}

void ChiSquaredValues2(const OptionData& opt, double S, int beta,
                       double &val1, double &val2)
{

    double r = opt.r; double K = opt.K; double q = opt.D;
    double T = opt.T; double sig = opt.sig;

    double c = 1.0 / (1.0 - beta);
    double w = 0.5*sig*sig*
    (std::exp(2.0*(r - q)*(beta - 1.0)*T) - 1.0) / ((r - q)*(beta - 1.0));
    double b = std::pow(K*std::exp(-(r - q)*T), 2.0*(1.0 - beta)) * c * c/w;
    double d = std::sqrt(S, 2.0*(1.0 - beta)) * c * c / w;

    boost::math::non_central_chi_squared_distribution<double> dist1(-c, b);
    val1 = boost::math::cdf(dist1, d);
    boost::math::non_central_chi_squared_distribution<double>
                                      dist2(2-c, d);

    val2 = boost::math::cdf(dist2, b);
}
```
```

作为健全性检查，我们创建一个测试 *put–call parity* 的函数（以防代码或公式在某些情况下出现错误或失效）：

```
```cpp
void PutCallParity(const OptionData& opt, double S, int beta)
{
    // Calculate prices
    auto tup = CEV(opt, S, beta);

    double P = std::get<0>(tup);
    double C = std::get<1>(tup);

    double lhs = C + opt.K*std::exp(-opt.r*opt.T);
    double rhs = P + S;

    std::cout << "put call parity " << lhs - rhs << '\n';
}
```
```

