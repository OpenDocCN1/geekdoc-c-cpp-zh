similarity score. Hence, the broker has to add these partial similarity scores that are related to each object and then sort the objects based on the summed similarity score.

# Algorithm 4: Reference-Based Approach: Searching

+   IN: Data structure DS, references R and query: q
+   OUT: Output list OL
+   1. if(broker):
+   2. Create the query partial ordered list \tilde{L}(q,R).
+   3. Notify the active processes: r_j \in \tilde{L}(q,R) and r_j \in R_p
+   4. Send \tilde{L}(q,R)_p to the active processes p
+   5. if(active):
+   6. Recv. \tilde{L}(q,R)
+   7. For r_j \in L(q,R) and r_j \in R_p
+   8.     OL_p = search in DS_p
+   9. Send OL_p to the broker
+   10. if(broker):
+   11. For p \in P
+   12.     Recv(OL_p).
+   13. Create OL and send the results to the user.

# 1.4.3 Index Based

# 1.4.3.1 Indexing

Similar to the previous techniques, the data domain is divided into P subdomains D1...Dp. It can be divided randomly or based on a clustering algorithm. The references are selected independently from each subdomain and not shared with the other processes Rp. Once the references are defined for each portion, the processes create the partial ordered lists \tilde{L}(o_j,R_p) for their own local objects Dp based on their local reference sets Rp. Hence, with the approach, the processes do not need to communicate to each other while indexing. The indexing complexity is reduced to O \frac{N \cdot n + nlog \frac{n}{P}}{P^2}. The main reason for this reduction is the division of the references between all the processes.

# 1.4.3.2 Searching

Algorithm 5 shows the searching process. The broker process has information about all the references R = {R1 \cup R2 \cup...\cup Rp}. Hence, once a query q is submitted, the partial ordered list \tilde{L}(q,R) is created using the full reference list. If the query is located within a certain data domain Dp, the reference points that were selected from that data domain Rp are located as the closest references to the query. Hence, the searching is only done through the process that is responsible for the corresponding data domain (lines 1-4). If the query is located between two or more data domains, the closest references are shared among these