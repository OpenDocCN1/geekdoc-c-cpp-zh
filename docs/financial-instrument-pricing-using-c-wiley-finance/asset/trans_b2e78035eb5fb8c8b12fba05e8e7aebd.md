

## 28.2.1 进入 OpenMP 世界的一个小插曲

我们使用与上面类似的 OpenMP 代码来计算向量元素的和与积。事实上，学习一些 OpenMP 是深入了解多线程的好方法。编写代码并观察其行为很容易。我们首先展示如何查询硬件环境并设置要使用的线程数：

// Maximum # of threads in current team, here == 1 , master thread
std::cout << "Maximum number of threads: " << omp_get_max_threads();
std::cout << "Number of available processors: " << omp_get_num_procs();

// Set the number of threads to use
omp_set_num_threads(4);      // Number of threads = 4
```

我们现在给出计算和与积的三种解决方案：

- 使用 *共享变量* 结合 *临界区*（确保只有一个线程可以更新它们）。这是一种非常低效的解决方案。
- 使用 *归约变量*。这是一种高效的解决方案。
- 一种没有对变量加锁的多线程解决方案。这是一种高效的解决方案，但它会给出错误的结果，因为发生了数据竞争。

这三种情况对应的代码是：

// Using reduction-like variables
double sum = 0.0;
double product = 1.0;

long long N = 4;
std::vector<double>v(N, 0.0);
for (std::size_t j = 0; j < v.size(); ++j)
    { v[j] = 1.0 / static_cast<double>(j + 1); }

#pragma omp parallel for shared(N,v, sum, product)
for (long long j = 0; j < v.size(); ++j)
{
    #pragma omp critical
    { // Slow but thread-safe
        sum +=v[j];
        product *=v[j];
    }
}

std::cout << "Reduction, I: " << sum << ", " << product << '\n';

sum = 0.0;
product = 1.0;
#pragma omp parallel for reduction(+: sum), reduction(*: product)
for (long long j = 0; j < v.size(); ++j)
{
    sum +=v[j];
    product *=v[j];
}

std::cout << "Reduction, II: " << sum << ", " << product << '\n';

// Non thread-safe
{
    double sum = 0.0;
    double product = 1.0;
    #pragma omp parallel for //reduction(+: sum), reduction(*: product)
    for (long long j = 0; j < v.size(); ++j)
    {
        sum += v[j];
        product *= v[j];
    }
    std::cout << "Reduction, III: " << sum << ", " << product;
}
```

C++11 不支持归约变量。遗憾的是，本书的范围不包括对 OpenMP 的进一步讨论。

## 28.3 创建线程的六种方法

在介绍了 std::thread 并给出一些使用简单线程函数（存储的 lambda 函数）编写多线程代码的示例之后，我们现在讨论容纳各种可调用对象的其他方法，其中一些在本书的第 2 章和第 3 章中已介绍过：

- 1. 使用全局/自由函数的线程。
- 2. 使用静态函数的线程。
- 3. 使用可调用类型的线程。
- 4. 使用成员函数（无参数）的线程。
- 5. 使用成员函数（带参数）的线程。
- 6. 使用 lambda 函数的线程。

我们采用通用示例来展示代码的工作原理。然后就可以将代码扩展和推广到更广泛的示例和计算金融中的应用。为此，我们创建一个函数，根据选择返回 std::thread 的实例：

