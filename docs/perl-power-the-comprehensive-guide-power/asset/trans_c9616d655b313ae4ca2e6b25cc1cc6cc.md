

## 第 7 章 数组与数据容器

### 用栈控制穿梭巴士

如图 7.13 所示，栈是一种容器，你在其中添加元素到末尾，然后在某个时刻从末尾移除元素。通常，程序员说他们将元素 *push* 到栈中，或从栈中 *pop* 元素。前面章节中回顾的 `push()` 和 `pop()` 函数对数组执行的操作，对应于常见的栈操作。栈容器中另一种常见的操作是获取栈的长度。`scalar()` 函数或用于赋值 `@` 数组值的过程（`$Length = @some array`）可用于此目的。

在使用栈时，一个关键概念通常涉及阈值的概念。阈值是一个累积量。例如，考虑工厂中的一种情况，你想要关联两条生产线的动作。一条生产线供应塑料娃娃。另一条供应装有塑料娃娃的箱子。栈允许你做到这一点。你可以创建一个计算机程序，记录电子检测设备的动作，该设备监控生产娃娃的生产线的输出。每当一个娃娃从生产线出来时，你可以向栈中添加一个元素。当栈中的元素增长到某个点时，你可以“pop”栈。当你 pop 栈时

### 将栈用作累加器

要创建一个简短程序来说明如何将栈用作 _累加器_，可以使用娃娃工厂的示例作为起点。目标涉及机场中人们到达机场周围几个停靠点之一。一名服务代表在每个停靠点值守，每当有新乘客到达需要穿梭巴士时，就向中央办公室的计算机发送一条消息。在高峰时段，当计算机显示有八个人在等待时，中央办公室会向停靠点派遣一辆穿梭巴士。图 7.14 说明了这种情况。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_190_0.png)

Listing07_09 的规格可能如下：

- 记录每个来到穿梭巴士停靠点并请求交通的乘客。
- 累积请求（在栈中）。
- 当栈达到指定的最大值（8）时，发出派遣穿梭巴士的命令。

诚然，在商业环境中，开发任何此类调度系统可能涉及更多内容，但在这种情况下，该场景提供了一个背景，使你可以看到栈如何作为累加器来关联两个活动：乘客到达穿梭巴士停靠点和派遣穿梭巴士接载乘客。

**Figure 7.14**  
当计算机发现有八个人在等待时，它会派遣一辆穿梭巴士。

```perl
#Listing07_09
#Setting up a stack as a shuttle schedule
#1 Define a passenger list
@Passengers =    qw (Ali Mo Stu Ed Tra Abe Todd Ham
                     Si Lil Min Lo Dli Regi Cal Hal
                     Su Len Joy Jay Xi Chi Tan Nu);

#Obtain a general number for the passengers
$Length = scalar(@Passengers);
print "\nNumber of passengers: $Length \n";
$ShuttleCount = 0;
$SHUTTLEMAX = 8; # Capacity of shuttle

#2 Set up "peak hours" with a for loop
for($Itr = 0; $Itr < $Length; $Itr++){

    #Comment out one of the following options
    # a. manual $AnyChar = <STDIN>;
    # b. delay the program's execution by one second
    sleep(1.0);

    #This involves a queue, passengers are taken on a first arrived,
    #first served basis

    #3 Use the push function to push passenger names into the stack
    push(@ShuttlePassengers, shift(@Passengers));

    #Accumulate shuttle passengers
    $WLength = scalar(@ShuttlePassengers);
    print "\n Waiting: $WLength";
    if($WLength >= $SHUTTLEMAX )
    {
        print "\n Please notify passengers: \n";
        for($Itr = 0; $Itr < $WLength; $Itr++){
        #4 When the stack is full, pop the passengers
            print "\t" . pop(@ShuttlePassengers);
        }
        #4.1 Augment the shuttle count and call for the shuttle
        $ShuttleCount++;
        print "\n Summon shuttle " . $ShuttleCount . "\n";
        print "\n Current group: " . $WLength . "\n";
        #4.2 Subtract the number who have left on the shuttle
        # from the total count
        $CurrentGroup = ($Length - ($ShuttleCount * $WLength));
        print "\n Passengers still waiting: $CurrentGroup\n";
        #4.3 Clear the stack array so the accumulation can start over
        undef(@ShuttlePassengers);
        if ($CurrentGroup <= 0) {
            print "\n Passengers accommodated.\n";
            print "\n";
            print "\n";
            exit(0);
        }
    }
}
```

图 7.15 说明了 Listing07_09 的输出。在注释 #1 之后的行中，你设置了一组模拟乘客。这样的列表代表在穿梭巴士停靠点注册的乘客。你将列表存储在 @Passengers 数组中，要获取此乘客列表的计数，你使用 scalar() 函数提取数组的长度，并将其赋给标量 $Length。此时，你还声明一个标量 $ShuttleCount，你暂时用它来存储已派遣的穿梭巴士数量。你还设置了一个标量 ($SHUTTLEMAX)，它确定穿梭巴士能容纳的最大人数。在这种情况下，最大数量需要调整，因此你设置的阈值是 8。

在注释 #2 之后的行中，for 语句的迭代次数由乘客总数 ($Length) 控制。在 for 循环内部，你设置了两个选项来控制程序的工作方式。一个选项 (a) 允许你手动操作程序。你按 Return 键将客户添加到等待列表。另一个选项自动化程序，使其以每秒一个客户的速度执行，添加客户。

在注释 #3 处，你使用 push() 函数配合 shift() 函数，从常规乘客列表中提取乘客姓名，并将其放入你设置的用于累积寻求穿梭巴士的乘客姓名的栈中。每次 for 循环迭代时，@ShuttlePassengers 数组的大小会增加一个乘客姓名。执行此操作后，你使用 scalar() 函数获取等待列表的大小，并将其赋给标量 $WLength。你使用 print() 函数显示此信息。

当你继续到注释 #4 时，你处于一个 if 语句中。if 语句评估栈中的乘客姓名数量 ($WLength)，以确定它是否大于或等于穿梭巴士能容纳的最大乘客数量 ($SHUTTLEMAX)。如果是，则执行 if 语句内部的代码。首要任务是 pop 栈。当你 pop 栈时，你使用 $WLength 标量来控制一个 for 语句，该语句调用 pop() 函数的次数与 $SHUTTLEMAX 允许的次数相同。这会 pop 出当前正在等待的每个人的姓名，你将其打印以供显示。

在注释 #4.1 处，你增加已召唤的穿梭巴士数量 ($ShuttleCount++)，然后显示新计数。你还记录登车的人数。

注释 #4.2 标记了一些记账细节。你通过将每辆穿梭巴士离开的当前人数乘以已离开的穿梭巴士数量，来确定离开的人数，然后将乘积从总乘客数中减去。这给你 $CurrentGroup 的值，你将其显示为仍在等待的乘客数量。

在注释 #4.3 之后的行中，你清除当前栈 (@ShuttlePassengers)。这是一种预防措施。人们有时会抱怨被困在队列或栈中。这样，如果他们没有收到服务或在合理的时间内看不到自己的名字，他们就可以抱怨。pop() 函数应该已经清除了它。然后，你要么遍历另一组乘客，要么退出程序。exit() 函数，你向其提供参数 0，退出程序并返回零值。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_193_0.png)

**Figure 7.15**  
Pop 栈可以让你知道何时呼叫穿梭巴士。

