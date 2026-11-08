

### 图17-10：命名ACL与编号ACL的配置对比

![](img/79473ea15699e01619d2aa789f5bd43b_527_0.png)

命名ACL配置中真正全新的部分只有 ip access-list 全局配置命令。该命令定义ACL是标准ACL还是扩展ACL，并定义名称。它还将用户带入ACL配置模式，如即将展示的示例17-4所示。进入ACL配置模式后，你可以配置 permit、deny 和 remark 命令，这些命令与编号ACL的 access-list 命令语法相同。如果你配置的是标准命名ACL，这些命令与标准编号ACL的语法匹配；如果你配置的是扩展命名ACL，它们则与扩展编号ACL的语法匹配。

示例17-4展示了一个命名扩展ACL的配置。请特别留意配置模式提示符，它们显示的是ACL配置模式。

### 示例17-4：命名访问列表配置

```text
Router# configure terminal
Enter configuration commands, one per line.  End with Ctrl-Z.
Router(config)# ip access-list extended barney
Router(config-ext-nacl)# permit tcp host 10.1.1.2 eq www any
Router(config-ext-nacl)# deny udp host 10.1.1.1 10.1.2.0 0.0.0.255
Router(config-ext-nacl)# deny ip 10.1.3.0 0.0.0.255 10.1.2.0 0.0.0.255
Router(config-ext-nacl)# deny ip 10.1.2.0 0.0.0.255 10.2.3.0 0.0.0.255
Router(config-ext-nacl)# permit ip any any
Router(config-ext-nacl)# interface serial1
Router(config-if)# ip access-group barney out
Router(config-if)# ^Z
Router# show running-config
Building configuration...

Current configuration:

! lines omitted for brevity

interface serial 1
 ip access-group barney out
!
ip access-list extended barney
 permit tcp host 10.1.1.2 eq www any
 deny   udp host 10.1.1.1 10.1.2.0 0.0.0.255
 deny   ip 10.1.3.0 0.0.0.255 10.1.2.0 0.0.0.255
 deny   ip 10.1.2.0 0.0.0.255 10.2.3.0 0.0.0.255
 permit ip any any
```

示例17-4首先创建了一个名为barney的ACL。**ip access-list extended barney** 命令创建了该ACL，命名为barney，并将用户置于ACL配置模式。此命令还告诉IOS，barney是一个扩展ACL。接下来，五条不同的**permit**和**deny**语句定义了匹配逻辑以及匹配后要执行的操作。**show running-config**命令的输出在删除单一条目前列出了命名ACL配置。

命名ACL允许用户在ACL配置模式下删除和添加ACL中的新行。示例17-5展示了如何使用 no deny ip . . . 命令从ACL中删除单个条目。请注意，示例末尾的**show access-list**命令输出仍然列出了该ACL，但包含的是四条**permit**和**deny**命令，而不是五条。

### 示例17-5：从命名ACL中移除一条命令

```text
Router# configure terminal
Enter configuration commands, one per line.  End with Ctrl-Z.
Router(config)# ip access-list extended barney
Router(config-ext-nacl)# no deny ip 10.1.2.0 0.0.0.255 10.2.3.0 0.0.0.255
Router(config-ext-nacl)# ^Z
Router# show access-list

Extended IP access list barney
    10 permit tcp host 10.1.1.2 eq www any
    20 deny udp host 10.1.1.1 10.1.2.0 0.0.0.255
    30 deny   ip 10.1.3.0 0.0.0.255 10.1.2.0 0.0.0.255
    50 permit ip any any
```

## 使用序列号编辑ACL

编号ACL从Cisco路由器和IOS早期就已经存在于IOS中；然而，多年来，在许多IOS版本中，编辑编号IP ACL的能力一直很弱。例如，仅仅删除ACL中的一行，用户也不得不删除整个ACL，然后重新配置。

ACL编辑功能使用一个ACL序列号，该序列号被添加到每个ACL的permit或deny语句中，这些数字表示ACL中语句的顺序。ACL序列号为编号ACL和命名ACL提供了以下功能：

![](img/79473ea15699e01619d2aa789f5bd43b_528_0.png)

- **编号ACL的新配置样式：** 编号ACL可以使用类似于命名ACL的配置样式，也可以使用传统样式，用于同一个ACL；执行高级ACL编辑需要新样式。
- **删除单行：** 可以使用 *no sequence-number* 子命令删除单条ACL permit或deny语句。
- **插入新行：** 新添加的permit和deny命令可以在deny或permit命令前配置一个序列号，以此决定语句在ACL中的位置。
- **自动序列编号：** 即使你不包含序列号，IOS也会在配置命令时自动添加序列号。

