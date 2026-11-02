
are $v_a$ and $v_b$, and the end vertex is $v_k$. The in-degree of vertex $v_a$ is 1, and the out-degree of vertex $v_j$ is 2.

#### Definition 2

A *subgraph* $sub$-$G$ of the data stream graph $G$ is a subgraph consisting of a subset of the vertices with the edges in between. For vertices $v_i$ and $v_j$ in the subgraph $sub$-$G$ and any vertex $v$ in the data stream graph $G$, $v$ must also be in the $sub$-$G$ if $v$ is on a directed path from $v_i$ to $v_j$, that is, $\forall v_i, v_j \in V(sub\text{-}G), \forall v \in V(G)$, and if $v \in V(p(v_i, v_j))$, then $v \in V(p(sub\text{-}G))$.

A subgraph $sub$-$G$ is logically equivalent and can be substituted by a vertex. But reducing that subgraph to a single logical vertex would create a graph with a cycle, not a DAG.

#### Definition 3

A *path* $p(v_u, v_v)$ from vertex $v_u$ to vertex $v_v$ is a subset of $E(p(v_u, v_v))$, which should meet the conditions $\exists e_k \in p(v_u, v_v)$ and $\exists e_j \in p(v_u, v_v)$ for any directed edge $e_{i,j}$ in path $p(v_u, v_v)$ that displays the following properties: If $k \neq i$, then $\exists m$, and $e_{m,k} \in p(v_u, v_v)$; if $i \neq j$, then $\exists m$, and $e_{i,m} \in p(v_u, v_v)$.

The latency $l_p(v_u, v_v)$ of a path from vertex $v_u$ to vertex $v_v$ is the sum of latencies of both vertices and edges on the path, as given by Equation 11.1:

$l_p(v_u, v_v) = \sum_{v_i \in V(p(v_u, v_v))} c_{v_i} + \sum_{e_{i,j} \in E(p(v_u, v_v))} c_{e_{i,j}},\quad c_{v_i}, c_{v_j}, c_{e_{i,j}} \ge 0. \tag{11.1}$

A critical path, also called the longest path, is a path with the longest latency from a source vertex $v_s$ to an end vertex $v_e$ in a data stream graph $G$, which is also the latency of data stream graph $G$.

If there are $m$ paths from source vertex $v_s$ to end vertex $v_e$ in data stream graph $G$, then the latency $l(G)$ of data stream graph $G$ is given by Equation 11.2:

$l(G) = \max\{ l_{p1}(v_s, v_e), l_{p2}(v_s, v_e), \dots, l_{pm}(v_s, v_e) \}. \tag{11.2}$

where $l_{p_i}(v_s, v_e)$ is the latency of the $i$-th path from vertex $v_s$ to vertex $v_e$.

#### Definition 4

In data stream graph $G$, if $\exists e_{i,j}$ from vertex $v_i$ to vertex $v_j$, then vertex $v_i$ is a *parent* of vertex $v_j$, and vertex $v_j$ is a *child* of vertex $v_i$.

#### Definition 5

The throughput $t(v_i)$ of vertex $v_i$ is the average rate of successful data stream computing in a Big Data environment and is usually measured in bits per second (bps).

We identify the source vertex $v_s$ as in the first level, the children of source vertex $v_s$ as in the second level, and so on, and the end vertex $v_e$ as in the last level.

The throughput $t(level_i)$ of the $i$th level can be calculated by Equation 11.3:

$$t(level_i)=\sum_{k=1}^{n_i} t(v_k), \tag{11.3}$$

where $n_i$ is the number of vertices in the $i$th level.

If data stream graph $G$ has $m$ levels, then the throughput $t(G)$ of the data stream graph $G$ is the minimum throughput of all the throughput in the $m$ levels, as described by Equation 11.4:

$$t(G)=\min\{t(level_1), t(level_2),...,t(level_m)\}, \tag{11.4}$$

where $t(level_i)$ is the throughput of the $i$th level in data stream graph $G$.

#### Definition 6

A topological sort $TS(G)=(v_{s_1},v_{s_2},...,v_{s_n})$ of the vertices $V(G)$ in data stream graph $G$ is a linear ordering of its vertices, such that for every directed edge $e_{s_i,s_j}$ $(e_{s_i,s_j}\in E(G))$ from vertex $v_{s_i}$ to vertex $v_{s_j}$, $v_{s_i}$ comes before $v_{s_j}$ in the topological ordering.

A topological sort is possible if and only if the graph has no directed cycle, that is, it needs to be a directed acyclic graph. Any directed acyclic graph has at least one topological sort.

