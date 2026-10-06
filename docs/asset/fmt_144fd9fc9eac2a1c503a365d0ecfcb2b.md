
```c
void enc(void) {
  int index, index_out;
  while (1) {
    k_sem_take(&allforone, K_FOREVER);
    if (fUFIN == 1) { /* 1 表示处理文本 */
      printk("ENC Thread Received Data\n");
      /* 从共享内存中拷贝消息并
      清除标志位 */
      memcpy((void *)&enc_pt, (void *)BUFIN, SAMP_BLOCKSIZE);
      printk("ENC PT MSG: %s\n", (char*)&enc_pt);
      fUBIN = 0;
      /* 加密工作... */
      /* 重置恩格玛引擎轮轮：作为标志选项可能
      更好 */
      IW1 = 7;
      IW2 = 2;
      IW3 = 3;
      /* 编码 **/
      memset((void*)&enc_ct, 0, SAMP_BLOCKSIZE);
      for (index = 0, index_out = 0; index < SAMP_BLOCKSIZE; index++) {
        if (enc_pt[index] == '\0') {
          enc_ct[index_out] = '\0';
          break;
        }
        if (enc_pt[index] >= 'a' && enc_pt[index] <= 'z') {
          enc_ct[index_out] = (BYTE) enig_enc((BYTE) enc_pt[index]);
          index_out++;
        }
      }
      /* 测试 CT 标志位 */
      while (fBUFOUT != 0) {
        k_sleep(K_MSEC(1));
      }
      /* ct 线程已清空缓冲区 */
      memcpy((void*)&BUFOUT, (void*)&enc_ct, SAMP_BLOCKSIZE);
      fBUFOUT = 1;
      k_sem_give(&allforone);
    }
  }
}
```

```c
/* pt 函数将数据推送到 enc 线程。 */
void pt(void) {
  k_sleep(K_MSEC(20));
  while (1) {
    k_sem_take(&allforone, K_FOREVER);
    if (fUFIN == 0) { /* 发送消息进行编码 */
      printk("\nPT Sending Message 1\n");
      memset((void*)&BUFIN, 0, SAMP_BLOCKSIZE);
      memcpy((void*)&BUFIN, (void*)&ptMSG, sizeof(ptMSG));
      fBUFIN = 1;
      k_sem_give(&allforone);
      k_sem_take(&allforone, K_FOREVER);
      if (fBUFIN == 0) { /* 发送消息进行解码 */
        printk("\nPT Sending Message 1\n");
        memset((void*)&BUFIN, 0, SAMP_BLOCKSIZE);
        memcpy((void*)&BUFIN, (void*)&ptMSG2, sizeof(ptMSG2));
        fBUFIN = 1;
      }
      k_sem_give(&allforone);
      k_sleep(K_MSEC(50));
    }
  }
}
```

```c
void ct(void) {
  char tbuf[60];
  while (1) {
    k_sem_take(&allforone, K_FOREVER);
    if (fBUFOUT == 1) {
      printk("CT Thread Received Message\n");
      memset((void*)&tbuf, 0, sizeof(tbuf));
      memcpy((void*)&tbuf, (void*)BUFOUT, SAMP_BLOCKSIZE);
      fBUFOUT = 0;
      printk("CT MSG: %s\n", (char*)tbuf);
    }
    k_sem_give(&allforone);
  }
}
```

你应该尝试在多个开发板（如 `QEMU` 和 `Renode`）上运行它。

# 第 5 章 消息队列、管道、邮箱箱和工作队列

消息队列、邮箱箱和管道既提供了生产者（发送者）与接收者之间的同步，并在需要时提供数据的临时存储。工作队列代表了待完成的工作请求。

这些机制的底层是数据结构、算法和 API（应用程序接口）。对于消息队列，消息的最大尺寸以及与消息队列关联的循环缓冲区能存储的最大消息数量在创建消息队列实例时就已经固定了。相反，邮箱箱允许线程发送和接收任意大小的消息，并利用包含指向相关消息指针的消息描述符。消息队列和邮箱箱关注整个消息，而管道用于流式数据。与 POSIX 管道不同，Zephyr 管道不与文件描述符相关。

图 5-1 展示了一个常见的嵌入式系统场景。

**图 5-1.** 常见的嵌入式系统场景。在此场景中有三个线程：一个与获取传感器数据并写入输入队列的线程，一个负责分析输入数据并根据数据识别应用事件的线程，最后是一个负责从事件队列中检索事件信息并写入日志文件的线程。更复杂的场景可能涉及从多个传感器提取数据、向执行器写入命令，以及通过 BLE 或以太网等通信链路接收指令和命令。

