# 7.5.1 Operations on a Deque

Four operations can be performed on deque. They are

+   - PUSH-DEQ(ITEM) inserts ITEM at front end of Deque.
+   - POP-DEQ() deletes item at front of Deque.
+   - INSERT-DEQ(ITEM) inserts ITEM at REAR end of Deque.
+   - DELETE-DEQ() deletes ITEM from REAR end of Deque.

The algorithm for POP-DEQ() and INSERT-DEQ(ITEM) operations are same as DELETE-CQ() and INSERT-CQ(), respectively.

Consider DEQ[1..N] as a deque represented as circular array of size N. The following are the algorithms for insertion at the front end and deletion at the rear end.

# Algorithm 7.7: PUSH-DEQ(DEQ,FRONT,REAR,ITEM)

+   //Check whether FRONT is at left extreme
+   1. IF(FRONT=1) then
+   2. Set Temp=N
+   3. Else //check whether FRONT is at extreme right or deque empty
+   4. If(FRONT=N) OR (FRONT=0) then
+   5. Set Temp=1
+   6. Else
+   7. Set Temp=FRONT-1 //FRONT at middle position
+   8. If(Temp=REAR) then
+   9. Write "deque is full"
+   10. Else
+   11. FRONT=Temp
+   12. DEQ[FRONT]=ITEM
+   13. END.

# Algorithm 7.8: DELETE-DEQ(DEQ,FRONT,REAR,ITEM)

The element is deleted from the rear end and is assigned to ITEM

+   1. If (FRONT=0) then
+   2. Write "deque is empty"
+   3. Else
+   4. If(FRONT=REAR) then //DEQ contains right element
+   5. Set ITEM=DEQ(REAR)
+   6. Set FRONT=REAR=0 //Deque becomes empty
+   7. Else
+   8. If(REAR=1)then //check whether REAR is at extreme left
+   9. Set ITEM=DEQ[REAR]
+   10. Set REAR=N
+   11. Else
+   12. If(REAR=N)then //check for REAR at extreme right
+   13. Set ITEM=DEQ[REAR]
+   14. Set REAR=1 //REAR at middle position