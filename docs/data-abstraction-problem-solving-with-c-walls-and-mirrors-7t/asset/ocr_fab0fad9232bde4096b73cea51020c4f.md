# 2.5 Organizing Data

Given some data organized in one way, you might need to organize it in another way. Thus, you will actually change some aspect of the data and not, for example, simply search it. The problem in this section is called the Towers of Hanoi. Although this classic problem probably has no direct real-world application, we consider it because its solution so well illustrates the use of recursion.

# 2.5.1 The Towers of Hanoi

Many, many years ago, in a distant part of the Orient—in the Vietnamese city of Hanoi—the emperor's wiseperson passed on to join his ancestors. The emperor needed a replacement wiseperson. Being a rather wise person himself, the emperor devised a puzzle, declaring that its solver could have the job of wiseperson.

![](bbox=[0.206, 0.325, 0.936, 0.795])

The emperor's puzzle consisted of n disks (he didn't say exactly how many) and three poles: A (the source), B (the destination), and C (the spare). The disks were of different sizes and had holes in the middle so that they could fit on the poles. Because of their great weight, the disks could be placed only on top of disks larger than themselves. Initially, all the disks were on pole A, as shown in Figure 2-16a. The puzzle was to move the disks, one by one, from pole A to pole B. A person could also use pole C in the course of the transfer, but again a disk could be placed only on top of a disk larger than itself.