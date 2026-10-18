the value of *scanned_bit_position* by 1, and look for *S*, *C* and *N* signals. Increment *round_count* by 1 and go back to Step 4 for the next round.

**Step 4.4:** If an acknowledgment was received only in the slot *S* but not in *C* and *N*, the state of the node is changed back to *active*, i.e., the transmission was successful. Increment *round_count* by 1 and go back to Step 3 for the next round.

**Step 5:** (*receive* state actions) If node state is *receive*, execute Steps 5.1 to 5.4.

**Step 5.1:** If a signal is received in *test* slot, send *ack1* in this round. If signal received in *ack2* slot, send *ack3* signal in this round. Increment *round_count* by 1 and go back to Step 5 for the next round.

**Step 5.2:** If clean *M* is received, send an acknowledgment in *S* slot and change state to *active*. Increment *round_count* by 1 and go back to Step 3 for the next round.

**Step 5.3:** If collision occurs in *message* slot, send acknowledgment in *C* slot and change state to *collision*. Increment *round_count* by 1 and go to Step 6 for the next round.

**Step 6:** (*Collision* state actions) If node state is *collision*, execute Steps 6.1 to 6.5.

**Step 6.1:** If a signal is received in *test* slot or *ack1* slot, send the *ack2* signal in this round. Increment *round_count* by 1 and go back to Step 6 for the next round.

**Step 6.2:** If a collision is encountered in the *message* slot, send an acknowledgment in *C* slot. Increment *round_count* by 1 and go back to Step 6 for the next round.