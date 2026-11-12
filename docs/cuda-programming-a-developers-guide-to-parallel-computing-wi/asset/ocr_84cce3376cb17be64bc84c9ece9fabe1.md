As you can see, the calculated thread, or the thread ID, goes from 0 to 127. Within that you allocate two blocks of 64 threads each. The thread indexes within each of these blocks goes from 0 to 63. You also see that each block generates two warps.

# # GRIDS

A grid is simply a set of blocks where you have an X and a Y axis, in effect a 2D mapping. The final Y mapping gives you Y × X × T possibilities for a thread index. Let’s look at this using an example, but limiting the Y axis to a single row to start off with.

If you were to look at a typical HD image, you have a 1920 × 1080 resolution. The number of threads in a block should _always_ be a multiple of the warp size, which is currently defined as 32. As you can only schedule a full warp on the hardware, if you don’t do this, then the remaining part of the warp goes unused and you have to introduce a condition to ensure you don’t process elements off the end of the X axis. This, as you’ll see later, slows everything down.

To avoid poor memory coalescing, you should always try to arrange the memory and thread usage so they match. This will be covered in more detail in the next chapter on memory. Failure to do so will result in something in the order of a five times drop in performance.

To avoid tiny blocks, as they don’t make full use of the hardware, we’ll pick 192 threads per block. In most cases, this is the _minimum_ number of threads you should think about using. This gives you exactly 10 blocks across each row of the image, which is an easy number to work with (Figure 5.9). Using a thread size that is a multiple of the X axis and the warp size makes life a lot easier.

Along the top on the X axis, you have the thread index. The row index forms the Y axis. The height of the row is exactly one pixel. As you have 1080 rows of 10 blocks, you have in total 1080 × 10 = 10,800 blocks. As each block has 192 threads, you are scheduling just over two million threads, one for each pixel.

This particular block is useful where you have just one operation on a single pixel or data point, _or_ where you have some operation on a number of data points in the _same_ row. On the Fermi hardware, at eight blocks per SM, you’d need a total of 1350 SMs (10,800 total blocks ÷ 8 scheduled blocks) to run out of parallelism at the application level. On the Fermi hardware currently available, you have only 16 SMs (GTX580), so each SM would be given 675 blocks to process.

This is all very well, but what if your data is not row based? As with arrays, you are not limited to a single dimension. You can have a 2D thread block arrangement. A lot of image algorithms, for

| | 0 | 192 | 384 | 576 | 768 | 960 | 1152 | 1344 | 1536 | 1728 | 1920 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Row 0 | Block 0 | Block 1 | Block 2 | Block 3 | Block 4 | Block 5 | Block 6 | Block 7 | Block 8 | Block 9 | |
| Row 1 | Block 10 | Block 11 | Block 12 | Block 13 | Block 14 | Block 15 | Block 16 | Block 17 | Block 18 | Block 19 | |
| Row 2 | Block 20 | Block 21 | Block 22 | Block 23 | Block 24 | Block 25 | Block 26 | Block 27 | Block 28 | Block 29 | |
| Row ... | | | | | | | | | | | |
| Row 1079 | Block 10,790 | Block 10,791 | Block 10,792 | Block 10,793 | Block 10,794 | Block 10,795 | Block 10,796 | Block 10,797 | Block 10,798 | Block 10,799 | |

**FIGURE 5.9**
Block allocation to rows.