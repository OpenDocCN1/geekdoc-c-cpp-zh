# _Wireless Networks and Mobile Computing_

+   2: /\* First receive an RBNS data frame of length len + 1 *\/
+   3: /\* Then converted it to its equivalent binary value *\/
+   4: RBN vector recv_buf : array [0..len]; \(\triangleright\) received RBNS data frame
+   5: bit vector out_buf : array [0..len]; \(\triangleright\) Output binary frame
+   6: /\* Receive the data frame *\/
+   7: Call ReceiveRBNDataFrame(recv_buf, len);
+   8: Call ConvertRBNtoBinary(recvbuf, len, out_buf);
+   9:
+   10: /\* The binary data in out_buf is len + 1 bits. The msb *\/
+   11: /\* can be ignored as it will always be 0, and only the *\/
+   12: /\* lower order len bits needs to be returned *\/
+   13: end procedure

+   1: procedure RECEIVERBNDATAFRAME(INOUT recv_buf, IN len)
+   2: /\* null indicated no signal in channel *\/
+   3: /\* time_slot[i] refers to the ith time slot *\/
+   4: for i = 0 to len do
+   5: if time_slot[i] = null then
+   6: recv_buf[i] ← 0; \(\triangleright\) channel status null during ith time slot
+   7: else
+   8: recv_buf[i] ← time_slot[i]; \(\triangleright\) received 1 or 1 in ith time slot
+   9: end if
+   10: end for
+   11: end procedure

+   1: procedure CONVERTRBNTOBINARY(IN recv_buf, IN len, INOUT out_buf)