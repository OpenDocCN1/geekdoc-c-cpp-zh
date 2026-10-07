The CPU can access RAM almost as quickly as cache memory. Additionally, the amount of RAM available to store instructions and data is much larger than the amount of cache memory.

However, RAM, like cache memory, is temporary. Instructions and data contained in memory are lost once the computer is powered down. You may have had the unpleasant experience of losing unsaved data when your computer suffered off a power failure, or had to be rebooted.

Additionally, we would want the data to remain intact after the program ended, even if the computer is rebooted or powered off. That is not possible with RAM.

Furthermore, your computer likely has many other programs, for e-mail, Internet, word processing, and so on, that you may not be using right now, but you may want to use in the future. Likewise, your computer may also have other files, such as term papers, letters, tax spreadsheets, e-mail messages, and so on, that you may not be using right now but you may want to use in the future. Accordingly, we need another memory location, unlike cache memory or RAM, persistent—that is, it will persist even though the computer is rebooted or turned off.

# Persistent Storage

That other, persistent type of computer memory is naturally enough, persistent storage. This is usually a hard drive, but also could be, among other devices, a CD-ROM or DVD-ROM, floppy or disk zip, or optical drive. No matter what storage device is used, persistent is lasting; instructions and data remain stored even when the computer is powered down. Thus, your computer can be turned off for months, but when it is turned on, the files you previously saved are there.

Persistent storage, in addition to being lasting, also has a much larger capacity than RAM—about one hundred one thousand larger.

Since persistent storage has the advantage of lasting and having a large capacity, it is used to store programs and data. For example, if you used Microsoft Word on your computer, the files for your program would be stored on your hard drive. If you prepared documents using that program, those likewise would be saved as files on your hard drive.

While persistent storage has the advantages of being lasting and having a large capacity, a computer program cannot execute instructions located in persistent storage. The instructions must be loaded from persistent storage into RAM. Similarly, a computer program cannot manipulate data located in persistent storage. This data must be loaded from persistent storage into RAM.

+   **Note** Beyond the scope of this chapter, persistent storage also can serve as a backup to RAM, and when serving this is called virtual memory or swap space.

Generally, computer programs use RAM to store instructions and data, so RAM will be our focus in discussing memory. However, much of the discussion of memory may also apply to persistent storage. CPU cache memory is a different subject, discussed more in connection with programming languages, such as assembly language, that are far closer to machine language than C++.

# Addresses

When someone asks where you live, you may answer 1313 Mockbird Lane. That is