
XX

CONTENTS

## 24 Summary Dialogue on Memory Virtualization 295

## II Concurrency 299

## 25 A Dialogue on Concurrency 301

### 26 Concurrency: An Introduction . . . . . . . . . . 303
- 26.1 Why Use Threads? . . . . . . . . . . . . . . . . . . 304
- 26.2 An Example: Thread Creation . . . . . . . . . . . . . . . . . . 305
- 26.3 Why It Gets Wavy: Shared Data . . . . . . . . . . . . . . . . . . 308
- 26.4 The Heart Of The Problem: Uncontrolled Scheduling . . . . . . . . . 311
- 26.5 The Wish For Atomicity . . . . . . . . . . . . . . . . . . . . . . 313
- 26.6 One More Problem: Waiting For Another . . . . . . . . . . . 314
- 26.7 Summary: Why in OS Class? . . . . . . . . . . . . . . . . . . 315
- References . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 316
- Homework (Simulation) . . . . . . . . . . . . . . . . . . . . . . 317

## 27 Interlude: Thread API 319
- 27.1 Thread Creation . . . . . . . . . . . . . . . . . . . . . . 319
- 27.2 Thread Completion . . . . . . . . . . . . . . . . . . . . . . 320
- 27.3 Locks . . . . . . . . . . . . . . . . . . . . . . . . . . . 323
- 27.4 Condition Variables . . . . . . . . . . . . . . . . . 325
- 27.5 Compiling and Running . . . . . . . . . . . . . . . . 327
- 27.6 Summary . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 327
- References . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 329
- Homework (Code) . . . . . . . . . . . . . . . . . . . . . . . 330

## 28 Locks 331
- 28.1 Locks: The Basic Idea . . . . . . . . . . . . . . 331
- 28.2 Pthread Locks . . . . . . . . . . . . . . . . . . . . . . 332
- 28.3 Building A Lock . . . . . . . . . . . . . . . . . . . . . . 333
- 28.4 Evaluating Locks . . . . . . . . . . . . . . . . . . . . . . 333
- 28.5 Controlling Interrupts . . . . . . . . . . . . . . . . . 334
- 28.6 A Failed Attempt: Using Locks/Stores . . . . . 335
- 28.7 Building Working Spin Locks with Test-And-Set . . . 336
- 28.8 Evaluating Spin Locks . . . . . . . . . . . . . . . . . . . . . 339
- 28.9 Compare-and-Swap . . . . . . . . . . . . . . . . . . . . . . 340
- 28.10 Load-Linked and Store-Conditional . . . . . . . . . 341
- 28.11 Fetch-and-Add . . . . . . . . . . . . . . . . . . . . . . . 342
- 28.12 Too Many Spinning: What Now? . . . . . . . . . . . . 343
- 28.13 A Simple Approach: Just Yield, Baby. . . . . . 344
- 28.14 Using Queues: Sleeping Instead Of Spinning . . 345
- 28.15 Different OS, Different Support . . . . . . . 348
- 28.16 Two-Phase Locks . . . . . . . . . . . . . . . . . . . . . 350
- 28.17 Summary . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 350
- References . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 351

OPERATING SYSTEMS
[Version 1.01]

WWW.OSTEP.ORG

# CONTENTS

- Homework (Simulation) . . . . . . . . . . . . . . . . . . . . . . 352

## 29 Lock-based Concurrent Data Structures . . . . . . . . . . 353
- 29.1 Concurrent Counters . . . . . . . . . . . . . . . . . . . 353
- 29.2 Concurrent Linked Lists . . . . . . . . . . . . . . . . . 359
- 29.3 Concurrent Queues . . . . . . . . . . . . . . . . . . . 362
- 29.4 Concurrent Hash Table . . . . . . . . . . . . . . . 364
- 29.5 Summary . . . . . . . . . . . . . . . . . . . . . . . 364
- References . . . . . . . . . . . . . . . . . . . . . . . 367
- Homework (Code) . . . . . . . . . . . . . . . . . . . 368

