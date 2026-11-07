

```cpp
// check for collision with right Paddle
if ( ( ballPosition.y - RADIUS ) <=
     ( rightPaddlePosition.y + ( PADDLE_HEIGHT / 2 ) ) &&
     ( ballPosition.y + RADIUS ) >=
     ( rightPaddlePosition.y - ( PADDLE_HEIGHT / 2 ) ) )
{
    reverseHorizontalDirection(); // reverse the ball's direction

    // place the Ball at the edge of the Paddle
    nodePtr->setPosition(
        rightPaddlePosition.x - ( PADDLE_WIDTH / 2 ) - RADIUS,
        ballPosition.y, ballPosition.z );
} // end if
} // end else
} // end function hitPaddle
```

**图 27.8** | Ball 类成员函数定义。（第 4 部分，共 4 部分。）

第 31 行设置用于给 Entity 着色的材质。参数“ball”是用于给 Ball 着色的材质名称。在 Ogre 中，材质通常通过脚本创建，不过也可以直接在程序中创建。材质脚本（图 27.9）是 Ogre 用来创建材质的文本文件。请将该文本文件保存为 .material 扩展名。

```text
// ball material definition
material ball
{
    // define one technique for rendering the Ball
    technique
    {
        // render the Ball in one pass
        pass
        {
            // color the Ball violet
            ambient 0.58 0 0.827
            diffuse 0.58 0 0.827
            specular 0.58 0 0.827 120
        }
    }
}
```

**图 27.9** | ball 材质脚本。

注意，ball 材质的结构与 C++ 代码类似，每个部分都用花括号括起来。第 2 行表明我们正在定义一个名为 ball 的材质。在材质内部，我们定义一种 technique——即如何渲染对象（第 5—15 行）。可以为一种材质定义多种 technique，但这超出了本书范围。在每种 technique 内，定义了一个或多个 pass（第 8—14 行）。每个 pass 定义材质渲染过程中的一个步骤。使用多个 pass 也超出了本书范围。颜色是在 pass 中通过为场景中不同类型的光照设置颜色值来确定的。我们希望 Ball 呈紫色，因此将颜色值设置为 (0.58, 0, 0.827)（第 11—13 行）。每种光照类型（ambient、diffuse 和 specular）后面的数字表示颜色值。specular 中的第四个数字（120）决定 Ball 的光泽程度。它可以是任何大于 0 的值。值越高，对象看起来越有光泽。

注意，“ball”不是定义该材质的文件名称，而是该文件内材质的名称。一个材质文件可以定义多个材质。同一个材质可用于多个 Entity 对象，但定义的每个材质都必须具有唯一名称。

我们已经为 Ball 创建了 Entity，但它尚未成为场景的一部分。第 33—35 行（图 27.8）将其添加到场景中，以便它能在屏幕上渲染。我们使用 SceneManager 创建一个 SceneNode——场景图中的一个 Node，它保存关于对象及其在场景中位置的信息（无论可见与否）。一个 SceneNode 可以挂接许多子 SceneNode，但只能有一个父 Node。参数“Ball”是 Ogre 引擎中引用该 SceneNode 时使用的名称。场景图中的每个 SceneNode 都必须具有唯一名称。调用 getRootSceneNode 会获取场景图中的最顶层节点。根节点是所有其他节点的父节点。创建根节点的子节点时，其初始位置为 (0, 0, 0)。第 35 行将表示 Ball 的 Entity 挂接到新创建的 SceneNode 上。Ball 现在已成为场景的一部分，并会被渲染。注意，用于将 Ball 添加到场景的所有函数都是 SceneManager 的成员函数。这就是 Ball 构造函数将指向 SceneManager 的指针作为参数的原因——Ball 对象必须能够访问 SceneManager，以便将自己添加到场景中。

Ogre SDK 提供的球体网格半径为 100。这比我们需要的尺寸大得多。第 36 行更改挂接到 SceneNode 的 Entity 的大小，但不会影响该节点的 Entity 所基于的实际网格大小。我们为每个轴（x、y 和 z）提供一个缩放因子。我们将 .05 作为所有三个轴的缩放因子。对所有三个轴使用相同缩放因子会均匀缩放网格，从而保持其原始形状。该函数将球体在每个轴上的半径乘以缩放因子，从而将半径从 100 改为 5。缩放网格时，光照效果会有些失真。我们通过让 Entity 在每次缩放时计算网格的新法线来修正这一点（第 32 行）。[注意：在 Ogre 1.6（Shoggoth）中，该函数不存在——此操作会自动执行。你需要注释掉或删除这一行以及其他文件中的类似行，才能使示例编译。] 这里的法线指的是对象表面的每个面片（即小区域）所朝向的方向。如果面片朝向光源，它就更亮。如果它背向光源，就更暗。

