
- 表演者的物理布局及其在表演小组中的组织

- 给表演者和表演小组的表演指令

- 以表演指令记录的作曲家的音乐想法

对于管弦作品作曲家来说，所有因素都是重要的。因此，每个因素都需要在管弦乐作曲库中表示，以便该库能够充分创建一个类似于为管弦乐作曲的体验。上述每个因素通过以下面向对象的编程类在作曲库中表示：具有属性的类、这些类的配置以及调用类的方法。通过使用面向对象编程的这些方面，我们可以创建一个我们对管弦乐作曲观察的模型。以下子节将介绍上述管弦乐作曲的每一个方面。

### 14.3.1 使用 Csdound 处理乐器和音符

我们需要软件或硬件乐器来产生声音。我们还需要一种执行这些乐器的方法，传入不同的参数来影响诸如乐器音高和音量等音乐特性。此时，我们有多种处理方法。虽然我们可以开发一个音乐乐器软件库并创建一个音乐软件引擎用控制信息驱动这些乐器，但这将花费大量时间。由于该库的重点是更高层次的作曲抽象，因此选择了针对一个现有的音乐软件合成系统。通过重用现有的音乐软件系统，我们可以利用已有的解决方案，并更密切关注我们的作曲兴趣。

尽管基于 MIDI 的乐器和软件无处不在且广受欢迎，但由于若干原因放弃了这个选项。首先，由于 MIDI 是一种二进制协议，这使得针对它的软件开发比基于文本的协议更复杂。处理 MIDI 需要非常熟悉规范，或者直接为其作曲，或者使用一种在协议开发之上添加更高层次抽象的 MIDI 编程语言。这些做起来都不困难，但有更简单的替代方案。

除了协议是二进制的之外，MIDI 规范在音乐表达能力也有局限性，无法满足管弦乐作曲库的需求。MIDI 中的大多数值被定义为 0–127 的七位范围，这对于表达我们所需的细微差别来说太粗糙了。

## 683 弦乐作曲的建模

任意定义每个乐器允许的 p 字段（p-fields）这种灵活性是以兼容性为代价的。如果不同的乐器使用的 p 字段数量和含义不同，为一个乐器编写的 SCO 就无法重用于另一个乐器，因此，用于一个乐器的编程库也无法用于另一个乐器。那么，解决这个问题的方案是定义一个标准的 p 字段签名，使其既能处理弦乐作曲库的音乐需求，又能被所有 Csound 乐器实现。通过使用我们共同认可的标准格式，我们可以创建出接受该格式信息的乐器，以及一个可以生成该格式的编程库。结果是，不同的乐器可以在项目中进行切换，生成结果的程序也可以进行切换。

对于弦乐作曲库，我们将使用能够接受 8 个 p 字段格式的乐器，其取值如下：

- `p1`—乐器标识符

- `p2`—开始时间

- `p3`—持续时间

- `p4`—音高 1（频率或 Csound PCH 记法之一）

- `p5`—音高 2（频率或 Csound PCH 记法之一）

- `p6`—以 dB 为单位的幅度

- `p7`—空间位置（从 –1.0 到 1.0，对应左右声位平衡）

- `p8`—发音法（幅和滤波器包络的类型，可以是 0 或 ADSR 包络，1 为三角形包络，或 2 为渐变包络）

这种八字段格式的注释将足够灵活，能够处理下面提供的示例的作曲需求。`p4` 和 `p5` 字段被示例乐器用于指示起始音高和结束音高，尽管所使用的乐器可能会实现对值的其他替代解释（例如，音高 1 可以被解释为基础音高，而音高 2 可以被解释为颤颤音的装饰音高）。`p6` 字段将用于输入要播放音符的幅度。