## 30 Condition Variables . . . . . . . . . . . . . . . . . . . . . . 369
- 30.1 Definition and Routines . . . . . . . . . . . . . . . . . 370
- 30.2 The Producer / Consumer (Bounded Buffer) . . . 374
- 30.3 Covering Conditions . . . . . . . . . . . . . . . 382
- 30.4 Summary . . . . . . . . . . . . . . . . . . . . . . . 384
- References . . . . . . . . . . . . . . . . . . . . . . . 385
- Homework (Code) . . . . . . . . . . . . . . . . . . . . . . . 386

## 31 Semaphores . . . . . . . . . . . . . . . . . . . . . . . . 389
- 31.1 Semaphores: A Definition . . . . . . . . . . . . . . . 389
- 31.2 Binary Semaphores (Locks) . . . . . . . . . 391
- 31.3 Semaphores For Ordering . . . . . . . . . . . 392
- 31.4 The Producer / Consumer (Bounded Buffer) . . . 394
- 31.5 Reader-Writer Locks . . . . . . . . . . . . . . 399
- 31.6 The Dining Philosophers . . . . . . . . . 401
- 31.7 Throttling . . . . . . . . . . . . . . 404
- 31.8 How To Implement Semaphores . . . . 404
- 31.9 Summary . . . . . . . . . . . . . . . . . . . . . . . . 405
- References . . . . . . . . . . . . . . . . . . . . . . . 407
- Homework (Code) . . . . . . . . . . . . . . . . . . . . . . . 408

## 32 Common Concurrency Problems . . . . . . . . . 409
- 32.1 What Types Of Bugs Exist? . . . . . . . . 409
- 32.2 Non-Deadlock Bugs . . . . . . . . . 410
- 32.3 Deadlock Bugs . . . . . . . . . . . . . . 413
- 32.4 Summary . . . . . . . . . . . . . . . . . . . . . . . 422
- References . . . . . . . . . . . . . . . . . . . . . . . . 423
- Homework (Code) . . . . . . . . . . . . . . . . . . . . . . . 424

## 33 Event-based Concurrency (Advanced) . . . . . 425
- 33.1 The Basic Idea: An Event Loop . . . . . . 425
- 33.2 An Important API: select() (or poll()) . . . 426
- 33.3 Using select() . . . . . . . . . . . . . . . 427
- 33.4 Why Simpler? No Locks Needed . . . . 429
- 33.5 A Problem: Blocking System Calls . . . . . 429
- 33.6 A Solution: Asynchronous I/O . . . . . . 430
- 33.7 Another Problem: State Management . . . . . . . . . . . . . . 431
- 33.8 What Is Still Difficult With Events . . . . . . . . . . . . . . . 433
- 33.9 Summary . . . . . . . . . . . . . . . . . . . . . . . 434
- References . . . . . . . . . . . . . . . . . . . . . . . 435
- Homework (Code) . . . . . . . . . . . . . . . . . . . . . . . . 436

## 34 Summary Dialogue on Concurrency 437

## III Persistence 439

## 35 A Dialogue on Persistence 441

## 36 I/O Devices . . . . . . . . . . . . . . . . . . . . 443
- 36.1 System Architecture . . . . . . . . . . . . . . . 443
- 36.2 A Canonical Device . . . . . . . . . . . . . . . 445
- 36.3 The Canonical Protocol . . . . . . . . . . . . . . 446
- 36.4 Lowering CPU Overhead With Interrupts . . . . . . 447
- 36.5 More Data Movement With DMA . . . . . 448
- 36.6 Methods Of Device Interaction . . . . . 449
- 36.7 Fitting Into The OS: The Driver . . . . 450
- 36.8 Case Study: A Simple Disk Driver . . . 451
- 36.9 Historical Notes . . . . . . . . . . . . . . 453
- 36.10 Summary . . . . . . . . . . . . . . . . . . . . . . . . 455
- References . . . . . . . . . . . . . . . . . . . . . . . . . 456

## 37 Hard Drives 457
- 37.1 Interface . . . . . . . . . . . . . . . . . . . . 457
- 37.2 Geometry . . . . . . . . . . . . . . . . . . . . . 458
- 37.3 A Simple Disk . . . . . . . . . . . . . . . . . . . 459
- 37.4 I/O Time: Doing The Math . . . . . . . 462
- 37.5 Disk Scheduling . . . . . . . . . . . . . . . 466
- 37.6 Summary . . . . . . . . . . . . . . . . . . . . . . . 470
- References . . . . . . . . . . . . . . . . . . . . . . . . 471
- Homework (Simulation) . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 472

