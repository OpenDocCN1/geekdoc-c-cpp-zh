# ### 5.3 Transmission Schedule

We use the successive partitioning scheme developed in the previous section to design the transmission schedule of an arbitrary node in an ad hoc network. Consider a node with identification number *my_id*; the node knows only its own identification number *n* (total number of nodes in the network) and Δ, the maximum node degree of the network. Given Δ, we compute *h* such that 2^h ≤ Δ < 2^(h + 1). The node then computes the blocks up to the level *h* partitioning, P(*h*, *k*), 0 ≤ *k* ≤ r^h · m!/(m−h)! − 1. The details of the pseudo-code for the protocol to be used at each node to compute its own transmission slot or round are given in the algorithm below. The *find_my_slots* and *compute_slot* procedures needed for this purpose are also given below.

```
/* code to be executed by each node having my_id as identifier */

h = ⌊log₂ Δ⌋;
max_slot_number ← r^h × m × (m − 1) × ··· × (m − h + 1) − 1;
find_my_slots(my_id, n, Δ);
for phase_number = 1 to D − 1 do
    for i = 0 to max_slot_number do
        if T(i) = 1 then
            transmit the message;
        end if
    end for
end for
```

```
procedure find_my_slots(my_id, n, Δ);
begin;
    h = ⌊log₂ Δ⌋;
    offset ← 0;
    Flag ← 0;
    T ← 0;
    find_partition(my_id, 1, h, offset, Flag);
    compute_slot(Flag, h, T);
end procedure;
```