#### Definition 7

A graph partitioning $GP(G)=\{GP_1, GP_2,...,GP_m\}$ of the data stream graph $G$ is a topological sort-based split of the vertex set $V(G)$ and the corresponding directed edges. A graph partitioning should meet the nonoverlapping and covering properties, that is, if $\forall i \neq j, i,j \in [1,m]$, then $GP_i \cap GP_j = \varnothing$, and $\bigcup_{i=1}^{m} GP_i = V(G)$.

### 11.2.2 System Architecture for Stream Computing

In BDSC environments, stream computing is the model of straight-through computing. As shown in Figure 11.2, the input data stream is in a real-time data stream form, all

![](img/1643181e79c76dc765d55a7355afb4a4_236_0.png)

FIGURE 11.4 Master-slave structure.

has a special function, and it always receives a data stream from the master node, processes the data stream, and sends the results to the master node. Usually, the master node is the bottleneck in the master–slave structure system. If it fails, the whole system will not work.

#### 11.2.3.2 Data Stream Transmission

Push and pull are two main data stream transmissions in a BDSC system.

In a push system, once an upstream node gets a result, it will immediately push the result data to downstream nodes. When this is done, the upstream data will be immediately sent to downstream nodes. However, if some downstream nodes are busy or fail, some data will be discarded.

In a pull system, a downstream node requests data from an upstream node. If some data need to be further processed, the upstream node will send the data to the requesting downstream node. When this is done, the upstream data will be stored in upstream nodes until corresponding downstream nodes make a request. Some data will wait a long time for further processing and may lose their timeliness.

#### 11.2.3.3 Application Interfaces

An application interface is used to design a data stream graph, a bridge between a user and a BDSC system. Usually, a good application interface is flexible and efficient for users. Currently, most BDSC systems provide MapReduce-like interfaces; for example, the Storm system provides spouts and bolts as application interfaces, and a user can design a data stream graph using spouts and bolts. Some other BDSC systems provide structured query language (SQL)-like interfaces and graphical user interfaces.

#### 11.2.3.4 High Availability

State backup and recovery is the main method to achieve high availability in a BDSC system. There are three main high-availability strategies, that is, passive standby strategy, active standby strategy, and upstream backup strategy.

In the passive standby strategy (see Figure 11.5), each primary node periodically sends checkpoint data to a backup node. If the primary node fails, the backup node takes over from the last checkpoint. Usually, this strategy will achieve precise recovery.

## 11.3 EXAMPLE BDSC SYSTEMS

In this section, the system architecture and key technologies of four popular BDSC system instances are presented. These systems are Twitter Storm, Yahoo! S4, Microsoft TimeStream, and Microsoft Naiad, which are specially designed for BDSC.

### 11.3.1 Twitter Storm

Storm is an open-source and distributed BDSC system licensed under the Eclipse Public License. Similar to how Hadoop provides a set of general primitives for doing batch processing, Storm provides a set of general primitives for doing real-time Big Data computing. The Storm platform has the features of simplicity, scalability, fault tolerance, and so on. It can be used with any programming language and is easy to set up and operate [1,20,21].

#### 11.3.1.1 Task Topology

In BDSC environments, the logic for an application is packaged in the form of a task topology. Once a task topology is designed and submitted to a system, it will run forever until the user kills it.

A task topology can be described as a directed acyclic graph and comprises spouts and bolts, as shown in Figure 11.9. A spout is a source of streams in a task topology and will read data streams (in tuples) from an external source and emit them into bolts. Spouts can emit more than one data stream. The processing of a data stream in a task topology is done in bolts. Anything can be done by bolts, such as filtering, aggregations, joins, and so on. Some simple functions can be achieved by a bolt, while complex functions will be achieved by many bolts. The logic should be designed by a user. For example, transforming a stream of tweets into a stream of trending images requires at least two steps: a bolt to do a rolling count of retweets for each image and one or more bolts to stream out the top *n* images. Bolts can also emit more than one stream. Each edge in the directed acyclic graph represents a bolt subscribing to the output stream of some other spout or bolt.

A data stream is an unbounded sequence of tuples that is processed and created in parallel in a distributed BDSC environment. A task topology processes data streams in many complex ways. Repartitioning the streams between each stage of the computation is needed. Task topologies are inherently parallel and run across a cluster of machines. Any

![](img/1643181e79c76dc765d55a7355afb4a4_238_0.png)

FIGURE 11.9 Task topology of Storm.