要利用在ACL中删除和插入行的功能，编号ACL和命名ACL都必须使用与命名ACL相同的整体配置样式和命令。语法上的唯一区别是使用名称还是编号。示例17-6展示了使用这种替代配置样式配置标准编号IP ACL的过程。该示例展示了ACL序列号在编辑方面的强大功能。在此示例中，进行了以下操作：

1. **第1步：** 使用这种新样式配置编号ACL 24，其中包含三条permit命令。
2. **第2步：** `show ip access-lists` 命令显示三条permit命令及其序列号10、20和30。
3. **第3步：** 工程师使用 **no 20** ACL子命令仅删除第二条permit命令，该子命令直接引用序列号20。
4. **第4步：** `show ip access-lists` 命令确认该ACL现在只有两行（序列号10和30）。
5. **第5步：** 工程师使用 **5 deny 10.1.1.1** ACL子命令在ACL开头添加一条新的deny命令。
6. **第6步：** `show ip access-lists` 命令再次确认了这些更改，这次列出了三条命令，序列号分别为5、10和30。

> **注意** 在本示例中，注意用户没有退出配置模式，而是使用 `do` 命令让IOS从配置模式执行 `show ip access-lists` EXEC命令。

### 示例17-6 — 使用序列号编辑ACL

```text
! Step 1: The 3-line Standard Numbered IP ACL is configured.
R1# configure terminal
Enter configuration commands, one per line.  End with Ctrl-Z.
R1(config)# ip access-list standard 24
R1(config-std-nacl)# permit 10.1.1.0 0.0.0.255
R1(config-std-nacl)# permit 10.1.2.0 0.0.0.255
R1(config-std-nacl)# permit 10.1.3.0 0.0.0.255

! Step 2: Displaying the ACL's contents, without leaving configuration mode.
R1(config-std-nacl)# do show ip access-lists 24
Standard IP access list 24
    10 permit 10.1.1.0, wildcard bits 0.0.0.255
    20 permit 10.1.2.0, wildcard bits 0.0.0.255
    30 permit 10.1.3.0, wildcard bits 0.0.0.255

! Step 3: Still in ACL 24 configuration mode, the line with sequence number 20 is deleted.
R1(config-std-nacl)# no 20

! Step 4: Displaying the ACL's contents again, without leaving configuration mode.
! Note that line number 20 is no longer listed.
R1(config-std-nacl)# do show ip access-lists 24
Standard IP access list 24
    10 permit 10.1.1.0, wildcard bits 0.0.0.255
    30 permit 10.1.3.0, wildcard bits 0.0.0.255

! Step 5: Inserting a new first line in the ACL.
R1(config-std-nacl)# 5 deny 10.1.1.1

! Step 6: Displaying the ACL's contents one last time, with the new statement
! (sequence number 5) listed first.
R1(config-std-nacl)# do show ip access-lists 24
Standard IP access list 24
     5 deny 10.1.1.1
    10 permit 10.1.1.0, wildcard bits 0.0.0.255
    30 permit 10.1.3.0, wildcard bits 0.0.0.255
```

请注意，虽然示例17-6使用的是编号ACL，但命名ACL使用相同的流程来编辑（添加和移除）条目。

## 编号ACL配置与命名ACL配置对比

关于编号ACL，顺便提一下，在较新的IOS版本中，IOS实际上允许两种方式来配置编号ACL。首先，IOS支持传统方法，即使用前面示例17-1、17-2和17-3中展示的 access-list 全局命令。IOS也支持使用与命名ACL类似的命令来配置编号ACL，如示例17-6所示。

奇怪的是，无论使用哪种方法配置ACL，IOS总是以原始配置样式（即全局 access-list 命令）来存储编号ACL。示例17-7紧接示例17-6的结束继续演示这些事实，包含以下额外步骤：

7. **第7步：** 工程师列出配置（**show running-config**），其中列出了旧样式的配置命令——尽管该ACL是使用新样式命令创建的。
8. **第8步：** 工程师使用旧样式的 access-list 24 permit 10.1.4.0 0.0.0.255 全局配置命令向ACL末尾添加一条新语句。
9. **第9步：** **show ip access-lists** 命令确认了上一步中的旧样式 access-list 命令遵循了只能添加到ACL末尾的规则。
10. **第10步：** 工程师显示配置，以确认使用新样式命令和旧样式命令配置的ACL 24各部分都列在同一条旧样式ACL中（**show running-config**）。

### 示例17-7：添加并显示编号ACL配置

```text
! Step 7: A configuration snippet for ACL 24.
R1# show running-config
```

