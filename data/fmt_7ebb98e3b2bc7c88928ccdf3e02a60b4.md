
Found: moonrocks at Address: 000000
pref: 00 01 02 03 04 05 06 07 08 09 0a 0b 0c 0d 0e 0f
000000 60 61 62 63 64 65 66 67 68 69 6a 6b 6c 6d 6e 6f
000001 70 71 72 73 74 75 76 77 78 79 7a 7b 7c 7d 7e 7f
000002 80 81 82 83 84 85 86 87 88 89 8a 8b 8c 8d 8e 8f
000003 90 91 92 93 94 95 96 97 98 99 9a 9b 9c 9d 9e 9f
000004 00 01 02 03 04 05 06 07 08 09 0a 0b 0c 0d 0e 0f
000005 10 11 12 13 14 15 16 17 18 19 1a 1b 1c 1d 1e 1f
000006 20 21 22 23 24 25 26 27 28 29 2a 2b 2c 2d 2e 2f
000007 30 31 32 33 34 35 36 37 38 39 3a 3b 3c 3d 3e 3f
000008 40 41 42 43 44 45 46 47 48 49 4a 4b 4c 4d 4e 4f
000009 50 51 52 53 54 55 56 57 58 59 9a 9b 9c 9d 9e 9f

# 116 第 4 章 使用 Python 进行取证搜索与索引

```python
logging.basicConfig(filename='pSearchLog.log',level=logging.DEBUG,
format='%(asctime)s:%(message)s')
```

```python
### 处理命令行参数
_psearch.ParseCommandLine()

log = logging.getLogger('main._psearch')
log.info("p-search started")

### 记录开始时间
startTime = time.time()

# 执行关键词搜索
_psearch.SearchWords()

# 记录结束时间
endTime = time.time()
duration = endTime - startTime

logging.info('Elapsed Time: '+str(duration)+'seconds')
logging.info("Program Terminated Norm")
```

# p-search.py

```python
# psearch 支持函数，所有的实际工作在此完成
#
# DisplayMessage()            ParseCommandLine()
# ValidateReadFile()          ValidateFileWrite()
### Matrix (class)
#
import argparse

# Python 标准库 -
# 用于命令行选项
# 和参数的解析器
# 标准库 OS
# 函数
# 标准库 Logging
# 函数

log = logging.getLogger('main._psearch')
#常量
MIN_WORD = 5               # 最小单词大小（字节）
MAX_WORD = 15               # 最大单词大小（字节）
PREDECESSOR_SIZE = 32      # 在找到匹配项前打印的值
WINDOW_SIZE = 128          # 储出的总值
# 名称: ParseCommandLine() 函数
# 描述: 处理并验证命令行参数
#    使用 Python 标准库模块 argparse
```

# p-search 完整代码列表 117

# 输入：无

# 操作：

# 使用标准库 argparse 来处理命令行

# 行

```python
def ParseCommandLine():
    parser = argparse.ArgumentParser('Python Search')
    parser.add_argument('-v', '--verbose', help='启用打印
        额外的程序消息', action='store_true')
    parser.add_argument('-k', '--keywords', type= ValidateFileRead,
        required=True, help='指定包含搜索词的文件')
    parser.add_argument('-t', '--target', type= ValidateFileRead,
        required=True, help='指定要搜索的目标文件')
    parser.add_argument('-m', '--Matrix', type= ValidateFileRead,
        required=True, help='指定权重矩阵文件')
    global gl_args
    gl_args = parser.parse_args()
    DisplayMessage("命令行处理完成：成功")
    return
```

# 结束命令行处理

# 名称: ValidateFileRead 函数

# 描述: 验证文件是否存在且可读的函数

# 输入：带有完整路径的文件名

# 操作：

```python
if 有效则返回路径
```

```python
if 无效则将抛出 ArgumentTypeError
argparse
    该错误将由 argparse 报告给用户
```

```python
def ValidateFileRead(file):
    # 验证路径是否有效
    if not os.path.exists(file):
        raise argparse.ArgumentTypeError('文件不存在')

    # 验证路径是否可读
    if os.access(file, os.R_OK):
        return file
    else:
        raise argparse.ArgumentTypeError('文件不可读')
#End ValidateFileRead ===================================
```

```python
#
# 名称: DisplayMessage() 函数
#
# 描述: 如果存在 verbose 命令行选项则显示消息
### 输入：消息类型字符串
#
# 操作：
#    使用标准库 print 函数来显示
# 消息
```

```python
def DisplayMessage(msg):
    if gl_args.verbose:
        print(msg)
    return
```

#End DisplayMessage==================================================

### 名称: SearchWords()

### 使用命令行参数

### 在目标文件中搜索关键词

```python
def SearchWords():
    # 创建一个空集合
    searchWords = set()
    # 尝试打开并读取搜索词
    try:
        fileWords = open(gl_args.keywords)
        for line in fileWords:
            searchWords.add(line)
    except:
        log.error('关键词文件失败：'+gl_args.keywords)
        sys.exit()
    finally:
        fileWords.close()
    # 创建要搜索的日志条目
```

# p-search 完整代码列表 119

```python
log.info('搜索')
log.info('输入文件： '+gl_args.keywords)
log.info(searchWords)
```

# 尝试打开并读取目标文件

# 直接加载到 bytearray

