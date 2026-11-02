
```cpp
// Get the discrete state of the cell
state_t getState() const { return s; }
protected:
    // This is the rule for computing the cell’s next state
    virtual state_t cell_rule(state_t left, state_t right, state_t s) = 0;
private:
    state_t s;
    const int location;
};

#endif
```

*CellularAutomaton* 类派生自仿真引擎的 *Network* 类，包含一个 *Cell* 对象数组。一个细胞的输出会发送给它的两个邻居：位置 *i* 处的细胞输出会发送到位置 *i + 1*（右）和 *i − 1*（左）处的细胞。数组两端两个细胞的输出可以被丢弃，或者发送到另一端的细胞。该数组初始为空，细胞通过 *placeCell* 方法显式分配到各自的位置。*CellularAutomaton* 类的源代码如下所示。

## CellularAutomaton 类

```cpp
#ifndef CellularAutomaton_h
#define CellularAutomaton_h
#include "Cell.h"

class CellularAutomaton: public adtss::Network<IO_Type>
{
public:
    // Create an automaton with space for size cells
    CellularAutomaton(int size, bool ring):
        adtss::Network<IO_Type>(),
        size(size),ring(ring)
    {
        cell = new Cell*[size];
        for (int i = 0; i < size; i++) cell[i] = NULL;
    }
    void getComponents(adtss::Set<adtss::Dtss<IO_Type> >* c)
    {
        for (int i = 0; i < size; i++) c->insert(cell[i]);
    }
    void route(const IO_Type& value, adtss::Dtss<IO_Type>* model,
        adtss::Bag<adtss::Event<IO_Type> >& r)
    {
        adtss::Event<IO_Type> x;
        x.value = value;
        // Get the positions of the cells to the left and right
        int left = value.src - 1, right = value.src + 1;

        // Wrap the left end of the automaton to form a ring
        if (left < 0 && ring) {
            x.value.src = size;
            x.model = cell[size-1];
            r.insert(x);
        }
        // or just send the event to the left
        else if (left >= 0) {
            x.value.src = value.src;
            x.model = cell[left];
            r.insert(x);
        }

        // Wrap the right end of the automaton to form a ring
        if (right == size && ring) {
            x.value.src = -1;
            x.model = cell[0];
            r.insert(x);
        }
        // or just send the event to the right
        else if (right < size) {
            x.value.src = value.src;
            x.model = cell[right];
            r.insert(x);
        }
    }

    // The destructor destroys the Cells too
    ~CellularAutomaton()
    {
        for (int i = 0; i < size; i++)
            delete cell[i];
        delete [] cell;
    }
    // The placed cell is adopted by the CellularAutomaton
    void placeCell(Cell* new_cell)
    {
        new_cell->setParent(this);
        if (cell[new_cell->getLocation()] != NULL)
            delete cell[new_cell->getLocation()];
        cell[new_cell->getLocation()] = new_cell;
    }

private:
    int size;
    bool ring;
    Cell** cell;
};

#endif
```

**表 3.3** 描述细胞状态转移函数的位

| 左、状态、右 | 位 |
|---|---:|
| *bbb* | 7 |
| *bbw* | 6 |
| *bwb* | 5 |
| *bww* | 4 |
| *wbb* | 3 |
| *wbw* | 2 |
| *wwb* | 1 |
| *www* | 0 |

我们可以通过从 *Cell* 类派生新类，一次创建一个细胞类型。每个细胞将三个二进制值——左输入、状态和右输入——映射为一个二进制值——下一状态。状态转移函数完全由 2³ 种情况定义：每种输入和状态的组合对应一种情况。如果将每种细胞类型编码为一个新类，则需要 2⁸ 个类。

更紧凑的解决方案是创建一个名为 *BinaryCell* 的类，其构造函数接受一个编码所需行为的字节。规则在 8 位中的编码如表 3.3 所示。使用这种编码，规则通过右移位来实现：左邻居为黑色时移 4 位，状态为黑色时移 2 位，右邻居为黑色时移 1 位，状态和邻居为白色时移 0 位。移位后，模型的下一状态由最低有效位给出。该类的实现如下所示。

