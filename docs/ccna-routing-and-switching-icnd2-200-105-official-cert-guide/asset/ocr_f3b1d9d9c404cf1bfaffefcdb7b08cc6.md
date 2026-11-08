In Chapter 3, the section titled “Configuring EtherChannel” listed the small set of working configuration options on the `channel-group` command. Those rules can be summarized as follows, for a single EtherChannel:

+   1. On the local switch, all the `channel-group` commands for all the physical interfaces must use the same `channel-group` number.
+   2. The `channel-group` number can be different on the neighboring switches.
+   3. If using the `on` keyword, you must use it on the corresponding interfaces of both switches.
+   4. If you use the `desirable` keyword on one switch, the switch uses PAgP; the other switch must use either `desirable` or `auto`.
+   5. If you use the `active` keyword on one switch, the switch uses LACP; the other switch must use either `active` or `passive`.