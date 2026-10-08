The 32-bit word is used as two numeric fields (one of 22 bits and one of 3 bits) and four flags (1 bit each). The sizes and positions of these pieces of data are fixed. There is even an unused (and unnamed) “field” in the middle. We can express this as a **struct**:

```
```
struct PPN {
unsigned int PFN : 22;   // R6000 Physical Page Number
int : 3;                 // unused
unsigned int CCA : 3;    // Cache Coherency Algorithm
bool nonreachable : 1;
bool dirty : 1;
bool valid : 1;
bool global : 1;
};
```
```

We had to read the manual to see that **PFN** and **CCA** should be interpreted as unsigned integers, but otherwise we could write out that **struct** directly from the diagram. Bitfields fill a word left to right. You give the number of bits as an integer value after a colon. You can’t specify an absolute position (e.g., bit 8). If you “consume” more bits with bitfields than a word can hold, the fields that don’t fit are put into the next word. Hopefully, that’s what you want. Once defined, a bitfield is used exactly like other variables:

```
```
void part_of_VM_system(PPN *p)
{
// ...
if (p->dirty) {  // contents changed
// copy to disk
p->dirty = 0;
}
// ...
}
```
```

Bitfields primarily save you the bother of shifting and masking to get to information placed in the middle of a word. For example, given a **PPN** called *pn* we could extract **CCA** like this:

```
```
unsigned int x = pn.CCA;  // extract CCA
```
```

Had we used an **int** called *pni* to represent the same bits, we could instead have written

```
```
unsigned int y = (pni>>4)&0x7;  // extract CCA
```
```