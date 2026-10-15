
process of incremental upgrades, and if you are interested in attempting to supercharge your PC then you need to do so in small stages with regular tests. In that sense it can be a bit of a laborious task, but much like the thrill of putting together your first gaming PC the sensation of reaching new and better benchmarking tests can be enough of a thrill to get enthusiasts interested.

To help you get your head around overclocking your hardware we've detailed everything you need to know to assist in your own overclocking adventures. Since every piece of hardware is different, there's no sure-fire, step-by-step method to unlocking your PC's full potential, but as long as you have the knowledge to follow the process without any concern then you'll soon find it's not nearly as scary as it first sounds. We'll also document some of the best, most useful pieces of software you'll need for benchmarking – the process of stress-testing your PC to ensure your changes are safe – and some of the most popular games and applications overclockers like to use to show off just how powerful their PCs really are.

![](img/f51994701f272059dc108a0376ffceb8_123_0.png)

## Understanding overclocking

Before you actually jump into the overclocking itself, it is important that you first understand the technical side of what it is you’re trying to achieve. Every piece of hardware is different; one part could be minutely different to another of the exact same make and model due to the manufacturing process, so it’s important to know what you’re changing and what effect that change has. To help we’re going to explain some of the terms you’ll need to understand when overclocking – that way you won’t have any problems when overclocking your own system. And since you can enhance the performance of parts such as your graphics card, processor and memory, we’ll try to keep this section as general as possible across all forms of overclocking.

### Key terms to learn

**Overclocking** – Let’s start with the phrase itself, which is fairly self-explanatory. Overclocking is the process of increasing the clock speed of a particular piece of PC hardware to run faster than its initial factory settings, unlocking performance gains. Additionally this can mean increasing the voltage that piece of hardware accepts to help it attain higher speeds.

**BIOS** – This is the set-up screen where you’ll do your adjustments to the hardware – the actual process of overclocking itself. This is essentially the software hardwired into your motherboard, and lets you control the system’s hardware and how it performs. You may have seen the BIOS before or you may not have needed to, but either way it is always accessed immediately after starting the system up.

**Clock** – With all this mention of ‘clocks’ you’re probably asking ‘What is a clock?’ Well, this is the microchip inside your computer that regulates timing, that vibrates when electricity is applied. It is measured in hertz, with a 2.0GHz processor capable of two billion cycles – or vibrations – a second. It is often represented in your BIOS as `BCLK`. This is your base clock speed, and is used to calculate your CPU’s overall speed: so if your system has a base clock of 100MHz (perhaps shown as slightly under that) with a CPU multiplier or ratio of 30 then your CPU will have a total speed of 3,000MHz, or 3.0GHz. Increasing the multiplier to 33 will make your CPU a 3.3GHz processor.

**Data buses** – There are multiple buses inside your computer, but the most important is the main one connecting your CPU to the rest of the system. It is the communication interface that transfers data from your processor to the rest of your PC’s hardware, so essentially its speed affects how fast the other parts of your computer can be given commands from the CPU. These can come in various forms, but the function is always the same. Older processors call this the frontside bus (or FSB), while more recent terms include AMD’s EV6 or Intel’s QuickPath Interconnect. Though these don’t all work in exactly the same way, they do control the processing of information and so are pivotal to understand when overclocking.

**Clock multiplier/ratio** – Otherwise known as CPU multiplier, bus/core ratio or internal multiplier, this is the number of times the processor’s own internal clock completes a cycle within every external clock count. This is used to calculate the total speed of your processor by multiplying the clock multiplier with the external clock’s speed. It is one of the first numbers you’ll want to try and adjust in the overclocking process.

**Voltage** – This is an extra side to overclocking that is important to understand. While increasing the voltage supply to a particular piece of hardware won't actually increase its performance – much like putting extra fuel into a car – it is often a necessity as you increase the speed of that component. The faster an overclocked part runs the more power it's going to need to function at its best. As with the overclocking process, this should be done slowly and incrementally, to ensure the right voltage is set.

