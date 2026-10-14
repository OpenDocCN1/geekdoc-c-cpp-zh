

#---基础先攻值---

```python
def marineInitiative(self):
    """Creates the base level for a Marine
    character type.

    Marines with an MOS of Sniper/Scout, Recon
    , or Pilot gain +1 to initiative.
    Marines with an MOS of Supply, Intelligence
    , or Medical lose -1 to initiative."""

    if self.mosChoice == 6 or self.mosChoice == 7 or self.mosChoice == 18:
        self.marineInit = self.coreInitiative + 1
    elif self.mosChoice == 0 or self.mosChoice == 3 or 15 <= self.mosChoice <= 17:
        self.marineInit = self.coreInitiative - 1
    else:
        self.marineInit = self.coreInitiative

def test():
    marine = Character()
    marine = Marine()
    marine.setName()
    marine.setGender()
    marine.setAge()
    marine.setSkills()
    marine.setEquipment("Rucksack")
    marine.setEquipment("Knife")
    marine.setEquipment("Flashlight")
    #print "\nName = ", marine.name
    #print "Gender = ", marine.gender
    #print "Age = ", marine.age
    #for key in marine.attrib_dict.keys():
    #    print key, marine.attrib_dict[key]
    #for key in marine.hp_dict.keys():
    #     print key, marine.hp_dict[key]
    #print marine.chosenSkills
    #print marine.subskills
    #marine.getEquipment()
    marine.setRank()
    print "Rank: ", marine.rank
    #print "Rank name: ", marine.rankName
    marine.requirements()
    marine.eligibleMOS()
    print "Your MOS is: ", marine.mos
    marine.mosSkills(marine.mosChoice)
    print marine.chosenSkills
    marine.setInitiative()
    marine.marineInitiative()
    print "Your Initiative is: ", marine.marineInit

if __name__ == "__main__":
    test()
```

## 附录 F

## GNU 通用公共许可证

版权所有 © 2007 自由软件基金会。 http://fsf.org/

允许任何人逐字复制和分发本许可文档，但不允许对其进行修改。

GNU 通用公共许可证是一项针对软件及其他类型作品的自由、自由复制（copyleft）许可。

大多数软件和其他实用作品的许可证旨在剥夺您分享和修改这些作品的自由。相比之下，GNU 通用公共许可证旨在保证您分享和修改程序所有版本的自由——确保它对所有用户而言始终是自由软件。我们，自由软件基金会，在大多数软件中采用 GNU 通用公共许可证；该许可证同样适用于作者以这种方式发布的任何其他作品。您也可以将其应用于您的程序。

当我们谈论自由软件时，我们指的是自由，而非价格。我们的通用公共许可证旨在确保您拥有分发自由软件副本的自由（如果您愿意，可以为此收费），确保您能获得源代码或在您想要时获取源代码，确保您可以修改软件或将其部分用于新的自由程序，并且确保您知道可以这样做。

为了保护您的权利，我们需要防止他人拒绝您这些权利或要求您放弃这些权利。因此，如果您分发软件副本或修改它，您将承担某些责任：尊重他人自由的责任。

例如，如果您分发此类程序的副本，无论是免费还是收费，您都必须将您获得的相同自由传递给接收者。您必须确保他们也能获得或获取源代码。您还必须向他们展示这些条款，以便他们了解自己的权利。

使用 GNU GPL 的开发者通过两步保护您的权利：（1）对软件主张版权，（2）向您提供本许可证，赋予您复制、分发和/或修改该软件的合法许可。

为了保护开发者和作者，GPL 明确说明该自由软件没有保修。为了用户和作者双方的利益，GPL 要求修改版本必须标记为已修改，以免其问题被错误地归咎于早期版本的作者。

某些设备被设计用于拒绝用户在其内部安装或运行修改后版本的软件，尽管制造商可以这样做。这与保护用户修改软件的自由的目标根本不相容。这种系统性的滥用模式发生在个人使用的产品领域，而这恰恰是最不可接受的领域。因此，我们设计了本版本的 GPL 以禁止在这些产品中此类做法。如果此类问题在其他领域大量出现，我们准备在未来版本的 GPL 中根据需要扩展此条款至那些领域，以保护用户的自由。

最后，每个程序都始终受到软件专利的威胁。国家不应允许专利限制通用计算机上软件的开发和使用，但在允许这种限制的国家，我们希望能避免针对免费程序的专利应用使其实际上成为专有软件的特别危险。为了防止这种情况，GPL 确保专利不能被用来使程序变得非自由。

复制、分发和修改的具体条款和条件如下。

### 条款和条件

1.  **定义。**

    “本许可证”指 GNU 通用公共许可证第 3 版。

    “版权”也指适用于其他类型作品的类似版权法律，例如半导体掩模。

    “该程序”指根据本许可证授权的任何受版权保护的作品。每个被许可人被称为“您”。“被许可人”和“接收者”可以是个人或组织。

    “修改”作品意味着以需要版权许可的方式复制全部或部分作品进行改编，制作完全副本除外。由此产生的作品被称为先前作品的“修改版本”或“基于”先前作品的作品。

    “覆盖作品”指未修改的程序或基于程序的作品。

    “传播”作品意味着对其执行任何行为，若无许可，根据适用的版权法将使你直接或间接承担侵权责任，但在计算机上执行或在私人副本上进行修改除外。传播包括复制、分发（无论是否修改）、向公众提供，在某些国家还包括其他活动。

    “传递”作品意味着任何使其他方能够制作或接收副本的传播形式。通过计算机网络与用户进行的纯粹交互，且没有副本转移的，不属于传递。

    交互式用户界面应在“适当的法律声明”范围内显示，即包含一个方便且显著可见的功能，该功能：(1) 显示适当的版权声明，(2) 告知用户该作品没有保修（除非提供了保修），被许可人可以根据本许可证传递该作品，以及如何查看本许可证的副本。如果界面呈现用户命令或选项列表（如菜单），列表中显著的项目即满足此标准。

2.  **源代码。**

    作品的“源代码”指制作该作品修改所需的优选形式。“目标代码”指作品的非源代码形式。

    “标准接口”指由公认标准机构定义的官方标准，或者在针对特定编程语言指定的接口情况下，指在该语言开发者中广泛使用的接口。

    可执行作品的“系统库”包括除作品整体以外的任何内容，这些内容：(a) 包含在主组件的正常打包形式中，但不是该主组件的一部分，且 (b) 仅用于启用该作品与该主组件的使用，或实现一种标准接口，而该接口的实现可以公开以源代码形式获得。在此上下文中，“主组件”指特定操作系统（如果有）的可执行作品运行在其上的主要基本组件（内核、窗口系统等），或用于生成该作品的编译器，或用于运行该作品的目标代码解释器。

    目标代码形式作品的“对应源代码”指生成、安装和（对于可执行作品）运行目标代码以及修改该作品所需的所有源代码，包括控制这些活动的脚本。然而，它不包括作品的系统库，或未修改用于执行这些活动的一般用途工具或通常可获得的免费程序，这些不是作品的一部分。例如，对应源代码包括与作品源文件相关的接口定义文件，以及作品特别设计为所需的共享库和动态链接子程序的源代码，例如通过那些子程序与作品其他部分之间的密切数据通信或控制流。

    对应源代码无需包含用户可以自动从对应源代码的其他部分重新生成的任何内容。