`p7` 字段的有趣之处在于，在非计算机音乐设置中，空间位置通常不是播放音符的因素，而是表演者的特质。在我们可能需要处理乐器生成的音频信号而不是将任务委托给 Csound 等其他软件的音乐系统中，我们拥有一种编程模型：`Performer` 对象的方法由生成带有空间位置属性的 `Audio` 组成，并将处理后的声音返回给声音引擎。然而，由于音频处理任务已被委托，将在音符的参数中传递空间位置的值，乐器将对信号应用空间位置处理。我们稍后会发现，虽然系统中的每个音符都会携带该信息，但库的用户不需要手动注释信息，而是在 `Performer` 对象上配置属性，然后 `Performer` 对象将在生成音符时将填充该信息。

在示例 Csound 乐器中设置的 `p8` 字段接受 0、1 和 2 的值，分别代表标准“攻击-衰减-维持-释放”（ADSR）包络、金字塔包络和渐变包络。发音法字段的灵活性在于，如果弦乐作曲库的用户想要扩展乐器以包含更多发音法，用户可以在乐器的编程中实现这一点，而无需对编程库进行任何更改。

通过将音频处理任务委托给 Csound，我们可以在弦乐作曲库中发现更高层次的音乐抽象。从我们的库与 Csound 交互只需要我们能够生成 Csound 能理解的 SCO 格式的文本文件。通过将 p 字段音符格式作为我们库的输出和乐器设计的输入标准，我们创建了一个允许使用不同乐器尝试不同音乐想法的系统。

# 14.4 设计编程库

在决定使用 Csound 作为我们弦乐作曲模型中的乐器部分，并建立了与 Csound 通信的手段（使用 SCO 格式的文本输出）之后，我们现在将通过定义几个类并建立使用这些类的约定（使其与弦乐作曲的约定并行），对我们观察到的弦乐作曲的其他因素进行建模。

尽管这里的类库是为 Csound 设计的，但通用的整体设计和架构适用于不同的音乐数据表示，如 MIDI、OSC 或用户可能需要构建的任何自定义音乐。

## 14.4.1 Note（音符）

`Note` 类用于表示给表演者的音符信息。它的设计使得当使用此类类记谱音乐想法时，用户仅需定义音乐片段固有的基本音乐参数，省略与表演者无关的参数：即将用哪种乐器演奏此 `Note`，以及生成的声音的空间位置将会在处。在声学音乐中，记谱谱被交给表演者进行表演。表演者反而在分配给他们的乐器上演奏音乐；空间位置取决于他们坐的位置。如果给同一个表演者一个可以演奏该记谱音乐的类似乐器，该表演者可以使用不同的乐器演奏相同的音乐以获得不同的结果。同样，给定相同的音乐和乐器但移动另一个位置，表演者将产生不同的最终结果。这就是空间位置和分配的乐器属性属于我们的 `Performer` 类而不是 `Note` 类的原因的原因。

然而，由于决定使用 Csound 并使用定义乐器编号和空间位置（`p1` 和 `p7`）的文本格式，我们需要最终将 `Note` 类转换为字符串格式。我们通过让 `Note` 类包含空间位置来实现此。以下是 `Note` 的头文件定义：

```cpp
class Note {
public:
    float startTime;
    float duration;
    float pitch;
    float pitch2;
    float amp;
    int envType;
    bool isRest;

    Note(float startTime, float duration, float pitch, float pitch2, float amp, int envType);
    // 此构造函数用于休符
    Note(float startTime, float duration);

    string getNote(int instrumentNum);
};
```

`Note` 有七个成员变量，其中六个映射到 Csound 格式，一个用于判断是否为休符：

- `startTime`—开始时间 (`p2`)

- `duration`—持续时间 (`p3`)

- `pitch`—起始音高 (`p4`)

- `pitch2`—结束音高 (`p5`)

- `amp`—以 dB 为单位的幅度 (`p6`)

- `envType`—使用的包络 (`p8`)

- `isRest`—是否为休符

`Note` 的两种构造形式取决于用户指示的是普通音符还是休符。当构造普通音符时，`Performer` 和 `PerformerGroup` 对象将获取 `Note` 数据并创建 Csound 文本。当构造休符时，它将不会生成任何 Csound 文本，而是用于增加时间。`getNote` 方法用于生成 `Note` 的字符串表示，并将输出到 SCO 文件。库的用户通常不会自己调用该方法，而是由 `Performer` 类用于辅助表演该音符。