![](img/f51994701f272059dc108a0376ffceb8_125_0.png)

If you want to achieve the very best graphics from your games, overclocking can be a good option for achieving that with cheaper or mid-range parts.

## Benchmarking

This is a process whereby you will monitor your PC – often under stress-test situations – to ensure that the upgrade you have made to a piece of hardware has both been successful and isn't likely to cause any damage to your hardware. Even outside of overclocking, benchmarking is a useful way of discovering just how powerful your PC is. Since there is a risk of permanent damage to your components by overclocking, it's imperative that you use benchmarking to ensure you haven't exceeded any boundaries. We'll talk in more depth about benchmarking and the software you can use later in this chapter.

## DirectX

When it comes to graphics cards, you'll often see the term DirectX pop up – often seen as DX9 or DX11. This is an API that a lot of modern games rely on to function, and though it's not a prerequisite for PC gaming a large portion of games do need a compatible graphics card to function well. Thankfully your only concern is whether or not you're running a DX9 or a DX11 card. DX11 is a more recent, up-to-date and powerful version of DirectX, and enables a lot of fancy extras within games, and most recent GPUs are powerful enough to handle DX11. Make sure you know which yours is, however, before going about overclocking, as it'll help you understand which games you're best testing it with.

## Preparation

Before you actually start overclocking there are a few things you'll want to consider first. This will mean downloading and installing some software to help monitor your changes – and stress-test those that you have made – as well as consider some of the hardware requirements for overclocking. This latter part might not be relevant to you, but it's worth knowing about if it is something you want to do in the future.

### CPU-Z/GPU-Z

这是一款非常实用的软件，可以详细列出系统各项数值，例如时钟速度、电压等等。在你进行任何改动之前最好先运行它，改动之后再运行一次，一方面确保改动已正确保持，另一方面检查你所调整的设置是否正常工作。当你需要超频显卡时，其对应的软件叫做 GPU-Z。

### 压力测试软件

市面上有多种压力测试软件可供选择，具体取决于你超频的硬件类型。我们将在每个具体章节中更详细地讨论它们，但对于 CPU 压力测试，你需要的是 Prime95、BurnInTest、FurMark 或 AIDA64 之类的软件。还有很多其他软件可以使用，但如果你担心的话，不妨使用多种压力测试软件组合——我们无法强调足够确保你的改动不会损坏硬件的重要性。对于 GPU 超频来说要简单一些，但最容易推荐的是 FutureMark 的 3DMark。

### Real Temp

既然压力测试是有目的的，你就需要有软件在旁边配合运行。Real Temp 可以让你监控所有硬件组件的真实温度，以确保它们在压力测试期间不会过热。

### 散热

如果你只是通过超频进行小幅升级，那么可能不必太担心散热问题。只要你的系统通风充足，并且散热系统适合你现有的硬件，那么对硬件的小幅改动很可能会在不更换散热的情况下通过。事实上，原装 CPU 风扇足以略微提升处理器的性能。这并不意味着你不应该关注系统的热量，因为那是超频时最大的威胁。如果你想进行更大的改动，那么你肯定需要确保电脑及其部件的更高温度得到解决。

### 电源

你几乎不需要升级电源，但由于在超频过程中你会增加部件使用的电压，因此机器所需的整体功率也会增加。很有可能你已安装的电源足以充分供应机器，但如果你电源供应较低，并且在超频后发现机器运行不充分，那么你可能需要升级电源。

### 超频兼容性

并非所有主板，甚至处理器和显卡都适合超频。有些厂商喜欢将功能锁定，而其他厂商则默认解锁硬件潜力供发烧友使用。值得庆幸的是，大多数高端 PC 游戏组件都是考虑到超频而构建的，尽管你通常需要为此支付溢价。
