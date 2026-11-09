
## 13 Integrity

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_343_0.png)

Several promises in the oath involve integrity.

### Small Cycles

*Promise 4. I will make frequent, small releases so that I do not impede the progress of others.*

Making small releases just means changing a small amount of code for each release. The system may be large, but the incremental changes to that system are small.

### The History of Source Code Control

Let’s go back to the 1960s for a moment. What is your source code control system when your source code is punched on a deck of cards (Figure 13.1)?

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_344_0.png)

**Figure 13.1** Punch card

The source code is not stored on disk. It’s not “in the computer.” Your source code is, literally, in your hand.

What is the source code control system? It is your desk drawer.

When you literally possess the source code, there is no need to “control” it. Nobody else can touch it.

And this was the situation throughout much of the 1950s and 1960s. Nobody even dreamed of something like a source code control system. You simply kept the source code under control by putting it in a drawer or a cabinet.

If anyone wanted to “check out” the source code, they simply went to the cabinet and took it. When they were done, they put it back.

We certainly didn’t have merge problems. It was physically impossible for two programmers to be making changes to the same modules at the same time.

But things started to change in the 1970s. The idea of storing your source code on magnetic tape or even on disk was becoming attractive. We wrote line editing programs that allowed us to add, replace, and delete lines in source files on tape. These programs weren’t screen editors. We *punched* our add, change, and delete directives on cards. The editor would read the source tape, apply the changes from the edit deck, and write the new source tape.

You may think this sounds awful. Looking back on it—it was. But it was better than trying to manage programs on cards! I mean 6,000 lines of code on cards weighs 30 pounds. What would you do if you accidentally dropped those cards and watched as they spread all over the floor and under furniture and down into heating vents?

If you drop a tape, you can just pick it up again.

Anyway, notice what happened. We started with one source tape, and in the editing process, we wound up with a second, new source tape. But the old tape still existed. If we put that old tape back on the rack, someone else might inadvertently apply their own changes to it, leaving us with a merge problem.

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_347_0.png)

**Figure 13.2** A bulletin board

The bulletin board had labels on it for each of the modules in the system. We programmers each had our own color thumbtack. I was blue. Ken was red. My buddy CK was yellow, and so on.

If I wanted to edit the Trunk Manager module, I’d look on the bulletin board to see if there was a pin in that module. If not, I put a blue pin in it. Then I took the master tape from the rack and copied it onto a separate tape.

I would edit the Trunk Manager module, and only the Trunk Manager module, generating a new tape with my changes. I’d compile, test, rinse and repeat until I got my changes to work. Then I’d go get the master tape from the rack, and I would create a new master by copying the current master but replacing the Trunk Manager module with my changes. I’d put the new master back in the rack.

Finally, I’d remove my blue pin from the bulletin board.

This worked, but it only worked because we all knew each other, we all worked in the same office together, we each knew what the others were doing. And we *talked* to each other all the time.

I’d holler across the lab: “Ken, I’m going to change the Trunk Manager module.” He’d say: “Put a pin in it.” I’d say: “I already did.”

The pins were just reminders. We all knew the status of the code and who was working on what. And that’s why the system worked.

Indeed, it worked very well. Knowing what each of the other programmers was doing meant that we could help each other. We could make suggestions. We could warn each other about problems we’d recently encountered. And we could avoid merges.

Back then, merges were NOT fun.

Then, in the 1980s, came the disks. Disks got big, and they got permanent. By *big*, I mean hundreds of megabytes. By *permanent*, I mean that they were permanently mounted—always on line.

The other thing that happened is that we got machines like PDP-11s and VAXes. We got screen editors, real operating systems, and multiple terminals. More than one person could be editing at exactly the same time.

The era of thumbtacks and bulletin boards had to come to an end.

First of all, by then, we had twenty or thirty programmers. There weren’t enough thumbtack colors. Second, we had hundreds and hundreds of modules. We didn’t have enough space on the bulletin board.

Fortunately, there was a solution.

In 1972, Marc Rochkind wrote the first source code control program. It was called the Source Code Control System (SCCS), and he wrote it in SNOBOL.[^1]

[^1]: A lovely little string processing language from the 1960s that had many of the pattern-matching facilities of our modern languages.

Later, he rewrote it in C, and it became part of the UNIX distribution on PDP-11s. SCCS worked on only one file at a time but allowed you to lock that file so that no one else could edit it until you were done. It was a life saver.

In 1982, RCS, the Revision Control System, was created by Walter Tichy. It too was file based and knew nothing of projects, but it was considered an improvement over SCCS and rapidly became the standard source code control system of the day.

Then, in 1986, CVS, the Concurrent Versions System, came along. It extended RCS to deal with whole projects, not just individual files. It also introduced the concept of *optimistic locking*.

Up to this time, most source code control systems worked like my thumbtacks. If you had checked out the module, nobody else could edit it. This is called *pessimistic locking*.

CVS used optimistic locking. Two programmers could check out and change the same file at the same time. CVS would try to merge any nonconflicting changes and would alert you if it couldn't figure out how to do the merge.

After that, source code control systems exploded and even became commercial products. Literally hundreds of them flooded the market. Some used optimistic locking, others used pessimistic locking. The locking strategy became a kind of religious divide in the industry.

Then, in 2000, Subversion was created. It vastly improved upon CVS, and was instrumental in driving the industry away from pessimistic locking once and for all. Subversion was also the first source code control system to be used in the cloud. Does anybody remember SourceForge?

Up to this point, all source code control systems were based on the master tape idea that I used back in my bulletin board days. The source code was maintained in a single central master repository. Source code was checked out from that master repository, and commits were made back into that master repository.

But all that was about to change.

### Git

The year is 2005. Multi-gigabyte disks are in our laptops. Network speeds are fast and getting faster. Processor clock rates have plateaued at 2.6GHz.

We are very, very far beyond my old bulletin board control system for source code. But we are still using the master tape concept. We still have a central repository that everybody has to check in and out of. Every commit, every reversion, every merge requires network connectivity to the master.

And then came git.

Well, actually, git was presaged by BitKeeper and monotone; but it was git that caught the attention of the programming world and changed everything. Because, you see, git eliminates the master tape.

Oh, you still need a final authoritative version of the source code. But git does not automatically provide this location for you. Git simply doesn't care about that. Where you decide to put your authoritative version is entirely up to you. Git has nothing whatever to do with it.

Git keeps the entire history of the source code on your local machine. Your laptop, if that's what you use. On your machine, you can commit changes, create branches, check out old versions, and generally do anything you could do with a centralized system like Subversion—except you don't need to be connected to some central server.

Any time you like, you can connect to another user and push any of the changes you've made to that user. Or you can pull any changes they have made into your local repository. Neither is master. Both are equal. That's why they call it peer to peer.

And the final authoritative location that you use for making production releases is just another peer that people can push to or pull from any time they like.

The end result is that you are free to make as many small commits as you like before you push your changes somewhere else. You can commit every
