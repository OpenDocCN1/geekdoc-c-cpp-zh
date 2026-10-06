
其中初始化函数的参数取决于具体的库。它可能包括采样率、采样大小和格式、通道数，以及选择 WAV 还是 AIFF 或声卡。另外两个函数的返回值用于错误检查。假值（即零）将意味着失败了.¹¹⁹

在例示例中，我们将使用并适配 Richard Ports 的 Port。库接口中的相关函数是 `psf_sndCreate`、`psf_sndWriteFloatFrames` 和 `psf_sndClose`。输出由一个 `int` 表示。此外，必须通过调用 `psf_init` 初始化库。

现在我们就可以开始编写代码了。文件格式固定为标准的单声道 WAV。采样率必须来自我们一直使用的变量 `sr`。我决定使用 16 位样本，因为长期以来一直都是这样。这引入了一个微小的困难：浮点样本的“自然”范围是 –1 到 +1，而 16 位样本的等效范围是 –32,768 到 +32,767。我们将在输出函数内部通过缩放来处理这个问题。如果在稍后的某个阶段决定支持其他采样大小，则必须重新审视这段代码。为了实现这些想法，我们可以定义：

```c
typedef OUTPUT int; /* For Portsf library */
```

```c
OUTPUT initialize_sound(char *name, int sr)
{
  PSF_PROPS inprops;
  inprops.srate = (long)sr;
  inprops.chans = 1L;
  inprops.samptype = PSF_SAMP_16;
  inprops.format = PSF_STDWAVE;
  inprops.chformat = MC_MONO;
  return psf_sndOpen(name, &inprops, 0);
}
```

```c
int output_sample(OUTPUT out, double sample)
{
  short buffer[1];
  buffer[0] = (short)(sample*32767.0);
  if (psf_sndWriteShortFrames(out, buffer, 1) != 1L)
    return 0;
  return 1;
}
```

```c
int close_sound(OUTPUT out)
{
  psf_sndClose(out);
  return 1;
}
```

并且我们需要在主程序中调用 `psf_init`。在主程序结束时调用 `close_sound` 函数也是一个好主意，以确保声音写入磁盘（如果我们使用更高级的库，则写入输出设备）。

## 用户界面

整个程序我们一直忽略的一个方面是程序的用户将如何指定使用哪种波形、以什么速度播放以及播放多长时间。当这些信息被指定时，我们就知道如何使用之前开发的程序来处理它们。这个方面通常被称为用户界面。在某些方面，这非常重要；它是程序对社区而言最明显的部分。它的风格是人们记忆的。但在另一个方面，它是最不重要的部分。它不产生任何作用，不解决问题，而且计算上非常简单。

我们可以将用户界面比作一段乐曲的结尾。它可能是某些观众记得的部分，因此必须运用技巧，但那（通常）并不是最重要的部分。

用户界面有两种根本上不同的方法：命令行方法和图形方法。传统上，前者受计算机专业人士青睐，后者受消费者喜爱。从我们的角度来看，设计这个简单程序的图形用户界面（GUI）要复杂得多，而且如果我们打算实现跨平台或保持中立，这会引入许多我们不愿面对的问题。我们将开发一个命令行系统，然后简要考虑如何使用工具将其适配到 GUI。

### 4.3.1 命令行接口

在设计用户界面时，可以使用相同的技术。我们已经说过，程序的用户将指定使用哪种波形、以什么速度播放以及播放多长时间。这识别出三个必须定义的实体：波形、速度和长度。对于这些每一个，我们都可以考虑可能期望的值类型：浮点数、字符或字符串。

## 第 4 章

查看它描述的是哪个参数。这段代码对于大多数 UNIX 传统的程序员来说非常熟悉：

```c
double duration = 3.0;
double speed = 440.0;
char *output = NULL;
char *wavename = NULL;
int formula = -1;
enum ARG_RES = {WAVEFORM_GIVEN, FORMULA_GIVEN};
typedef enum ARG_RES ARG_RES;
```