## 14.4.2 Performer（表演者）

`Performer` 类代表我们弦乐作曲模型中的表演者。以下是 `Performer` 类的头文件定义：

```cpp
class Performer {
  public:
    string name;
    int instrumentNum;
    float space;
    float baseAmp;

    Performer(int instrumentNum, float baseAmp, float space, string name);

    string toString();

    string perform(vector<Note> noteList, float startTime);

    string performAleatorically(vector<Note> noteList,
      float timeVariance, float ampVariance,
      float pitchVariance, float durationOfSection,
      float startTime);
};
```

`Performer` 类 `Performer`

`Performer` 类有四个成员变量，作为 `Performer` 对象构造方法的参数配置：

`string name`—用于引用和调试

`int instrument`—映射到 Csound 乐器 ID（此库仅支持数字乐器 ID）

`float space`—表示表演者将所处的声场位置（−1.0 = 左侧，0.0 = 中心，1.0 = 右侧）

`float baseAmp`—表演者应用于给定的音符幅度的浮点乘法值（0.0–1.0）；这是在深度意义上表示空间的简便方式（即考虑到它们彼此之间的音量相同，表演者

在舞台靠后处与舞台靠前的人演奏相同的音乐和相同的乐器，其声音通常没有舞台靠前处的大。

`Performer` 对象还有三个方法：

- `toString()`—一个用于显示表演者属性的工具方法，对调试构图项目非常有用

- `perform(vector<Note> noteList, float startTime)`—`Performer` 类的主要表演方法，用于给 `Performer` 对象一段音乐进行表演，生成 Csound 性能信息 (SCO)

- `performAleatorically(...)`—一种表演方法，用于在给定的开始时间和持续时间内，以偶然（aleatoric）的方式表演一段音乐，并根据提供的修饰参数对参数进行随机化。

`Performer` 类的表演方法代表了表演者理解如何执行的表演技术。库的用户将使用 `Notes` 向量（vector）来创建和配置音乐思想，然后让 `Performers` 在给定时间定义这些音乐思想。通过定义音乐材料并分离整个区块待执行的时间，我们获得了重用相同材料并在不同时间进行表演的能力。这与音乐的一般构思方式相似，即“该段动机在此时此刻演奏，在那个时间再次演奏。”

### 4.4.3 PerformerGroup

`Performer` 类代表我们交响乐构图模型中的表演者组。以下是 `PerformerGroup` 类的头定义：

```cpp
class PerformerGroup {
  public:
    string name;
    vector<Performer *> performers;

    PerformerGroup(string name);

    string toString();

    string perform(vector<Note> noteList, float startTime);
    string performAleatorically(vector<Note> noteList,
        float timeVariance, float ampVariance,
        float pitchVariance, float durationOfSection,
        float startRange);

    string performSurface(float amp, int envType,
        float timela, float pchla,
        float time1b, float pch1b,
        float time2a, float pch2a,
        float time2b, float pch2b);
```

表演者组有两个成员变量：

- `string name`—用于引用和调试

- `vector<Performer *> performers`—持有了要放入此组的 Performers 引用；使用指针使得不同的组可以共享同一个 Performformer 的引用。

表演者对象有四个方法：

- `string toString()`—一个用于显示表演者组属性的工具方法，对调试概念项目非常有用

- `string perform(vector<Note> noteList, float startTime)`—调用组中的所有表演者在开始时间执行给定的 noteList

- `string performSurface()...`给定表面的边界参数，计算组中每个表演者将执行的、且独特的滑音（glissandi），以创建组的滑音音乐表面

表演者组的表演方法建立在单个表演者的可用表演方法之上：组作为一个对象本身不执行任何表演。组表演方法使用一对多的关系，即作曲家为组注明一个思想，然后该组将其解释为针对每个表演者的指令。结果是，使用该库可以专注于标注一个将由组表演的音乐思想，而无需逐个标注和指导每个表演者执行具体内容。这允许用户继续使用抽象思想进行工作，并委托库将组指令转换为组内每个表演者的具体指示。

