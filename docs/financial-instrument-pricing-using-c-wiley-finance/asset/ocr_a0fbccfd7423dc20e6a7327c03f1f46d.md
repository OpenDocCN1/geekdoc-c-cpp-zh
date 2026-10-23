# Parallel Patterns Language (PPL)

# 30.1 INTRODUCTION AND OBJECTIVES

In this chapter we introduce the Parallel Patterns Library (PPL) that implements an imperative programming model to promote scalability and ease of use when developing concurrent applications. PPL is a Microsoft product and has been supported since Visual C++ 2010. It is not part of the C++ standard and there are other libraries (such as Intel’s Threading Building Blocks (TBB)) that offer similar functionality. Prediction is difficult but our guess is that future versions of the C++ standard might contain functionality that is not unlike that of PPL and TBB. PPL is easy to learn and to use in applications. The syntax is similar to that of STL and it supports C++11. The main challenge now is knowing which design pattern to use in a given context.

We assume the following prerequisites on the part of the reader (these topics have been discussed in previous chapters):

+   - Working knowledge of lambda functions, stored lambda functions, captured variables and closures.
+   - Knowing what parallel design patterns are and how to identify them in applications.
+   - Knowing the reasons for using parallel libraries and what the resulting consequences are.

Before we discuss PPL in detail we first give an overview of the lower-level component that is called the Concurrency Runtime. In a sense it abstracts away low-level infrastructure details related to concurrency. Its two main components are:

+   - Task Scheduler: this component can be seen as a special kind of thread pool which is used to optimise large numbers of fine-grained work requests. It does not automatically create a new worker thread when a request arrives but instead it queues the new task and executes it when processor resources become available.
+   - Resource Manager: this component allocates processor cores among an application’s task schedulers. It ensures that related tasks execute optimally in the sense of accessing hardware cache. It also provides dynamic resource management to adjust the level of concurrency across components based on core utilisation.