## Zephyr 消息队列

Zephyr 消息队列可以被认为一个包含固定大小数据项集合的容器。项的大小及其包含的数据由所实现的应用程序决定。当创建消息队列时，还会指定其能包含的最大项数。Zephyr 消息队列 API 和实现提供了从队列中添加和删除项的逻辑，还提供了阻塞语义，即尝试从空消息队列中检索消息的线程将表现出可配置的阻塞行为（立即返回 `K_NO`、无限阻塞 `K_FOREVER` 或在指定的超时期间内阻塞）。同样，当消息队列为空时，尝试从空队列中读取也会表现出阻塞语义。

在使用消息队列时，考虑可能的用例场景非常重要。这包括处理当消息队列满且消息发送者尝试向队列发布消息的情况，以及消息接收者尝试从空消息队列中接收消息的情况。在配置消息队列时，必须决定要使用的消息大小以及队列要存储的最大消息数量。

## 消息队列 API 函数概述

该 API 提供了创建和初始化消息队列的函数，以及向消息队列放入消息和从消息队列获取消息的函数。

总结如下：

```c
void k_msgq_init(struct k_msgq *msgq, char *buffer, size_t msg_size, uint32_t max_msgs)
```
用于在消息队列结构和消息队列缓冲区内存分配后初始化消息队列。

```c
int k_msgq_alloc_init(struct k_msgq *msgq, size_t msg_size, uint32_t max_msgs)
```
初始化消息队列并从调用线程的内存池中分配所需的内存。

```c
int k_msgq_put(struct k_msgq *msgq, const void *data, k_timeout_t timeout)
```
用于将消息（发送）放入消息队列，或者如果有线程在等待空队列，则放入等待队列。

```c
int k_msgq_get(struct k_msgq *msgq, void *data, k_timeout_t timeout)
```
用于从消息队列获取消息。

此外，还有查看队列头部消息项以及丢弃消息队列中所有未接收消息的方法。在查看（peek）操作中，数据项被复制到足够容纳该数据的指定区域。查看操作的一种可能用途是检查数据的有效性和安全性，如果数据检查通过，则可以从消息队列中检索数据进行应用程序处理，否则则检索或丢弃数据。

```c
int k_msgq_peek(struct k_msgq *msgq, void *data)
```
执行读取但不将该项从消息队列中移除。

```c
void k_msgq_purge(struct k_msgq *msgq)
```
通过丢弃消息队列中所有未接收的消息来对消息队列进行清理。与此同时，被阻塞并等待向消息队列发送消息的线程将获得解阻塞。与这些解阻塞线程相关的 put 调用将返回 `ENOMSG` 错误代码。

其他 API 方法还包括：

- `uint32_t k_msgq_num_free(struct k_msgq *msgq)` 用于查询消息队列中的可用空空间。
- `void k_msgq_get_attrs(struct k_msgq *msgq, struct k_msgq_attrs *attrs)` 用于查询消息队列的属性。
- `uint32_t k_msgq_num_used(struct k_msgq *msgq)` 用于查询消息队列中的消息数量，以及释放与消息队列环形缓冲区内存的方法。
- `int k_msgq_cleanup(struct k_msgq *msgq)`，释放队列分配的缓冲区和为环形缓冲区分配的内存。

## 消息队列示例

此示例涉及一种场景：按下一个按钮触发向消息队列写入消息，按下另一个按钮触发从该消息队列中检索消息。

消息包含消息接收者所使用的信息。

消息数据项包含两个字段：一个用于标识要闪烁的 LED，另一个指定该 LED 闪烁的次数。在本示例中，闪烁周期被设置为常数值，在本例中为 200 毫秒。消息项从启动期间生成的可能消息集合中随机选择。检索消息项的线程不仅会按指定的次数闪烁目标 LED，而且在执行闪烁序列期间会设置忙标志位。

当忙标志位被设置时，按下触发接收消息的按钮将不起任何作用。

示例描述的是针对 `nRF52840 DK` 板的构建，该示例也可以为其他板卡构建并在 `Renode` 和 `QEMU` 中运行。

按钮连接到配置为边触发中断的 GPIO 引脚。

按钮的按下将由检测目标按钮边触发中断的中断处理程序处理。中断将通过使用二进制计数信号量触发数据的发送或接收。

