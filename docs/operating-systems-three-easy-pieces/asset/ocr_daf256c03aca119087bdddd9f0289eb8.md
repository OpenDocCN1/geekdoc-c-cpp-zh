# 268 BEYOND PHYSICAL MEMORY: POLICIES

Unfortunately, as the number of pages in a system grows, scanning a huge array of times just to find the absolute last-recently-used page is prohibitively expensive. Imagine a modern machine with 4GB of memory, chopped into 4KB pages. This machine has 1 million pages, and finding the LRU page will take a long time, even at modern CPU speeds. Which begs the question: do we really need to find the absolute oldest to replace? Can we instead survive with an approximation?

CRUX: HOW TO IMPLEMENT AN LRU REPLACEMENT POLICY\ Given that it will be expensive to implement perfect LRU, can we approximate it in some way, and still obtain the desired behavior?

# 22.8 Approximating LRU

As it turns out, the answer is yes: approximating LRU is more feasible from a computational-overhead standpoint, and it is what many modern systems do. The idea requires some hardware, in the form of a use bit (sometimes called the reference bit), the first of which was implemented in the first system with paging, the Atlas one-level store [KE+62]. There is one bit per page of the system, and the use bits in memory somewhere (they could be in hardware, per-process page tables, for example, or just in an array somewhere). Whenever a page is referenced (i.e., read or write), the use bit is set by hardware to 1. The hardware never clears the bit, though (i.e., sets it to 0); that is the responsibility of the OS.

How does the OS use the bit to approximate LRU? Well, there could be a lot of ways, but with the clock algorithm [C69], one simple approach was suggested. Imagine all the pages of the system arranged in a circular list. A clock hand points to some page to begin with (it doesn't really matter). When a replacement must occur, the OS checks if the currently-pointed page P has a bit of 0 or 1. If it is, this implies that P was recently used and then is not a good candidate for replacement. We use the bit for P to set 0 (cleared), and the clock hand is incremented to the next page (P+1). The algorithm continues until it finds a bit that is set to 0, implying this page has not been recently used (or, in the worst, searched the entire set of pages, clearing all bits).

Note that this approach is not the only way to employ a use bit to approximate LRU. Indeed, any approach which periodically clears the bit and then differentiates between which pages use bits of 1 versus 0 to decide which to replace would be fine. The clock algorithm of Corbato was just one early approach which met with some success, and had the property of not repeatedly scanning through all of memory looking for an unused page.

OPERATING SYSTEMSn[Version 1.01]

WWW.OSTEP.ORG