![](bbox=[0.176, 0.078, 0.558, 0.319])

Process A Page Directory        Process A Page Tables

**FIGURE 5-40** Page file reservation cluster.

Once the page cluster is computed, free page space must be located to be reserved for this cluster of pages. Page file allocations are managed by a bitmap (where each set bit indicates a used page in the file). For page file reservation, a second bitmap is used that indicates pages that have been reserved (but not necessarily written to yet—this is the job of the page file allocation bitmap). Once page file space is not reserved and not allocated (based on these), the relevant bits are set in the reservation bitmap only. It is the job of the modified page writer to set these bits in the bitmap when it writes the contents of the pages to disk. If not enough page space could be found for the required cluster size, page file expansion is attempted, and if that already happened (or the maximum page file size is the expanded size), then the cluster is reduced to fit in the reservation size that was located.

> Note The clustered pages (except the starting PTE) are not linked to any of the physical page lists. The reservation information is placed in the Original PTE of the PFN.

The modified page writer handles writing pages that have reservations as a special case. It uses all the gathered information described previously to build an MDL that contains the correct PFNs for the cluster that is used as part of writing to the page file. Building the cluster includes finding contiguous pages that can span reservation clusters. If there are “holes” between clusters, a dummy page is added in between (a page that contains all bytes with 0xFF value). If the dummy page count is above 32, the cluster is broken. This “walk” is done going forward and then backward to build the final cluster to write. Figure 5-41 shows an example of the state of pages after a cluster has been built by the modified page writer.

CHAPTER 5 Memory management 445