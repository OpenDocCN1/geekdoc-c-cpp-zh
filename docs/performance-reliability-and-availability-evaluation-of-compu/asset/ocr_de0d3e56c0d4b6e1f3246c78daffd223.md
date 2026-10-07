# 410 Performance, Reliability, and Availability Evaluation of Computational Systems

+   - -t, --time enables time/date output,
- -T, --epoch enables time counter (seconds),
- -y, --sys enables system stats,
- -a, --all equals expands -C, -D, -I, -N and -S discovery lists,
- -v, --vmstat equals -pmgdsc -D total:

and

+   - --aio enables aio stats,
-- --fs, --filesystem enables fs stats,
-- --ipc enables ipc stats,
-- --lock enables lock stats,
-- --raw enables raw stats,
-- --socket enables socket stats,
-- --tcp enables tcp stats,
-- --udp enables udp stats,
-- --unix enables unix stats,
-- --vm enables vm stats.

The list of options and external plugins can also be seen by executing the command line:

> > dstat --list

A typical output shows the internal commands and the list of plugins as presented below.

internal:

```
aio, cpu, cpu24, disk, disk24, disk24old, epoch, fs, int,
int24, io, ipc, load, lock, mem, net, page, page24,
proc, raw, socket, swap, swapold, sys, tcp, time, udp,
unix, vm
```