```c
ARG_RES decode_arguments(int argc, char **argv) {
    int i = 0;
    char *a = argv[0];
    while (--argc) {
        a = argv[i];
        if (a[0]=='-') { /* 找到标签 */
            switch (a[1]) {
                case 'w': /* 波形 */
                    if (argc == 0) {
                        printf("No waveform argument\n"); exit(1);
                    }
                    wavename = argv[i+1];
                    i += 2;
                    break;
                case 'f':
                    if (argc == 0) {
                        printf("No formula argument\n"); exit(1);
                        formula = SINE;
                    } else if (strcmp(argv[i+1], "sine")==0)
                        formula = SINE;
                    } else if (strcmp(argv[i+1], "cosine")==0)
                        formula = COSINE;
                    else {
                        printf("No valid formula name\n"); exit(1);
                    }
                    i += 2;
                    break;
                case 's':
                    if (argc == 0) {
                        printf("No speed given\n"); exit(1);
                    }
                    speed = atof(argv[i+1]);
                    i += 2;
                    break;
                case 't':
                    if (argc == 0) {
                        printf("No duration given\n"); exit(1);
                    }
                    duration = atof(argv[i+1]);
                    i += 2;
                    break;
                case 'o':
                    if (argc == 0) {
                        printf("No output argument\n"); exit(1);
                    }
                    output = argv[i+1];
                    i += 2;
                    break;
                else:
                    printf("No tag found\n"); exit(1);
            }
        }
    }
    /* 现在进行空值检查 */
    if (output == NULL) {
        printf("No output file given\n"); exit(1);
    }
    if (waveform == NULL && formula == -1) {
        printf("Neither waveform nor formula specified\n"); exit(1);
    }
    if (waveform != NULL && formula != -1) {
        printf("Both waveform and formula specified\n"); exit(1);
    }
    if (waveform == NULL) return FORMULA_GIVEN;
    else return WAVEFORM_GIVEN;
}
```

该函数有多种形式。一种常见的接口是允许使用 `-t0` 或 `-t10`。修改程序以允许这种格式并不困难，你可能想思考如何实现它。

### 4.3.2 图形用户界面

图形用户界面的主要问题是，每个平台处理和支持图形的方法都不同。克服这一点的方法之一是使用不同的编程系统，一种完全为处理用户界面而设计的系统。这类系统较少；在许多方面最简单的是 Tcl/Tk.24。该语言运行较慢，在某些人看来，它产生的界面相当简单且单调。尽管如此，创建一个原型界面是非常容易的，如果我们已经有了完整的命令行界面，就可以使用 Tcl/Tk 来调用现有的程序。25

下面的片段提供了一个表单，用户可以在其中输入波形名称、选择公式并提供持续时间和速度。该表单通过合适的命令调用我们开发的程序。我们假设程序调用如下：

```tk
message .title -width 10 -justify center "Waveform Interface"
pack .title
radbutton f0 -text "none" -variable formula 0
radbutton f1 -text "sine" -variable formula 1
radbutton f2 -text "cosine" -variable formula 2
pack .f0 .f1 .f2
message .w -width 10 -justify center "waveform"
entry .w -width 25 -relief sunken -variable waveform
pack .w
message .o -width 10 -justify center "output"
entry .o -width 25 -relief sunken -variable output
pack .o
message .s -width 10 -justify center "speed"
entry .s -width 25 -relief sunken -variable speed
pack .s
message .t -width 10 -justify center "duration"
entry .t -width 25 -relief sunken -variable duration
pack .t
button .ok -text "OK" -command do_it
button .bad -text "Exit" -command exit
pack .ok left
pack .bad right
```

```tk
proc do_it () {
  global formula; global waveform
  global output; global speed; global duration
  set cc(0) "waveform"
  set cnt 1
  if {$formula == 1} {
    set cc(1) "-f"
    set cc(2) "sine"
    set cnt 3
  } else {
    if {$formula == 2} {
      set cc(1) "-f"
      set cc(2) "cosine"
      set cnt 3
    }
  }
  if {$waveform != ""} {
    set cc(cnt) "-w"
    incr cnt
    set cc(cnt) "$waveform"
    incr cnt
  }
  if {$output != ""} {
    set cc(cnt) "-o"
    incr cnt
    set cc(cnt) "$output"
    incr cnt
  }
  if {$speed != -1} {
    set cc(cnt) "-s"
    incr cnt
    set cc(cnt) "$speed"
    incr cnt
  }
  if {$duration != -1} {
    set cc(cnt) "-t"
    incr cnt
```
