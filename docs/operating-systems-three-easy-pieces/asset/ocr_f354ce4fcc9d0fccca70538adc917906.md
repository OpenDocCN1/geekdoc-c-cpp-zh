# FILE SYSTEM IMPLEMENTATION

# 525

# TIP: CONSIDER EXTENT-BASED APPROACHES

A different approach is to use extents instead of pointers. An extent is simply a disk pointer plus a length (in blocks); thus, instead of requiring a pointer for every block of a file, all one needs a pointer and a length to specify the on-disk location of a file. Just a single extent is limiting, one might have trouble finding a contiguous chunk of on-disk free space when allocating a file. Thus, extent-based systems often offer for more than one extent, giving more freedom to the file system during file allocation.

In comparing the two approaches, pointer-based approaches are the most flexible but use a large amount of metadata per file (particularly for large files). Extent-based approaches are less flexible but more compact; particular, they work well when there is enough free space on the disk and files can be laid out contiguously (which is the goal for virtually any file allocation policy).

Not surprisingly, in such an approach, you might want to support larger files. To do so, add another pointer to the inode: the **double indirect pointer**. This pointer refers to a block that contains pointers each of which contains pointers to data blocks. A double indirect block thus adds the possibility to grow files with additional 1024 · 1024 or 1-million 4KB blocks, in other words supplying files that are over 4GB in size. You may want even more, and we bet you know where this is headed: the **triple indirect pointer**.

Overall, this imbalanced tree is referred to as the **multi-level index approach** pointing to files. Let's examine an example with twelve direct pointers, as well as a single and a double indirect block. As summing a block size of 4 KB, this structure can accommodate a file of over 4 GB in size (i.e., $12 + 1024 + 1024^2 	imes 4$ KB). You can figure out how big of a file can be handled with the handle of a triple-indirect block (hint: pretty big)

Many file systems use a level-index approach, including commonly-used file systems like Linux ext2 [9] and ext3, NetApp's WAAF, as well as the original Unix file system. Other file systems, including SGI XPS and Linux ext4, use extents instead of simple pointers; the earlier aside on how extent-based schemes work (which are akin to segments in the discussion of virtual memory).

You might be wondering: why use an imbalanced tree this? Why not a different approach? Well, as it turns out, many researchers have studied file systems and how they are used, and virtually every time they find "truths" that hold across the decades. One finding is that *most files are small*. This imbalanced design reflects such reality; if most files are indeed small, it makes sense to optimize for this case. Thus, with a small number of direct pointers (12 is a typical number), an inode

© 2008–19, ARPACI-DUSSEAU

THREE
EASY
PIECES