## BinaryCell 类

```cpp
#ifndef BinaryCell_h_
#define BinaryCell_h_
#include "Cell.h"

class BinaryCell: public Cell
{
    public:
        BinaryCell(state_t s0, int location, unsigned char rule):
            Cell(s0,location),rule(rule) {}
    protected:
        state_t cell_rule(state_t left, state_t right, state_t s)
        {
            // Calculate the number of bit shifts
            unsigned char shift = 0;
            if (left == BLACK) shift += 4;
            if (s == BLACK) shift += 2;
            if (right == BLACK) shift += 1;
            // Extract the outcome
            if ((rule >> shift) & 0x01) return BLACK;
            else return WHITE;
        }
    private:
        const unsigned char rule;
};
#endif
```

仿真程序从命令行接受四个参数：要使用的细胞数量、要仿真的代数、编码转移函数的一个字节，以及指示细胞形成环还是线的标志。如果选择线，则线边缘之外的空白区域颜色为白色。使用 EventListener 在细胞状态改变时更新显示，并将最终图像保存到文件中。创建元胞自动机时，中心有一个黑色细胞，其他细胞为白色。主仿真程序如下所示。

## 主仿真程序

```cpp
#include "CellularAutomaton.h"
#include "Display.h"
#include "BinaryCell.h"
using namespace std;

// The event listener displays the state of the cells when it changes
class CellListener: public EventListener<IO_Type>
{
  public:
    // Create display for the simulation
    CellListener(int num_cells, int num_generations):
        display(Display::initializeDisplay(num_cells,num_generations)){}
    // Draw the state of a cell to the off-screen buffer
    void showState(const Cell* cell, int gen)
    {
        // Draw a white cell (red = green = blue = 255)
        if (cell->getState() == WHITE)
            display.setColor(cell->getLocation(),gen,255,255,255);
        // or draw a black cell (red = green = blue = 0)
        else display.setColor(cell->getLocation(),gen,0,0,0);
    }
    // Update the screen
    void update() { display.redraw(); }
    // The listener ignores output events
    void outputEvent(Event<IO_Type>, unsigned int){}
    // Update the appearance of the cell when its state changes
    void stateChange(Atomic<IO_Type>* model, unsigned int t)
    {
        Cell* cell = dynamic_cast<Cell*>(model);
        showState(cell,t);
    }
    // Save the image to a file
    void saveImage() { display.toBmp("image.bmp"); }
  private:
    Display& display; // Reference to the display
};

int main(int argc, char** argv)
{
    // Get the number of generations to run the simulation
    if (argc != 5) {
        cout << "Requires # cells, # generations, rule #, and ring | line"
             << endl;
        return 0;
    }
    // Get the model parameters from the command line
    int num_cells = atoi(argv[1]);
    int num_gens = atoi(argv[2]);
    unsigned char rule = atoi(argv[3]);
    bool ring = (strcmp(argv[4],"ring") == 0);
    // Create the display
    CellListener* listener = new CellListener(num_cells,num_gens);
    // Create the cellular automaton
    CellularAutomaton* automaton = new CellularAutomaton(num_cells,ring);
    // Create the cells with a black one at the center and all others white
    for (int i = 0; i < num_cells; i++) {
        // Create and initialize the cell
        state_t s0 = WHITE;
        if (i == num_cells/2) s0 = BLACK;
        Cell* cell = new BinaryCell(s0,i,rule);
        // Display it
        listener->showState(cell,0);
        // Add it to the automata
        automaton->placeCell(cell);
    }
    // Run the simulation
    Bag<Event<IO_Type> > empty_input; // This is a closed system
    Simulator<IO_Type>* sim = new Simulator<IO_Type>(automaton);
    sim->addEventListener(listener);
    for (int i = 0; i < num_gens; i++) {
        // Display the output
        listener->update();
        // Compute the next state
        sim->computeNextState(empty_input);
    }
```
