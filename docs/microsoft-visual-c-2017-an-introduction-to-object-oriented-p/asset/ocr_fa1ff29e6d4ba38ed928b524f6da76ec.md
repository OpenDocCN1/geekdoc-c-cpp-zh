In summary, the Visual Studio version of the ThreeLinesOutput provides everything you need to run the program and saves you as much typing as possible in case you want to include additional options. The command-line and Visual Studio versions of the program function identically.

| Notepad version of the program | Visual Studio version of the program |
|--- |--- |
| using static System.Console; | using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using static System.Console;
namespace ThreeLinesOutput
| class ThreeLinesOutput | class Program
| static void Main() { static void Main(string[] args) {
| { WriteLine("Line one"); | { WriteLine("Line one");
| WriteLine("Line two"); | WriteLine("Line two");
| WriteLine("Line three"); | WriteLine("Line three");
| } } | } } |

**Figure 1-14** Comparing the command line and Visual Studio versions of the ThreeLinesOutput

# Deciding Which Environment to Use

When you write, compile, and execute a C# program, you can either use a text editor or the command line, or you can use the Visual Studio IDE. You would never need to use both. You might prefer using an editor with you are already familiar (such as Notepad) and compiling from the command line because only two files are generated, saving disk space.

On the other hand, the IDE provides many useful features, such as automatic statement completion. For example, if you type `u`, a list of choices including using is displayed and you can click `using` instead of typing it. Similarly, if you use `s`, then a list of choices is displayed

Additionally, in the IDE, words are displayed using different colors based on their category; for example, one color is used for C#-reserved words and a different color