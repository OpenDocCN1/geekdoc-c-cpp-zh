
我们在打印时必须将每个单独的元素转换为字符串。我们可以通过 `map` 来克服这一局限，`map` 会获取数组中的每个元素并对其运行某个函数：
"".join(map(str,mask))

通过使用 `map`，我们将网络掩码中的每个整数转换为字符串。这让我们得到了一个字符串列表。接下来我们使用 `join` 将它们连接在一起。`join` 函数的工作原理是使用分隔符将列表元素组合成一个字符串，每个元素之间由该分隔符隔开。我们已经有了组合最终程序所需的所有。让我们尝试一下，并验证一切是否运行正常：

```python
#!/usr/bin/python
import sys
# 从命令行获取地址字符串和 cidr 字符串
(addrString,cidrString) = sys.argv[1].split('/')
# 将地址拆分为字节并将 cidr 转换为整数
addr = addrString.split('.')
cid = int(cidrString)
# 初始化网络掩码并根据 cidr 掩码计算
mask = [0,0,0,0]
for i in range(cidr):
mask[i/8] = mask[i/8] + (1 << (7 - i % 8))
# 使用 addr 获取网络、二进制和网络掩码
net = []
for i in range(4):
net.append(int(addr[i]) & mask[i])
# 将 net 复制到广播数组，收集主机位，并
# 生成广播
broad = list(net)
brange = 32 - cidr
for i in range(brange):
broad[3 - i/8] = broad[3 - i/8] + (1 << (i % 8))
# 打印信息，将整数列表映射为
# 易打印
print "Address: " , addrString
print "Netmask: " , "".join(map(str,mask))
print "Network: " , "".join(map(str,net))
print "Broadcast: " , "".join(map(str,broad))
```

现在，查看图 2.6 中的输出。

# root@mostdefinitelynotkali: ~/Desktop

```
root@mostdefinitelynotkali:~/Desktop/.subnet.py 192.168.1.1/24
Address: 192.168.1.1
Netmask: 255.255.255.0
Network: 192.168.1.0
Broadcast: 192.168.1.255
Address: 192.168.1.1
Netmask: 255.255.255.0
Network: 192.168.1.0
Broadcast: 192.168.1.255
Address: 192.168.1.1
Netmask: 255.255.255.0
Network: 192.168.1.0
Broadcast: 192.168.1.255
Address: 192.168.1.1
Netmask: 255.255.255.0
Network: 192.168.1.0
Broadcast: 192.168.1.255
Address: 192.168.1.1
Netmask: 255.255.255.0
Network: 192.168.1.0
Broadcast: 192.168.1.255
```

# 图 2.6 子子网的乐趣。

我们现在有了一个可以运行的代码示例，它以多种方式使用了列表。虽然这为使用列表提供了一些基础，但我们将在本章下一节的示例中进一步探讨这些主题。

## 字典
当我们有想要标记的列表元素时，使用字典。例如，我们可以将 ID 映射到员工姓名，或者将多个漏洞关联到特定的主机。

为了研究字典，让我们从一个实际示例开始。公司可能会根据某种模式为用户设置标准的初始密码。这可能包括使用与个人相关的字母和数字——例如，名字的第一个字母加上人力资源部门分配的员工 ID。如果我们发现了一个影子密码文件，只要我们知道密码是如何计算的，我们就可以确定哪些用户使用了默认密码。

假设我们发现了一个密码文件：
kevin:j5PRTBmoSymUI:42:42:Kevin,,, 42:/home/kevin:/bin/bash
ryan:A1QD3nPMW5e:1000:1000:Ryan,,, 431/home/ryan:/bin/bash
jason:aPg1C.EYR0db:1001:1001:Jason,,, 739/home/jason:/bin/bash
don:JCZWI:1002:1002:Don,,, 831/home/don:/bin/bash
ed:yN:1337:1337:Ed,,, 337/home/ed:/bin/bash

# 注意
关于字段的快速复习：第一个字段是用户名，第二个字段是 GECO 信息，第三个字段是 UID，第四个字段是家目录，第五个字段是 shell。

使用字典破解密码，可以使用 `crypt` 模块对潜在密码进行哈希并与文件中的哈希值进行比较。例如，我们使用字典来存储结果。

```python
#!/usr/bin/python
import sys
import crypt
f = open(sys.argv[1],"r+")
lines = f.readlines()
f.close()

found = []
for line in lines:
    data = line.split(':')
    # 设置前两个字段用户名和密码
    user,password = data[0:2]
    geco = data[4].split(',')
    # 使用名字的首字母和最后一个字段创建密码猜测
    guess = geco[0][0] + geco[-1]
    # 将加密密码的前两个字符作为盐（salt）
    salt = password[0:2]
    # 检查加密值是否匹配，如果是，则放入 found 列表
    if crypt.crypt(guess,salt) == password:
        userInfo = { "user": user, "pass": guess, "home" : data[5],
                    "uid" : data[2] , "name" : geco[0] }
        found.append(userInfo)

for user in found:
    print "User : %s " % user['user']
    for k in user.keys():
        if k == "user":
            continue
        print "\t%s %s" (k,user[k])
```
