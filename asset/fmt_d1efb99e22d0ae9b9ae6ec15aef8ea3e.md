
这里是以骨架形式表示的 `P1F`。假设了 `QS` 的常规定义以及入口处的编码。

```
GO TO Q1, Q2, ... Qn DEPENDING ON QS.
PISEQ.
Q1.
    PERFORM X.
    MOVE "OK" TO RESULT.
MOVE 2 TO QS. GOBACK.
Q2.
```

# 第 9 章 复杂反转 197

`MOVE RECORD TO RECAREA.`

`MOVE "OK" TO RESULT.`

`MOVE 3 TO QS. GOBACK.`

`Q3.`

...

...

`FORM Y.`

`MOVE "EF" TO RESULT.`

`MOVE n TO QS. GOBACK.`

`Qn.`

`PERFORM Z.`

`GOBACK.`

`PEND.`

对关闭的处理至关重要。我们将其分成了两部分。第一部分是一个写入操作，通过在结果字段中放置值 `"EF"` 来写入文件结束标记。`P1F` 中的这一写入操作是对 `P2` 中恰好遇到文件结束的读取操作的响应。第二部分是对 `P2` 中关闭操作的响应。它从 `Qn` 开始，以孤立的 `GOBACK` 结束。注意，如果编码为：

```
Qn.
MOVE p TO QS. GOBACK.
Qp.
PERFORM Z.
PEND.
```

我们选择在 `open` 时返回结果 `"OK"`，而在 `close` 时留空未指定的的结果。这是一个关于接口详细规范的问题。我们必须遵守我们所采用的任何惯例作为标准。

请注意，如果 `P2` 没有读取文件结束记录（可能是因为它本身能够独立地识别文件结束），那么 `P1F` 将无法正常运行。以下指令：

```
PERFORM Y.
MOVE "EF" TO RESULT.
MOVE n TO QS. GOBACK.
```

# 198 程序设计原理

将响应来自 `P2` 的关闭调用而执行，而不是响应最后一次读取调用的响应；指令

# `PERFORM Z.`

将完全不会被执行。除非重新设计 `P1F`，使其也能识别出自己何时被最后一次调用，否则它将一直等待一个永远不会来的调用。一种识别方法当然是让 `P1F` 检查 `OPCODE` 的值：这会产生一些复杂性，将在下文中讨论。目前，我们假设在 `P1F` 中不需要检查 `OPCODE` 的值：只要 `P2` 的设计与 `P1` 进行了正确的协调，并且只要 `P2` 读取了 `F` 的所有记录（包括文件结束标记），我们就知道 `OPCODE` 在 `Q1` 处的值为“`OP`”，在 `Qn` 处的值为“`CL`”，在所有其他时间的值为“`RN`”。

反转 `P2` 得到 `P2F`，就像是给读者的的一项练习。

## 9.3

我们现在回到问题 13（电报分析），更详细地考虑 `P1` 相对于单词文件反转的版本。

首先，我们引入了 `P2` 和 `P1W` 之间的标准接口。`P2` 现在使用 `OPCODE` 值“`OP`”、“`RN`”和“`CL`”分别来打开、读取和关闭单词文件。第 8.5 节给出的 `P1W` 编码必须修改为：

```
ENTRY “P1W” USING COMM, WORD.
GO TO Q1, Q2, Q3, Q4 DEPENDING ON QS.
PISEQ.
OPEN INPUT TAPE.
READ PTAPE AT END MOVE “E” TO TAPE-EOF.
MOVE “OK” TO RESULT.
MOVE 2 TO QS. GOBACK.
Q2.
PTAPEBODYITER.
IF PTAPE-EOF = “E”...
...
PWODYEND.

# 第 9 章 复杂反转 199

MOVE “OK” TO RESULT.
MOVE 3 TO QS. GOBACK.
Q3.
...
...
PTAPEBEND.
MOVE “EF” TO RESULT.
MOVE 4 TO QS. GOBACK.
Q4.
CLOSE PTAPE.
GOBACK.
P1END.
```

