3) Delete the node A and edges going from A
QUEUE : C,G front = 2 Rear = 3 SORT : A
4) Now the indegree of nodes will be
B=2, D=1, E=3, F=2

# STEP-3:

1) Delete the node C and edges going from C
QUEUE :G front = 3 Rear = 3 SORT :A,C
2) Now the indegree of nodes will be
B=1, D=0, E=3, F=2

# STEP-4:

1) Add the node D to the Queue
QUEUE : G,D front = 3, rear = 4 SORT : A,C
2) Delete the node G and edges going from G
QUEUE :D front = 4 Rear = 4 SORT :A,C,G
3) Now the indegree of nodes will be
B=1, E=2, F=1

# STEP-5:

1) Delete the node D and edges going from D
QUEUE : front = 0 Rear = 0 SORT :A,C,G,D
2) Now the indegree of nodes will be
B=0, E=1, F=1

# STEP-6:

1) Add the node B to the Queue
QUEUE : B front = 1, rear = 1 SORT : A,C,G,D
2) Delete the node B and edges going from B
QUEUE : front = 0 Rear = 0 SORT :A,C,G,D,B
3) Now the indegree of nodes will be
E=0, F=0

# STEP-7:

1) Add the node E,F to the Queue
QUEUE : E,F front = 1, rear = 2 SORT : A,C,G,D,B
2) Delete the node E and edges going from E
QUEUE :F front = 2 Rear = 2 SORT :A,C,G,D,B,E