For each cell, a mobile terminal is also elected as the *cell leader* to handle mobility of mobile terminals, joining of new mobile terminals and MTs leaving the cell or network. For simplicity, we arbitrarily assume the lowest id MT in a cell to be the cell leader. An advantage of such a leader election protocol is that no additional communication is required among the MTs to elect the cell leader. The cell leader must:

+   - Compute the slot demand of the cell.
+   - Control admission of new mobile terminals into the network.
+   - Handle handoff situations and MTs leaving the network.
+   - Communicate to the *network leader* the demand of the cell and request a recomputation of the allocated slots whenever necessary.

To handle mobility of the mobile terminals, each cell keeps a few slots for transmitting control messages and some unused slots for handling new MTs joining the network and handoff scenarios. In general, a cell *i* computes its demand *wᵢ* as the sum of the number of mobile terminals in the cell, the number of slots allocated for control messages and an additional few unused slots. We assume the number of unused slots to be some fraction *f* of the number of mobile terminals currently in the cell. If *mᵢ* is the number of MTs currently in cell *i* and *c* slots are used for control purposes, then the demand, *wᵢ*, of cell *i* is, *wᵢ = mᵢ + c + max(1, ⌈fmᵢ⌉), 0 ≤ f ≤ 1*.

# 5.4.6.1  Algorithm COSA

The steps of the algorithm are:

+   **Step 1:** Elect an MT as the *network leader* through some leader election protocol [10, 11] and call it *L*.