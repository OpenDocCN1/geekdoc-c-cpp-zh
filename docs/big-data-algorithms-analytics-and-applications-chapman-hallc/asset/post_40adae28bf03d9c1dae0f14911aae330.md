
Data streaming is the main reason for the new design in this section. Time awareness and processing during replay are the features of the new design that are implemented with data streaming in mind. Coincidentally, the resulting architecture can benefit from running on multicore hardware.

*Multicore* technology is a special case of parallel processing [24]. It has already been applied to MapReduce in Reference 4, which improves its performance but does not solve the other problems discussed in this section. Most existing multicore methods implement traditional scheduling-based parallelization [4,24,25], which requires intensive message exchange across processes. This chapter uses a special case of parallelization, which features minimum overhead due to a lock-free design. More details are presented further in this section.

## 12.4 THE DATA STREAMING PROBLEM

This section is specific to data streaming. It may sound like data streaming is only about methods that are used to *stream* data, but in fact, the topic is extremely rigorous scientifically. The rigor is the information theory that underlies the topic. But many formulations in data streaming are demanded in new areas of data processing and therefore require somewhat new-looking formulations. Although data streaming is commonly written with a great deal of mathematical notation, this section and this chapter as a whole will stick to the bare minimum of math, strictly with the purpose of providing basic understanding of the numeric essence of formulations.

A second round of terminology is presented in Section 12.4.1.

### 12.4.1 Data Streaming Terminology

As was mentioned before, the terms *data streams*, *data streaming*, and *streaming algorithms* all refer to the same class of methods.

*Bloom filter* and *Bloom structure* both refer to a space in memory that stores the current state of the filter, which normally takes the form of a bit string. However, the Bloom filter itself is not only the data it contains but also the methods used to create and maintain the state.

A *Double-Linked List* (*DLL*) is also a kind of structure. However, DLLs are arguably exclusively used in *C/C++* [14,26]. This is not 100% true—in reality, even this author has been able to use DLLs in other programming languages like *PHP* or *JavaScript*—but *C/C++* programs can benefit the most from DLLs because of the nature of pointers in *C/C++* versus those in any other programming language. DLLs refer to a memory structure (*struct* in *C/C++*) alternatively to traditional lists—vectors, stacks, and so forth. In DLLs, each item/element is linked to its neighbors via raw *C/C++* pointers, thus forming a chain that can be traversed in either direction. DLLs are revisited later in this chapter and are part of the practical application discussed at the end of the chapter.

The terms *word*, *byte*, and *digest* are specific to hashing. The word is normally a 32-bit (4-B) integer on 32-bit architectures. A hashing method *digests* an arbitrary length input at the grain of a *byte* or *word* and outputs a hash key. Hashing often involves *bitwise* operations where individual bits of a word are manipulated.

Some of this section will discuss the traditional design presented by this figure but then replace it with a more modern design. From earlier in this chapter, we know that blooming is performed by calculating one or more hash keys and updating the value of the filter by OR-ing each hash key with its current state. This is referred to as the insert operation. The lookup operation is done by taking the bitwise operation AND between a given hash key and current state of the filter. The decision making from this point on can go in one of the following two directions:

- The result of AND is the same as the value of the hash key—this is either true positive (TP) or false positive (FP), with no way to tell between the two.
- The result of AND is not the same as the value of the hash key—this is a 100% reliable true negative.

One common way to describe this lookup behavior of Bloom filters is to describe the filter as a person with memory who can only answer the question “Have you seen this item before?” reliably [11]. This is not to underestimate the utility of the filter, as the answer to this exact question is precisely what is needed in many practical situations.

Let us look at the Bloom filter design from the viewpoint of hashing, especially given that the state of the filter is gradually built by adding more hash keys onto its state.

Let us put n as the number of items and m as the bit length of hash keys and, therefore, the filter. We know from before that each bit in the hash key can be set to 1 with 50% probability. Therefore, omitting details, the optimal number of hash function can be calculated as

$k = \ln 2 \frac{m}{n} \approx 0.6 \frac{m}{n}$

If each hash function is perfectly independent of all others, then the probability of a bit remaining 0 after n elements is

$p = 1 - \left(1 - \frac{1}{m}\right)^{kn} \approx e^{-\frac{kn}{m}}$.

The FP—an important performance metric of a Bloom filter—is then

