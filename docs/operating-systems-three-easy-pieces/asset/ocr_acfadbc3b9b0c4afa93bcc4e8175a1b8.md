# A Detailed Example

Because the process of writing (i.e., erasing and programming) is so unusual, let's go through a detailed example to make sure it makes sense. In this example, imagine we have the following four 8-bit pages, within a 4-page block (both unrealistically small sizes, but useful within this example); each page is VALID as each has been previously programmed.

| Page 0 | Page 1 | Page 2 | Page 3 |
| --- | --- | --- | --- |
| 00011000 | 11001110 | 00000001 | 00111111 |
| VALID | VALID | VALID | VALID |

Now say we wish to write page 0, filling it with new contents. To write any page, we must first erase the entire block. Let's assume we do so, thus leaving the block in this state:

| Page 0 | Page 1 | Page 2 | Page 3 |
| --- | --- | --- | --- |
| 11111111 | 11111111 | 11111111 | 11111111 |
| ERASED | ERASED | ERASED | ERASED |

Good news! We could now erase and program page 0, for example with contents 0000011, overwriting the old page 0 (contents 00011000) as desired. After doing so, our block looks like this:

| Page 0 | Page 1 | Page 2 | Page 3 |
| --- | --- | --- | --- |
| 00000011 | 11111111 | 11111111 | 11111111 |
| ERASED | ERASED | ERASED | ERASED |

And now we are: the contents of pages 1, 2, and 3 are all gone! Thus, before overwriting any page *within a block*, we must first move any data we care about to another location (e.g., memory, or elsewhere on the flash). The nature of erase will have a strong impact on how we design flash-based SSDs, as we'll soon learn about.

# Summary

To summarize, reading a page is easy: just read the page. Flash chips do this well, and quickly; in terms of performance, they offer the potential to greatly exceed the random read performance of disk drives, which are slow due to mechanical and rotation costs.

Writing a page is trickier; the entire block must be erased (taking care to first move any data we care about to another location), and then the desired page programmed. Not only is this expensive, frequent repetitions of this program/erase cycle can lead to the reliability problem flash chips have: wear out. When designing a storage system with flash, the performance and reliability of writing is a central focus. We'll soon learn more about how modern SSDs attack these issues, delivering excellent performance and reliability despite these limitations.