// Function to create a thread with different styles of functions
std::thread CreateThread(int i)
{
    // Create a thread using the requested function
    switch (i)
{
    default:
    case 1:
    {
        // Create thread with a function pointer to a
        // global function (& can be left out)
        return std::thread(&GlobalFunction);
    }

    case 2:
    {
        // Create thread with a function pointer to a
        // static function (& can be left out)
        return std::thread(&CallableClass::StaticFunction);
    }

    case 3:
    {
        // Ask the number of iterations
        std::cout<<"Number of iterations: ";
        int iterations;
        std::cin>>iterations;

        // Create thread with a callable class (has operator() )
        // CallableClass object is copied to the thread so its
        // lifetime is the same as that of the thread
        CallableClass c(iterations);
        return std::thread(c);
    }

    case 4:
    {
        // Ask the number of iterations
        std::cout << "Number of iterations: ";
        int iterations;
        std::cin >> iterations;

        // Create thread with a callable class (has operator() )
        // CallableClass object is copied to the thread so
        // its lifetime is the same as that of the thread
        CallableClass c(iterations);
        return std::thread(&CallableClass::Algorithm, &c);
    }
    case 5:
    {
        // Ask the number of iterations
        std::cout << "Number of iterations: ";
        int iterations;
        std::cin >> iterations;

CallableClass c(iterations);
return std::thread(&CallableClass::AlgorithmII, &c, 20);
}
case 6:
{
    // Create thread with a lambda function
    return std::thread([]()
    { std::cout << "lambda called\n"; });
}
}
}
```

自由（全局）函数的代码为：

// Global function called by thread
void GlobalFunction()
{
    for (int i=0; i<10; i++)
    {
        std::cout<< i
                 <<" - Do something in parallel of main "<<'\n';
        std::this_thread::yield();
    }
}
```

此代码中使用的类 CallableClass 具有以下接口和主体：

// Class that is a callable type (has operator() )
class CallableClass
{
private:
    // Number of iterations
    int m_iterations;

public:
    // Default constructor
    CallableClass()
    {
        m_iterations=10;
    }

    // Constructor with number of iterations
    CallableClass(int iterations)
    {
        m_iterations=iterations;
    }

    // Copy constructor
    CallableClass(const CallableClass& source)
{
    m_iterations=source.m_iterations;
}

// Destructor
~CallableClass()
{
}

// Assignment operator
CallableClass& operator = (const CallableClass& source)
{
    m_iterations=source.m_iterations;
    return *this;
}

// Static function called by thread
static void StaticFunction()
{
    for (int i=0; i<10; i++)
    {
        std::cout<<i<<
            " - Do something in parallel static"<<'\n';
        std::this_thread::yield();
    }
}

// Operator() called by the thread
void operator () ()
{
    for (int i=0; i<m_iterations; i++)
    {
        std::cout<<i<<"Do with main method ()"<<'\n';
        std::this_thread::yield();
    }
}

void Algorithm ()
{
    for (int i = 0; i<m_iterations; i++)
    {
        std::cout << i << " - Cooperative processing";
        std::this_thread::yield();
    }
}

void AlgorithmII(int count)
{
    for (int i = 0; i<count; i++)
    {
        std::cout << i << "Algorithm with parameter, value " << count;
        std::this_thread::yield();
    }
}
};
```

一个简单的测试程序是：

// Entry point of the program.
int main()
{
    // Display the number of processors/cores
    std::cout<<std::thread::hardware_concurrency()
        <<" processors/cores detected."<<'\n'<<'\n';

    int choice;

    // Do till exit
    do
    {
        // Display menu
        std::cout<<"1. Thread with global/free function"<<'\n';
        std::cout<<"2. Thread with static functions"<<'\n';
        std::cout<<"3. Thread with callable type"<<'\n';
        std::cout <<"4.Thread with member func(no args)"<< '\n';
        std::cout << "5. Thread with member func(+ arg)" << '\n';
        std::cout << "6. Thread with lambda function" << '\n';
        std::cout<<"0. Exit"<<'\n';
        std::cout<<"Your choice: ";

        // Read input
        std::cin>>choice;

        if (choice>0 && choice<7)
        {
            // Create and start thread
            std::thread t(CreateThread(choice));

            // Do something
            for (int i=0; i<10; i++)
            {
                std::cout<<i<<" - Do something in main."<<'\n';
                std::this_thread::yield();
            }

            // Wait till thread is finished
            t.join();
        }

        // Empty line
        std::cout<<'\n';