在这种情况下，中断处理程序将控制向消息队列读写消息的线程的行为。

此示例的目的是为 Zephyr 应用程序如何利用消息传递和随机数生成提供见解。

## 练习描述

该场景的核心如图 5-2 所示。

![图 5-2](img/d25a3dc0e99570aa2c88d3c917f02390.png)

# 第 5 章 消息队列、管道、邮箱箱和工作队列

定义存储在消息队列中的消息类型代码段所示：

```c
struct k_msgq shd_msgq;

struct data_item_type {
    uint32_t num_flashes;
    uint32_t which_led;
};

char _aligned(4) shd_msgq_buffer[10 * sizeof(struct data_item_type)];

void main(void) {
  ...
  k_msgq_init(&shd_msgq, shd_msgq_buffer, sizeof(struct data_item_type), 10U);
  ...
}
```

应用程序中使用的消息数组设置和初始化如下：

```c
struct data_item_type {
    uint32_t num_flashes;
    uint32_t which_led;
};

struct data_item_type test_patterns[10];
```

```c
struct patternsCollection {
    uint32_t size;
    struct data_item_type *patterns;
};patternData;
```

```c
void init_test_patterns(struct data_item_type* test_patterns_, uint32_t arr_size) {
    int i;
    for (i = 0; i < arr_size; i++) {
        test_patterns_arry[i].num_flashes = (sys_rand32_get() % 10U) + 1;
        test_patterns_arry[i].which_led = (sys_rand32_get() % 2U) + 1;
    }
}

void main(void) {
    ...
    init_test_patterns(test_patterns, sizeof(test_patterns) / sizeof(struct data_item_type));
    patternData.size = sizeof(test_patterns) / sizeof(struct data_item_type);
    patternData.patterns = test_patterns;
}
```

对应两个按钮及其相关回调结构的全局变量以如下方式定义：

```c
static const struct gpio_dt_spec button1 =
    GPIO_DT_SPEC_GET_OR(SW0_NODE, gpios, {0});
static struct gpio_callback button1_cb_data;
static const struct gpio_dt_spec button2 =
    GPIO_DT_SPEC_GET_OR(SW1_NODE, gpios, {0});
static struct gpio_callback button2_cb_data;
```

全局 `working` 标志位以及按钮中断回调函数的代码定义在下一个代码片段中：

```c
uint32_t working = 0;
```

## 第 5 章 消息队列、管道、邮箱与工作队列

```c
void button1_pressed(const struct device *dev,
struct gpio_callback *cb, uint32_t pins)
{
printf("Button1 pressed at %u" PRU32 "\n", k_cycle_get_32(0));
/* 触发向消息队列投送数据 */
k_sem_give(&b1_sem);
printf("button1 press give \n");
}
```

```c
void button2_pressed(const struct device *dev,
struct gpio_callback *cb,uint32_t pins){
printf("Button2 pressed at %u" PRU32 "\n", k_cycle_get_32(0));
if (!working){
/* 触发从消息队列检索消息 */
k_sem_give(&b2_sem);
}else {
printf("Busy\n");
}
}
```

`main` 函数中用于设置按钮中断处理程序的代码所示：

```c
if (!device_is_ready(button1.port)) {
    printf("Error: button1 device %s is not ready\n", button1.port->name);
    return;
}
if (!device_is_ready(button2.port)) {
    printk("Error: button2 device %s is not ready\n", button2.port->name);
}
```

```c
ret = gpio_pin_configure_dt(&button1, GPIO_INPUT);
if (ret != 0) {
    printk("Error %d: failed to configure %s pin %d\n", ret, button1.port->name, button1.pin);
}
```

```c
ret = gpio_pin_configure_dt(&button2, GPIO_INPUT);
if (ret != 0) {
    printk("Error %d: failed to configure %s pin %d\n", ret, button1.port->name, button1.pin);
}
```

```c
ret = gpio_pin_interrupt_configure_dt(&button1, GPIO_INT_EDGE_TO_ACTIVE);
```

```c
if (ret != 0) {
    printk("Error %d: failed to configure interrupt %s pin %d\n", ret, button1.port->name, button1.pin);
}
```

```c
ret = gpio_pin_interrupt_configure_dt(&button2, GPIO_INT_EDGE_TO_ACTIVE);
```

```c
if (ret != 0) {
    printf("Error %d: failed to configure interrupt on %s pin %d\n", ret, button2.port->name, button2.pin);
    return;
}
```
