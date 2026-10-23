
```cpp
// Define variables needed by payoffs and pricers
double r = opt.r; double q = opt.q;
double T = opt.T;
double K = opt.K;
double S = opt.sig;
double S0 = 100.0;
double Q = 10.0;

// Define payoffs
double d1 = (std::log(S0/K)
          + (r -q + 0.5*s*s)*T) / (s*std::sqrt(T));
double d2 = d1 - s*std::sqrt(T);

// Cash-or-nothing options
auto CashOrNothingCallPayoff = [_] (double S)-> double
{
    if (S <= K) return 0.0;
    return Q;
};

auto CashOrNothingPutPayoff = [_] (double S)-> double
{
    if (S >= K) return 0.0;
    return Q;
};

auto CashOrNothingCallPrice = [_] (double S)-> double
{
    return Q*std::exp(-r*T)*NCdf(d2);
};

auto CashOrNothingPutPrice = [&] (double S)-> double
{
    return Q*std::exp(-r*T)*NCdf(-d2);
};

// Exercise to test this

// Asset-or-nothing options
auto AssetOrNothingCallPayoff = [_] (double S)-> double
{
    if (S <= K) return 0.0;
    return S;
};

auto AssetOrNothingPutPayoff = [_] (double S)-> double
{
    if (S >= K) return 0.0;
    return S;
};

auto AssetOrNothingCallPrice = [=] (double S) -> double
{
    return S*std::exp(-q*T)*NCdf(d1);
};

auto AssetOrNothingPutPrice = [=] (double S) -> double
{
    return S*std::exp(-q*T)*NCdf(-d1);
};

double NCdf(double x)
{
    // Normal cumulative distribution

    boost::math::normal_distribution<> myNormal(0.0, 1.0);
    return boost::math::cdf(myNormal, x);
}
```

## 10. (Parallelising the Generalised Binomial Method)

The objective of this exercise is to parallelise the algorithms to compute call and put option prices for a range of payoffs in equations (12.5) and (12.6). In all cases we return the prices in a 2-tuple.

Answer the following questions:

+   a) Implement equations (12.5) and (12.6) by Bernoulli paths using sequential C++ (a single thread). Test the code for standard calls and puts as well as the following two option types:
+   
+   **Standard power contract:**
+   
+   \[
+   g(S) = \max(K - S^p, 0), \quad \text{(put)}\ p > 0
+   \]
+   \[
+   g(S) = \max(S^p - K, 0), \quad \text{(call)}\ p > 0
+   \]
+   
+   **Power contract:**
+   
+   \[
+   g(S) = (S/K)^p, \quad p > 0.
+   \]

In the case of a standard power contract we use the following data: S = 555, K = 550, r = 0.06, volatility = 0.15, dividend yield = 0.04, T = 0.5. For p = 0.96 we get C = 0.17614 and for p = 1.05 we get C = 213.01648.

+   b) We wish to parallelise the code in part a) using C++ threads. To this end, we divide the index range [0, n] in equations (12.5) and (12.6) into four subranges. We then assign each subrange to a single thread and each thread computes a part of the price. Then the partial sums are added together to give the final answers. Compare the prices with those computed in part a).
+   
+   c) Compare the run-time performance of the solutions in parts a) and b).
+   
+   d) (After you have read Sections 30.2.4 and 30.4 of Chapter 30.) The objective now is to apply the *parallel reduction technique* and *Aggregation/Reduction pattern* from the PPL to achieve the same result as in part b).
+   
+   e) Solve the current problem using OpenMP’s *reduction* clause. A simple example to motivate your solution is:

```
int N = 10000;
double vec1[N];
double vec2[N];
double sum = 0.0;
int i;
#pragma omp parallel for reduction (+:sum)
for (i = 0; i < N; ++i)
    sum += vec1[i]*vec2[i];
```

## 11. (Parallelising the Finite Difference Method)

In Chapters 20 to 23 we discussed how to approximate the solution of partial differential equations using the finite difference method. We proposed a number of schemes and we give some examples (see Section 21.8 for more details):

```
CNIBVP fdmCN(currentImp, earlyExercise,N, J);
ImplicitEulerIBVP fdmIE(currentImp, earlyExercise,N, J);
ExtrapolatedImplicitEulerIBVP fdmEIE (currentImp,earlyExercise,N, J);
ADE fdmADE(currentImp, earlyExercise,N, J);
ADE_BC_CRTP fdmADE2(currentImp, earlyExercise,N, J);
ADE_Larkin_RW_CRTP fdmADE3(currentImp, earlyExercise,N, J);
ADEExtrapolated fdmADE4(currentImp, earlyExercise, N, J);
```

In general, we can think of several use cases and viewpoints to take in order to test finite difference schemes for accuracy and performance:

+   UC1: Compare the accuracy of a new finite difference scheme with an accurate baseline scheme or exact solution.
+   UC2: Stress test a scheme for a range of input parameters to the PDE. The parameters are randomly generated using the designs that we used in Chapter 16 (in particular, Section 16.4). The focus is to determine the robustness and accuracy of a scheme for a range of input parameters.
+   UC3: Compute option prices for an input data set.