`P1W` 现在处理一个打开调用和一个关闭调用；此外，它在单词上写入文件结束标记。到目前为止，我们只是让 13 的解决方案与 9.1 和 9.2 的讨论保持一致。现在我们引入了一个显著的情况：不再假设 `P2` 总是读取到文件结束，而是允许它关闭单词文件。例如，我们可以假设 `P2` 处理前 20 条电报，如果少于 20 条则处理整个磁带。`P1W` 现在必须检查 `OPCODE` 的值。以前，`P1W` 忽略 `OPCODE` 的值，假设它在 `Q1` 处值为“`OP`”，在 `Q2` 和 `Q3` 处值为“`RN`”，在 `Q4` 处值为“`CL`”；实际上没有从 `P2` 到 `P1W` 的信息流。现在，我们有了以文件 `FINV` 形式从 `P2` 到 `P1W` 的信息流：

![](img/2af5282003b6600210009_214.png)

当然，这个调用文件一直存在；但我们之前忽略了它。现在我们必须在 `P1` 的设计中考虑到它，并且必须同时相对于 `FINV` 和 `WORDS` 进行反转。`FINV` 的结构显然如200 页顶部所示，其中 `RN` 记录的数量不能超过 `W+1`，其中 `W` 是磁带上的单词数。

# 215 程序设计原理

| FINV |
| :--- |
| OP | FINV BODY | CL | FULL° WORDS | PART° WORDS |
| FULL° FINV | PART° FINV | FULL WORDS BODY | EOF REC | WORD* REC |
| RN* | RN* | WORD* REC |

其中 `full finv` 包含 `W+1` 条 `RN` 记录，`part finv` 包含少于 `W+1` 条 `RN` 记录，`full words` 包含 `W` 条单词并在后跟结束标记，`part words` 包含 `W` 或更少单词记录且后没有结束标记。磁带文件的对应结构如所示。
形成程序结构所需的对应关系：

`finv body` 对应 `words` 和 `ptape`
`full finv` 对应 `full words` 和 `full ptape`

# 第 9 章 复杂反转 201

部分 `finv` 对应于 `words` 部分以及 `ptape` 的部分。

完整 `finv` 中的 `RN` 对应完整 `words` 体中的 `word rec`，以及 `eof rec`，并对应完整 `ptape` 中的 `word block` 和 `eof block`。

![](img/2af52882003b66fe0217f904c606a0f9_216_0.png)

由于我们无法预先判断获得的是完整的 `finv` 还是部分的 `finv`，我们将程序体结构化为带有回溯的选择结构。在设计的第一个阶段，在引入 `quit` 语句或处理副作用之前，我们有：

```
P1 seq

open finv;

read finv (OP record);

open words;

open ptape; (process OP record)

read block;

read finv (1st RN or CL record);
```

# 202 程序设计原理

```
PBODY select full

PFULLBODY iter until eof-ptape

    BS :=1;

    PBLOCKBODY iter until EOB

        CHARGROUP select word

            build word;

            write word rec; } (process RN record)

    read finv (RN record);

    PCHARGROUP or space group

        process spaces;

    PCHARGROUP end

    PBLOCKBODY end

    read block;

PFULLBODY end

    write eof-rec; (process RN record)

read finv (CL record);

...

PBODY or part

...

PBODY end

close ptape; } (process CL record)

close words;

close finv;
```

`P1` 括号中的注释指的是 `finv` 的记录：例如，
`read finv (RN record);`
意味着读取操作的结果必须是 `finv` 的一个 `RN` 记录，并且
`build word: write word rec: } (process RN record)`
意味着 `build` 和 `write` 操作构成了对 `finv` 的 `RN` 记录的处理。

显然，在回溯设计的第二个阶段，我们需要两个 `quit` 语句。`PBODY` 将采取以下形式：

```
PBODY posit full

PFULLBODY iter until eof-ptape

    BS :=1;
```

# 第 9 章 复杂反转 203

