# 7.5 Atomic Operation and Memory Model CHAPTER 07 PARALLELISM AND CONCURRENCY

x.store(1) x.store(3) x.load()
T1 ----------+-------+-----------+----->

T2 -------------------------------------
x.store(2)

Under order consistency requirement, x.load() must read the last written data, so x.store(2) and x.store(1) do not have any guarantees, as x.store(2) of T2 occurs before x.store(3).

3. Causal consistency: its requirements are further reduced, so only the sequence of causal operations is guaranteed, and the order of non-causal operations is not required.

a = 1 b = 2
T1 ----------+----------------->

T2 -------------------------------------
x.store(3) c = a + b y.load()

or
a = 1 b = 2
T1 ----------+--------------------

T2 ----------+---------------------
x.store(3) y.load() c = a + b

or
b = 2 a = 1
T1 ----------+--------------------

T2 -------------------------------------
y.load() c = a + b x.store(3)

The three examples given above are all causal consistent, because in the whole process, only c has a dependency on a and b, and x and y are not related in this example. (But in actual situations we need more detailed information to determine that x is not related to y)