We focus on questions related to case UC3.

Answer the following questions:

+   a) Adapt the code in Section 28.4 to test the Crank–Nicolson, ADE and MOL against each other. Each scheme will be run in its own thread.
+   b) Compute the option price in each case and compare the prices regarding accuracy. Concentrate on the cases where the differences are greater than a given tolerance.
+   c) Extend the code in parts a) and b) to the case where the input data is generated using the techniques we used in Section 16.4. Create a loop with a given number of iterations and compute the global maximum error between the solutions from all runs of random generation of the input data.

The advantage of this approach is that you can run the program in batch mode as it were, and when you come back from lunch it will give output on the accuracy of the scheme that you are testing.

## C++ Concurrency, Part II Tasks

## 29.1 INTRODUCTION AND OBJECTIVES

In this chapter we discuss how C++ supports the creation of programs and algorithms by decomposing them into components that can potentially run in parallel. In general terms, potential or exploitable concurrency involves being able to structure code to permit a problem’s subproblems to run on multiple processors. Each subproblem is implemented by a task. A task (Quinn, 2004) is a program in local memory in combination with a collection of I/O ports. Tasks send data to other tasks through their output ports and they receive data from other tasks through their input ports. It is obvious from this discussion that tasks can depend on other tasks because they need the data that is produced by other tasks. We model these dependencies by a data dependency graph or task graph. This is a directed graph where each vertex represents a task to be completed and an edge from vertex a to vertex b means that task a must complete before task b begins. The absence of an edge between two vertices means that there is no dependency between them and hence the related tasks can be run in parallel.

The goals of this chapter are to:

+   1. Analyse a program for potential parallelism. Create a data dependency graph to identify the main tasks and their dependencies.
+   2. Apply task and data decomposition patterns to break a program into pieces that can execute concurrently (Mattson, Sanders and Massingill, 2005).
+   3. Choose an algorithm structure pattern that is effective, simple and portable (Mattson, Sanders and Massingill, 2005).
+   4. Map the products from step 3 to multitasking language features in C++.

From this list we note that no mention has been made of the object-oriented programming model or threads. In the former case we do not see object technology as the main driver of parallel programming design and in the latter case we shall see tasking as being easier to apply and less error-prone than the use of threads. In short, we wish to have a one-to-one relationship between the tasks and their implementation in C++. To this end, we discuss the following language features:

+   - Implementing asynchronous operations.
+   - Using futures and promises to access the results of asynchronous operations.
+   - Running a function asynchronously by calling `std::async`.
+   - Using *shared futures* to access the results of asynchronous operations. These are similar to ‘normal’ futures except that multiple threads are allowed to wait for the same shared state in the former case.
+   - Creating a *packaged task* to wrap a *callable object* (for example, free function, lambda function, bind expression or function object) so that it can be invoked asynchronously.
+   - Exception handling in multitasking applications.

Summarising, we trace the design trajectory from initial requirements to implementing a parallel program in C++. We take simpler examples for motivation and we examine the applicability of the C++ *Concurrency* library to a number of the applications in this book, for example the Monte Carlo and finite difference methods. These design techniques can also be applied to other problems in computational finance.

## 29.2 FINDING CONCURRENCY: MOTIVATION

*Concurrency* refers to the existence of multiple threads of execution, each one receiving a slice of time to execute before being pre-empted by another thread. Concurrency is a requirement for a program that must react to external events and to stimuli resulting in data transfer from user input devices and sensors, for example. Typical examples of concurrent programs are operating systems and computer games. We note that a program can be concurrent even on a one-core machine. *Parallelism* involves several threads executing at the same time on multiple cores. The main goal of *parallel programming* is to improve the performance of compute-intensive applications that should not be interrupted when running on multiple cores. A task is the smallest exploitable unit of concurrency.

We are interested in applications that consist of concurrent tasks running on multiple processors. The question is how to design a system that makes optimal use of available hardware. In short, we wish to improve the *speedup*. Speedup is a scalar value that indicates how many times faster a parallel program executes than its sequential counterpart. It is intuitively obvious that we must find some way to decompose a system into tasks with each one running on a single processor. A task should not be too *coarse grained* or too *fine grained*.

It is not clear to the author how traditional object-oriented technology can be used as the driver of a system decomposition into concurrent tasks. Even in the case of a system that will run in single-threaded mode we use system decomposition methods as introduced in Chapter 9 rather than initially looking for objects and classes. On a related note we can imagine that porting single-threaded C++ applications to parallel code will be very time-consuming at best and impossible at worst. It is a dilemma and the possible choices are to do nothing to the application or to redesign it from scratch.

We now embark on a discussion of how to analyse and design parallel programs. In all cases and at each level of abstraction we are looking for ways to break a system into (quasi-)independent concurrent tasks. At some stage objects and classes will play a role, but only when we are reasonably sure that the *design blueprints* are stable.

### 29.2.1  Data and Task Parallelism

The two main decomposition patterns to break a problem into subproblems that can execute concurrently are based on data and tasks. *Task parallelism* (also known as *function parallelism*