还有一个 scale 函数可以更改 Entity 的大小。区别在于，scale 基于当前大小更改尺寸，而 setScale 基于节点的原始大小更改尺寸。这些函数还会按相同因子缩放 SceneNode 的所有子节点。可以通过告知父节点的每个子节点，在父节点缩放时不希望其被缩放来改变这一点——为此，请调用 setInheritScale 函数并向它传递 false。

## 添加球拍

Paddle 类（图 27.10—27.11）表示球拍。我们将 Paddle 添加到场景的方式与添加 Ball 非常相似。成员函数 addToScene（图 27.11，第 23—34 行）使用相同的前五个 Ogre 函数，但参数不同。

```cpp
// Paddle.h
// Paddle class definition (represents a paddle in the game).
#ifndef PADDLE_H
#define PADDLE_H

#include <Ogre.h> // Ogre class definitions
using namespace Ogre;

class Paddle
{
public:
    // constructor
    Paddle(SceneManager *sceneManagerPtr, String paddleName,
           int positionX );
    ~Paddle(); // destructor
    void addToScene(); // add a Paddle to the scene
    void movePaddle( const Vector3 &direction ); // move a Paddle

private:
    SceneManager* sceneManagerPtr; // pointer to the SceneManager
    SceneNode *nodePtr; // pointer to a SceneNode
    String name; // name of the Paddle
    int x; // x-coordinate of the Paddle
}; // end of class Paddle

#endif // PADDLE_H
```

**图 27.10** | Paddle 类定义（表示游戏中的球拍）。

```cpp
// Paddle.cpp
// Paddle class member-function definitions.
#include <Ogre.h> // Ogre class definitions
#include "Paddle.h" // Paddle class definition
using namespace Ogre;

// constructor
Paddle::Paddle( SceneManager *ptr, String paddleName,
                int positionX )
{
    sceneManagerPtr = ptr; // set the pointer to the SceneManager
    name = paddleName; // set the Paddle's name
    x = positionX; // set the Paddle's x-coordinate
} // end of Paddle constructor

// destructor
Paddle::~Paddle()
{
    // empty body
} // end Paddle default destructor
```

**图 27.11** | Paddle 类成员函数定义。（第 1 部分，共 2 部分。）

```text
// paddle material definition
material paddle
{
    // define one technique for rendering a Paddle
    technique
    {
        // render a Paddle in one pass
        pass
        {
            // color the Paddle dark orange
            ambient 1 0.549 0
            diffuse 1 0.549 0
            specular 1 0.549 0 120
        }
    }
}
```

**图 27.12** | Paddle 材质脚本。

## 添加墙壁

现在我们要添加一个盒子，其中包含弹跳的 Ball 和移动的 Paddles。我们在 Pong 类的 createScene 函数中创建这个盒子（图 27.5，第 128—168 行）。四面墙都使用 Ogre SDK 提供的同一个立方体网格——通过适当缩放墙壁来形成盒子，并重新计算法线以进行光照。墙壁添加到场景的方式与 Ball 和 Paddles 类似。我们使用立方体网格创建一个 Entity 来表示每面墙。我们使用一个简单材质将所有墙壁着色为青色（图 27.13）。该材质脚本看起来与我们见过的另外两个材质脚本相同，只是名称和颜色值不同。

```cpp
// wall material definition
material wall
{
    // define one technique for rendering a wall
    technique
    {
        // render a wall in one pass
        pass
        {
            // color the wall cyan
            ambient 0 0.545 0.545
            diffuse 0 0.545 0.545
            specular 0 0.545 0.545 120
        }
    }
}
```

**图 27.13** | Wall 材质脚本。

现在定位并缩放墙壁。左右两面墙分别沿 x 方向放置在距原点 95 个单位处。顶部和底部两面墙分别沿 y 方向放置在距原点 70 个单位处。然后每面墙被缩放到正确大小。顶部和

