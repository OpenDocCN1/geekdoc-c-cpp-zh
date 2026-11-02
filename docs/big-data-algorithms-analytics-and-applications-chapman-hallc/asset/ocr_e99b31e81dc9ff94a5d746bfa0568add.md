different domains. Formally, a process p is an active process if there exists r_i ∈ R_p, such that r_i ∈ L̂(q,R). After searching, the results from each process cannot be sent to the broker directly. The similarity between the query and each object for each process is defined by different sets of reference points R_p that are not related to each other. To combine and rank them, each process computes the distances between the submitted query and the K_p = Δ × k first objects in the candidate list of each process. We call Δ ≥ 1 the DDC factor. Then, this distance information with the related object IDs is sent to the broker process (lines 5–10). Finally, the broker ranks these objects based on their distances and sends the results back to the user. For example, if Δ = 2, for K-NN query(q,30), each process returns the most similar k = 30 objects to the query. Each process searches within its local data structure and gets the top set candidate list K_p = 2×30 = 60. Then, a DDC is performed between the query and this top K_p = 60 by each process. If the references of the query ordered list are located within the sets of 3 processes, the broker receives 3 × 60 = 180 distances. These 180 distances are sorted, and the top 30 objects are sent back to the user.

# Algorithm 5: Index-Based Approach: Searching

```
IN: Data structure DS, references R, and query q
OUT: Output list OL
1. if (broker):
2.   Create the query partial ordered list L̂(q,R).
3.   Notify the active processes.
4.   Send q to the active processes.
5. if (active):
6.   Recv q and create L̂(q,R_p).
7.   For r_i ∈ L̂(q,R_p),
8.     OL_p = search in DS_p,
9.     d_p = calculate_distance(q, 2k, OL_p).
10.  Send the distances d_p to the broker.
```

# 1.5 EVALUATION

Large-scale experiments were conducted to evaluate the efficiency and the scalability of the three approaches in terms of recall (RE), position error (PE), indexing time, and searching time. The three approaches were implemented using message passing interface (MPI) [30]. The results section is divided into three subsections.

In Section 1.5.1, we measure the average RE and PE for the three distributed approaches. The experiments were performed using a data set consisting of 5 million objects. The data set is composed of visual shape features (21 dimensional) and was extracted from the 12-million ImageNet corpus [31]. Three sets of references of sizes 1000, 2000, and 3000 are selected randomly from the data set. The average RE and PE are based on 250 different queries, which are selected randomly from the data set.