## 14.5 使用库进行构图

使用交响乐构图库的通用步骤与为现场管弦乐队作曲非常相似（见表 14.2）。

通常情况下，作曲家使用交响乐构图库处理音乐思想的方式与其为现场管弦乐队标注乐谱的方式类似。使用交响乐构图库的一个优势是，为现场管弦乐队标注需要为每个表演者写出线条，即使该音乐思想是一个单一的组音并被构思为一个单一思想。使用交响乐构图库，单一的组思想可以作为一个单一实体被标注和处理，而不是不断地分部。

| 为现场管弦乐队作曲 | 使用管弦乐库作曲 |

| :--- | :--- |

| 决定乐曲使用哪些乐器（木管、铜管、弦乐、打击乐、电子）， | 决定乐曲使用哪些 Csound 乐器并将它们放置在 Csound 管弦乐队 (ORC) 文件中。 |

| 在乐谱开头，定义并布局所选乐器的结构（某些方面可能没有显式定义，导致指挥家在表演时进行选择） | 创建一个 C++ 程序使用管弦乐库，并定义所选乐器的数量和布局，通过创建实例以及可选地将其分组为 `PerformerGroup` 对象来实现 |

| 根据表演者的指令注明一份由表演者执行的完整乐谱，给出演奏时间和要使用的技术；扩展表演技术的指令定义在乐谱开头。 | 在 C++ 中，对 `Performer` 和 `PerformerGroup` 对象调用表演方法并传入数据或其他参数；调用不同的方法等同于为不同的表演技术作曲，编写程序等同于为现场管弦乐队标注的乐谱；作曲家可以通过向 Perform 或 PerformerGroup 类添加方法来定义新的表演技术。 |

| 使用管弦乐队演奏乐谱，使用指挥驱动表演；此时表演者将指令解释为物理动作，用他们的乐器创建最终结果。 | 运行程序生成 Csound 乐谱 (SCO) 文件，该文件将作为管弦乐队的表演指令；在 ORC 和 SCO 中运行 Csound 乐器以创建最终结果。 |

## 691 弦乐合的建模

```cpp
groupD.performers.push_back(&d2);
groupD.performers.push_back(&d3);
```

********************

/* 音乐示例 */

********************

* 示例 1 - 直接使用音符

```cpp
Note direct(0, 1, 8.00, 8.00, 80, 0);
Note directCopy = direct;
directCopy.startTime = 1.00;
directCopy.pitch = 9.00;
directCopy.pitch2 = 9.00;
cout << direct.getNote(1, 0) << endl;
cout << directCopy.getNote(1, 0) << endl;
```

* 示例 2 - 使用执行者和执行者方法

* 执行者方法数据 *

// 定义音符数据

Note a (0, 1, 8.00, 80, 00);

```cpp
vector<Note> noteList;
noteList.push_back(a);
noteList.push_back(Note(1, 1, 8.04, 8.04, 80, 00));
noteList.push_back(Note(2, 1, 8.07, 8.07, 80, 00));
noteList.push_back(Note(3, 1, 9.00, 9.00, 80, 00));
noteList.push_back(Note(0, 3));
```

// 执行音符数据

```cpp
cout << "开始管乐队输出" << endl;
cout << "测试音符" << endl;
cout << a.getNote(1, 0.0) << endl;
cout << "测试执行者" << endl;
cout << a1.toString() << endl;
cout << a1.perform(noteList, 5.00) << endl;
cout << a2.toString() << endl;
cout << a2.perform(noteList, 10.0);
cout << a3.toString() << endl;
cout << a3.perform(noteList, 15.0);
```

## 第 14 章

```cpp
cout << endl << "测试执行者组" << endl << endl;
cout << groupA.toString() << endl;
cout << groupA.perform(noteList, 20.0) << endl;
```