$p_{FP} = (1 - p)^{k} \approx \left(1 - e^{-\frac{kn}{m}}\right)^{k} \approx \frac{1}{2^{k}}$, for the optimal k. Note that with increasing k, the probability of an FP actually is supposed to decrease, which is an unintuitive outcome because one would expect the filter to get filled up with keys earlier.

Let us analyze k. For the majority of cases, m ≪ n, which means that the optimal number of hash functions is 1. Two functions are feasible only with m > 2.5n. In most realistic cases, this is almost never so, because n is normally huge, while m is something practical like 24 or 32 (bits).

### 12.5.2 Unconventional Bloom Filter Designs for Data Streams

Based on Section 12.5.1, the obvious problem in Bloom filters is how to improve their flexibility. As a side note, such Bloom filters are normally referred to as dynamic.

Figure 12.3 shows the generic model, which applies to most of the proposals of dynamic Bloom filters. The simple idea is to replace a simple bit string with a richer data structure (the change in the Bloom filter in the figure). Each bit in the filter now simply is a pointer to a structure that supports dynamic operations.

The other change that ensues is that the OR operation is no longer applicable. Instead, a nontrivial manipulation has to be performed on each bit of the value that was supposed to be OR-ed in the traditional design. Naturally, this incurs a considerable overhead on performance.

The following classes of dynamic Bloom filters are found in the literature.

- Stop additions filter. This filter will stop accepting new keys beyond a given point. Obviously, this is done in order to keep the FP beyond a given target value.
- Deletion filter. This filter is tricky to build, but if accomplished, it can revert to a given previous state by forgetting the change introduced by a given key.
- Counting filter. This filter can count both individual bits of potential occurrences and entire values—combinations of bits. This particular class of filters obviously can find practical applications in data streaming. In fact, the existing example of the d-left hashing method in Reference 32 uses a kind of counting Bloom filter [33]. Another example can be found in Reference 34, where it is used roughly for the same purpose.

![](img/1643181e79c76dc765d55a7355afb4a4_263_0.png)

FIGURE 12.3 A generic model representing Bloom filters with dynamic functionality. The two main changes are (1) extended design of the Bloom filter structure itself, which is not a bit string anymore, and (2) nontrivial manipulation logic dictated by the first change—simply put, one cannot simply use logical ORs between hashes and Bloom filter states.

![](img/1643181e79c76dc765d55a7355afb4a4_265_0.png)

## FIGURE 12.4 Common components shared by all data streaming applications.

definition, cannot be higher than the arrival rate. On the other hand, arrival rate is important because a data streaming method has to be able to support a given rate of arrival in order to be feasible in practice.

Arrival rate is also the least popular topic in related research. In fact, per-unit processing time is not discussed much in literature, which instead focuses on efficient hashing or blooming methods [30,32,47,48]. Earlier work by this author in Reference 49 shows that per-unit processing cost is important—the study specifically shows that too much processing can have a major impact on throughput.

The topic of arrival rate is especially important in packet traffic [28,29,50]. With constantly increasing transmission rates as well as traffic volume, a higher level of efficiency is demanded of switching equipment. A Click router is one such technology [51], which is in the active development phase with recent achievements of billion packets per second (pps) processing rates [52]. The same objectives are pursued by Open vSwitch—a technology in network virtualization. It is interesting that research in this area uses roughly the same terminology as is found in data streaming. For example, References 52 and 53 talks about space efficiency of data structures used to support per-packet decision making. Such research often uses Bloom filters to improve search and lookup efficiency [13,32]. In general, this author predicts with high probability that high-rate packet processing research in the near future will discover the topic of data streaming and will greatly benefit from the discovery [50].

### 12.6.2 Streaming on Multicore

A method that packs n sketches into m cores is a well-known bin packing problem. The method presented in this section performs one (blind) initial packing but also repacks every time there is a change in state. Given that each sketch has start and end times that can differ from those of the replayed Big Data, changes in state can be frequent. With convergence speed in mind, this section and Section 12.7 discuss a simple packing heuristic. Given that all sketches on all cores share one time-ordered stream of items, the main objective of the heuristic is to minimize variance in processing cursors (current position in stream) across sketches. Intuitively, if all sketches with heavy-duty processing are packed into one core and all light-duty ones are packed into another, the replay will move at a greatly diminished speed. The new heuristic aspires to avoid such situations, while the design itself facilitates parallel processing without cores passing messages or competing for memory locks.
