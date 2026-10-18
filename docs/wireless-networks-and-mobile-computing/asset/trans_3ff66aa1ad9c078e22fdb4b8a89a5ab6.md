
## 5.36 请求泛洪

本质上，上述路由发现操作是基于在网络中泛洪 $RREQ$ 消息，以通过网络中的不同源和目的路径到达目的节点。为了说明此路由发现过程，请参考图 5.36 所示的网络。目的序列号未显示。从任意节点向其任何可能的邻居节点转发的 $RREQ$ 消息字段按顺序包含源 id、目的 id 和跳计数。每个节点转发的 $RREQ$ 消息都显示在相应的链路上。因此，当节点 $F$ 收到转发消息的跳计数为 2 时，$F$ 会忽略该消息，因为它已经收到一个跳计数为 1 的 $RREQ$ 消息。此外，节点 $C$ 从 $A$ 和 $B$ 分别收到两条 $RREQ$ 消息，仅处理其中一条，即最先到达 $C$ 的那条（假设是 $A$ 的消息）。

当 $RREQ$ 消息被目的节点 $D$ 收到时，$D$ 会向源节点 $S$ 发送路由回复消息 $RREP$。$RREP$ 消息包含源节点和目的节点的地址、目的序列号、初始化为零的跳计数，以及前向路由信息（从 $S$ 到 $D$）。最初，$RREP$ 消息中形成的前向路由信息为空。目的序列号从 $D$ 在上一次发送的 $RREP$ 消息中使用的序列号中递增。目的节点 $D$ 然后单播该 $RREP$ 消息到它从该消息中接收 $RREQ$ 的邻居节点（根据其对应的逆路由信息条目）。当一个 $RREP$ 消息被节点 $u$ 从其邻居节点（例如 $v$）接收时，$u$ 会通过在前向路由信息中追加节点 $v$ 的地址来增强接收到的 $RREP$ 消息，并使跳计数字段增加 1。因此，参考图 5.37，目的节点 $D$ 会将带有跳计数 3 的 $RREP$ 消息向源节点 $S$ 逆向沿着源-目的路径（$S$、$F$、$E$、$D$）发送回去。每个节点都知道它从哪个节点接收到对应的 $RREQ$ 消息，即节点 $D$ 知道 $RREQ$ 消息来自 $E$，因此它会将 $RREP$ 消息发送给 $E$；$E$ 知道它从 $F$ 收到 $RREQ$ 消息，因此转发 $RREP$ 消息给 $F$；最后 $F$ 将 $RREP$ 消息发送给 $S$。

如果 $D$ 后来收到另一个来自 $S$ 的、具有相同请求标识号且跳计数值更小的新 $RREQ$ 消息，$D$ 会基于新的路由信息（路径更短）重新向 $S$ 发送一条新的 $RREP$ 消息。

然而，如前所述，在路由发现过程中，$RREQ$ 消息也可能被中间节点 $u$（$u$ 不是目的节点 $D$）接收，而 $u$ 具有从 $u$ 到 $D$ 的路由信息，且该信息的目的序列号高于接收到的 $RREQ$ 消息中的序列号。此时，$u$ 会向从该 $RREQ$ 消息接收的邻居节点发送 $RREP$ 消息（而不是继续广播 $RREQ$），在 $RREP$ 消息的前向路由信息中填入 $u$ 到 $D$ 的已存储路由信息，并将 $RREP$ 消息的跳计数字段设置为其表中 $u$ 到 $D$ 的路由信息的跳计数。

在形成路由后，源节点 $S$ 开始通过该路由向目的节点 $D$ 发送数据包。一旦路由建立，必须在 $S$ 到 $D$ 发送数据包的整个过程中保持该路由。如果在此期间因节点移动或其他原因出现链路故障，类似于 $DSR$ 协议，会启动路由错误消息 $RERR$。

最后，当节点 $u$ 检测到网络分区（即包含 $u$ 的网络部分与目的地分离，使得 $u$ 无法再从目的节点到达），$u$ 会发出路由擦除消息，以从 $u$ 到目的地删除所有无效的路由。

区域路由协议（ZRP）[22]结合了主动和反应性协议的特点。每个节点周围定义一个区域，其范围以覆盖整个区域所需的跳数来衡量。每个节点在其区域内遵循主动路由协议，在区域外遵循反应性路由协议。因此，参考图 5.40，假设区域定义为两跳范围，则源节点 $S$ 的区域内包含节点 $A$、gion 被分割成六边形单元格。在这个叠加的单元格结构中，位于给定单元格中的移动终端数量指示该单元格的需求。假设两个位于距离至少 3 的两个单元格中的移动终端在传输期间不会相互干扰。因此，位于距离至少 3 的两个单元格中的移动终端可以使用相同的时间槽广播其消息。基于这些假设，请描述一个算法，以高效方式在不同单元格中的节点之间分配时间槽。计算该算法的时间复杂度。

+   5. 假设一个节点的 id 值为二进制的 00011。该节点有三个邻居，其二进制 id 值分别为 11101、11011 和 01110，它们都希望同时向节点 00011 发送消息。根据本章节描述的广度优先广播策略，说明碰撞将如何解决，以及节点 00011 最终如何正确接收消息。

+   6. 描content<unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk> 11 在二进制中为 00011 的节点有三个邻居，其二进制 id 值分别为 11101、11011 和 01110，它们都希望同时向节点 00011 发送消息。根据本章节描述的广度优先广播策略，说明碰撞将如何被解决，以及节点 00011 最终能否正确接收消息。

## 6. 描述一个确定性广播算法，用于在自适应网络中进行广播，明确说明底层模型和算法的工作原理。

## 7. 证明上述算法的正确性，并计算其最坏情况时间复杂度。

## 8. 主动、反应式和混<unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk><unk>