## 38 Redundant Arrays of Inexpensive Disks (RAIDs) 473
- 38.1 Interface And RAID . . . . . . . 774
- 38.2 Model . . . . . . . . . . . . . . . 475
- 38.3 How To Evaluate a RAID . . . . . 475
- 38.4 RAID Level 0: Striping . . . . . 476
- 38.5 RAID Level 1: Mirroring . . . . . 479
- 38.6 RAID Level 4: Saving Space With Parity . . . 482
- 38.7 RAID Level 5: Rotating Parity . . . 486
- 38.8 RAID Comparison: A Summary . . . 487
- 38.9 Other RAID Issues . . . . 488
- 38.10 Summary . . . . . . . . . . . . . . . . 488
- References . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 489
- Homework (Simulation) . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 490

## 39 Interlude: Files and Directories . . . . . . . . . . . . . . . . . . . 491
- 39.1 Files and Directories . . . . . . . . . . . . . . . . . . . . 491
- 39.2 The File System Interface . . . . . . . . . . . . . . . . 493
- 39.3 Creating Files . . . . . . . . . . . . . . . . . . . . . . . . . 493
- 39.4 Reading and Writing Files . . . . . . . . . . . . . . . . . 495
- 39.5 Reading and Writing, Not Sequentially . . . . . . . 497
- 39.6 Shared File Table Entries: fork() and dup() . . . . . 499
- 39.7 Writing Immediately with fsync() . . . . . . . . . . . . . . . 502
- 39.8 Renaming Files . . . . . . . . . . . . . . . . . . . . . . . 502
- 39.9 Getting Information About Files . . . . . . . . . . . . . 503
- 39.10 Removing Files . . . . . . . . . . . . . . . . . . . . . . . . 504
- 39.11 Making Directories . . . . . . . . . . . . . . . . . . . . 505
- 39.12 Reading Directories . . . . . . . . . . . . . . . . . . . . 506
- 39.13 Deleting Directories . . . . . . . . . . . . . . . . . . . . 507
- 39.14 Hard Links . . . . . . . . . . . . . . . . . . . . . . . . . 507
- 39.15 Symbolic Links . . . . . . . . . . . . . . . . . . . . . . . . 509
- 39.16 Permission Bits and Access Control Lists . . . . . 511
- 39.17 Making and Mounting a File System . . . . . . . 513
- 39.18 Summary . . . . . . . . . . . . . . . . . . . . . . . . . . . . 515
- References . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 517
- Homework (Code) . . . . . . . . . . . . . . . . . . . . . . . . . . . 518

## 40 File System Implementation . . . . . . . . . . . . . . . . . . . 519
- 40.1 The Way To Think . . . . . . . . . . . . . . . . . . . . . . . 519
- 40.2 Overall Organization . . . . . . . . . . . . . . . . . . . . 520
- 40.3 File Organization: The Inode . . . . . . . . . . . . . . 522
- 40.4 Directory Organization . . . . . . . . . . . . . . . . . . . . 526
- 40.5 Free Space Management . . . . . . . . . . . . . . . . . . . . 528
- 40.6 Access Paths: Reading and Writing . . . . . . . . 528
- 40.7 Caching and Buffering . . . . . . . . . . . . . . . . 532
- 40.8 Summary . . . . . . . . . . . . . . . . . . . . . . . . . . . . 534
- References . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 535
- Homework (Simulation) . . . . . . . . . . . . . . . . . . . . . . . . . . . 536

## 41 Locality and The Fast System . . . . . . . . . . . . . . . 537
- 41.1 The Problem: Poor Performance . . . . . . . . . . . . . . . . . 537
- 41.2 FFS: Disk Awareness Is The Solution . . . . . . . . . 539
- 41.3 Organizing Structure: The Cylinder Group . . . . . . 539
- 41.4 Policies: How To Allocate Files and Directories . . . 541
- 41.5 Measuring File Locality . . . . . . . . . . . . . . . . . . . . 543
- 41.6 The Large-File Exception . . . . . . . . . . . . . . . . 544
- 41.7 A Few Other Things About FFS . . . . . . . . . . . . 546
- 41.8 Summary . . . . . . . . . . . . . . . . . . . . . . . . . . . . 548