```python
try:
    targetFile = open(gl_args.srchTarget, 'rb')
    baTarget = bytearray(targetFile.read())
except:
    log.error('目标文件失败： '+gl_args.srchTarget)
    sys.exit()
finally:
    targetFile.close()
```

```python
sizeOfTarget = len(baTarget)
```

# 写入日志

log.info('目标： '+gl_args.srchTarget)

log.info('文件大小： '+str(sizeOfTarget))

```python
baTargetCopy = baTarget
wordCheck = class_Matrix()
# 搜索循环
# 第一步，替换所有非字符
```

```python
for i in range(0, sizeOfTarget):
    character = chr(baTarget[i])
    if not character.isalpha():
        baTarget[i] = 0
```

# 第二步，从 bytearray 提取可能的单词
# 然后检查搜索词
# 创建一个可能的项列表

```python
indexOfWords = []
cnt = 0
for i in range(0, sizeOfTarget):
    character = chr(baTarget[i])
    if character.isalpha():
        cnt += 1
    else:
        if (cnt >= MIN_WORD and cnt <= MAX_WORD):
            newWord = ""
            for z in range(i-cnt, i):
                newWord += chr(baTarget[z])
            newWord = newWord.lower()
```

```python
if (newWord in searchWords):
    PrintBuffer(newWord, i-cnt, baTargetCopy, PREDECESSOR_SIZE, WINDOW_SIZE)
    indexOfWords.append([newWord, i-cnt])
    cnt = 0
else:
    if wordCheck.isWordProbable(newWord):
        indexOfWords.append([newWord, i-cnt])
        cnt = 0
else:
    cnt = 0
PrintAllWords(indexOfWords)
return
# 结束 Search 函数
```

```python
#
# 打印十六进制 / ASCII 页眉
#
def PrintHeading():
    print("*00 01 02 03 04 05 06 07 08 09 0A 0B 0C 0D ASCII")
    print("------------------------------------------------------------------------------------------------")
return
# 结束 PrintHeading
```

```python
#
# 打印缓冲区
#
# 打印发现单词的缓冲区
# 参数
# 1) 发现的单词
# 2) 单词的直接偏移
# 3) 持有目标的 bytearray
# 4) 打印时的缓冲区起始位置
# 5) hexSize，打印的十六进制窗口大小
#
def PrintBuffer(word, directOffset, buff, hexSize):
    print("Found: *" + word + " * Address: ")
    print("%08x\n" % directOffset)
    PrintHeading()
    for i in range(offset, offset+hexSize, 16):
        for j in range(0, 16):
            if (j == 0):
                print("%08x" % i, end="")
            else:
                byteValue = buff[i+j]
                print("%02x" % byteValue, end="")
        print("*")
        for j in range(16):
            byteValue = buff[i+j]
            if (byteValue >= 0x20 and byteValue <= 0x7f):
                print("%c" % byteValue, end="")
            else:
                print(".", end="")
        print()
# 结束 Print Buffer
```

```python
#
# PrintAllWordsFound
#
def PrintAllWordsFound(wordList):
    print("Index of All Words")
    print("----------------------")
    wordList.sort()
    for entry in wordList:
        print entry
        print("----------------------")
        print entry
return
#End PrintAllWordsFound
```

```python
#
# Matrix 类
#
### init 方法，将矩阵加载到集合中
### weightedMatrix
#
### isProbable 方法
### 1) 计算提供单词的权重
### 2) 验证最小长度
### 3) 计算单词的权重
### 4) 测试单词在矩阵中是否存在
### 5) 返回真或假
```

```python
class class_Matrix:
    weightedMatrix = set()
    def __init__(self):
        try:
            fileTheMatrix = open(gl_args.theMatrix, 'rb')
            for line in fileTheMatrix:
                value = line.strip()
                self.weightedMatrix.add(int(value,16))
        except:
            log.error('矩阵文件错误：'+gl_args.theMatrix)
            sys.exit()
        finally:
            fileTheMatrix.close()
        return
```

```python
def isWordProbable(self, word):
    if (len(word) < MIN_WORD):
        return False
    else:
        BASE = 96
        wordWeight = 0
        for i in range(4,0,-1):
            charValue = (ord(word[i]) - BASE
            shiftValue = (i-1)*8
            charWeight = charValue << shiftValue
            wordWeight = (wordWeight | charWeight)
    if (word in self.weightedMatrix):
        return True
    else:
        return False
```

# 章末总结

在本章中，我使用了新的 Python 语言元素，包括集合和 bytearray，并扩展了列表和类的使用。我还提供了如何打开和读取包含关键词、原始二进制和十六进制值等多种值的文件的示例，并直接在 bytearray、列表和集合中处理这些值。我演示了利用正确的语言元素如何编写简单易读的代码。结果是，p-search 是一个实用的应用程序，为调查人员提供了搜索关键词的能力。

文档、磁盘镜像、内存快照甚至网络跟踪中找到单词生成索引。

此外，我再次通过在 Windows、Linux 和 Mac 上运行未经修改的示例代码并产生结果，再次证明了 Python 代码的互操作性。

## 总结问题

- 1. 内置语言类型（列表、集合和字典）的优缺点是什么？

- 2. 解释使用集合（set）来存储关键字列表的优点。

- 3. Python 处理宽泛数据（二进制、文本和整数）的能力与其他语言有何不同？