```
PBLOCKBODY iter until EOB

PCHARGROUP select word

quit PBODY if not RN;

build word;

write word rec;

read finv;

PCHARGROUP or space group

process spaces;

PCHARGROUP end

PBLOCKBODY end

read block;

PFULLBODY end

quit PBODY if not RN;

write eof-rec;

read finv;

PBODY admit part

...
```

注意，`quit` 语句被放置在处理 `finv` 记录的地方，而不是读取它们的地方。这在运行时的效果是导致纸带（paper tape）的处理比绝对需要的稍多一点：处理将持续到第一个要被忽略的单词的开始，而不是在最后一个写入单词的结束处停止。这种微小的效率低下是重要的——而且我们可能不会这样做——我们可以通过移动 `quit` 语句来优化，使其在最早的时间执行，即在读到每条 `finv` 记录时立即执行。生成的程序将是：

```
PBODY posit full

quit PBODY if not RN;

PFULLBODY iter until eof-ptape

BS:=1;

PBLOCKBODY iter until EOB

PCHARGROUP select word

build word:

write word rec;

read finv;

quit PBODY if not RN;

PCHARGROUP or space group

process spaces;

PCHARGROUP end
```

# 程序设计原理

```
PBLOCBODY end

read block;

PFULLBODY end

write eof-rec;

read finv;

...
```

`PBODY admit part`
我们现在考虑第三阶段，即副作用的处理。现在显而易见所有的副作用都是有益的：当我们退出 `PBODY` 时，我们恰好处理了应处理的纸带，不需要在 `PBODY` 的 `admit` 部分重复该处理，也不需要进一步考虑副作用。然而，我们必须考虑是否对 `part ptpage` 的剩余部分需要任何处理。这部分剩余仅由文件结束块组成，或由文件结束块及其之前的若干个普通块组成（其中第一个块可能被部分处理过）。在大多数现实环境中，我们可以忽略这部分剩余：在没有读取所有块的情况下关闭纸带将无影响。然而，为了提供说明，我们将假设所有块都必须被读取。那么 `PBODY` 第二部分的形式必须是：

```
PBODY admit part

PPARTBODY iter until eof-ptape

read block;

PPARTBODY end

PBODY end
```

我们现在有了新版本 `P1` 的完整设计，剩下的只是相对于 `finv` 和单词文件进行反转，以得到所需的 `P1W` 版本。`P1W` 的 `COBOL` 代码如下所示。以下点值得注意：

- 相对于两个文件的同时反转没有引起困难，因为“`write word`”语句与“`read finv`” 语句相匹配；
- 文件结束标记被显式地视为单词文件的一条记录，在关闭单词文件时不需要写入它；
- 反转中忽略了 `finv` 的 `open` 和 `close` 语句——否则我们将陷入无限递归。

# 第 9 章 复杂反转

`P1W` 的 `COBOL` 代码为：

```
ENTRY “P1W” USING 1, 2, 3, 4.

IF 1 = 1 THEN

    OPEN INPUT FINV;

    OPEN INPUT WORDS;

    OPEN OUTPUT PTAPE;

    PERFORM UNTIL STATUS-PTAPE = 0

        SET BS = 1

        PERFORM UNTIL STATUS-BLOCK = 0

            IF STATUS-CHAR = 1 THEN

                IF 2 IS NOT 1 THEN

                    EXIT PERFORM

                END IF

                BUILD WORD;

                WRITE WORD-REC.

                READ FINV;

                IF 2 IS NOT 1 THEN

                    EXIT PERFORM

                END IF

            ELSE IF STATUS-CHAR = 2 THEN

                PROCESS SPACES;

            END IF

        END-PERFORM

        READ BLOCK;

    END-PERFORM

        IF 2 IS NOT 1 THEN

            WRITE EOF-REC;

            READ FINV.

        END-

END-IF.

    END  = 

         = V.

    IF 2 = 4 THEN

        CLOSE PTAPE;

        CLOSE WORDS;

        CLOSE FINV.

    END-IF.

END-IF.
```
