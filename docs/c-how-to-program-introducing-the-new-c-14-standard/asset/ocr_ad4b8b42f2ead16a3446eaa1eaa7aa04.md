# 16.2 Minimum Iterator Requirements

With few exceptions, the *Standard Library* separates algorithms from containers. This makes it much easier to add new algorithms and to use them with multiple containers. An important part of every container is the *type* of iterator it supports (**Fig. 15.7**). This determines which algorithms can be applied to the container. For example, both `vectors` and `arrays` support *random-access iterators* that provide all of the iterator operations shown in **Fig. 15.9**. *All* Standard Library algorithms can operate on `vectors` and those that do not modify a container’s size can also operate on `arrays`. Each Standard Library algorithm that takes iterator arguments requires those iterators to provide a minimum level of functionality. If an algorithm requires a *forward iterator*, for example, that algorithm can operate on any container that supports *forward iterators*, *bidirectional iterators* or *random-access iterators*.

![](bbox=[0.12, 0.725, 0.196, 0.79])

# Software Engineering
Observation 16.1