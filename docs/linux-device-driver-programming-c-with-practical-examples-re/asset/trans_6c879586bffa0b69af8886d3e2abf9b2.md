

分配给已分配区域的地址。

```
void kmalloc(size_t size, gfp_t flags);
```

- size: 要分配的内存块的大小（以字节为单位）。
- flags: 指定内存类型和分配行为的分配标志。

## 示例：

```
C
void *buffer = kmalloc(PAGE_SIZE, GFP_KERNEL);
if (!buffer) {
    printk(KERN_ERR "Failed to allocate memory\n");
    return -ENOMEM;
}
// 使用已分配的内存
kfree(buffer);
```

kzalloc()

kzalloc() 是 kmalloc() 的一种变体，它将已分配的内存初始化为零。

```
C
void *kzalloc(size_t size, gfp_t flags);
```

vmalloc()

对于大块连续内存分配，使用 vmalloc()。它分配虚拟内存，其物理内存可能不连续。

```
C
void *vmalloc(unsigned long size);
```

- size: 要分配的内存块的大小（以字节为单位）。

```
C
struct mempool_s {
  /* ... */
};

struct mempool_s *mempool_create(int min_nr, mempool_alloc_t *alloc_fn,
    mempool_free_t *free_fn, void *pool_data);

void *mempool_alloc(struct mempool_s *pool, gfp_t gfp_mask);
void mempool_free(struct mempool_s *pool, void *obj);
```

## 内存管理最佳实践

- **只分配所需内存：** 避免过度内存分配。
- **使用适当的标志：** 根据分配上下文选择正确的 gfp_t 标志。
- **及时释放内存：** 在不再需要时释放已分配的内存。
- **考虑内存池：** 对于具有固定大小分配的性能关键场景。
- **优雅地处理分配失败：** 实现错误处理机制。
- **注意内存泄漏：** 使用像 memleak 这样的工具来检测内存泄漏。

## 示例：设备缓冲区分配

```c
struct my_device {
	void *buffer;
	/* ... */
};

static int my_device_probe(struct platform_device *pdev) {
	struct my_device *dev = devm_kzalloc(&pdev->dev, sizeof(*dev), GFP_KERNEL);
	if (!dev)
		return -ENOMEM;

	dev->buffer = dma_alloc_coherent(&pdev->dev, BUFFER_SIZE,
		&dev->dma_handle, GFP_KERNEL);
	if (!dev->buffer) {
		devm_kfree(&pdev->dev, dev);
		return -ENOMEM;
	}

	// ...
}
```

内核内存分配是 Linux 设备驱动开发的一个基本方面。通过了解可用的函数、标志和最佳实践，您可以有效地管理内存资源并创建健壮高效的设备驱动程序。

## Linux 设备驱动中的 DMA 一致性内存

## 理解 DMA 一致性内存

直接内存访问（DMA）是设备与系统内存之间高性能数据传输的关键技术，无需 CPU 作为瓶颈。然而，DMA 操作会引入缓存一致性问题。为了解决这个问题，内核提供了 DMA 一致性内存，它确保 CPU 写入的数据对 DMA 引擎立即可见，反之亦然。

## 分配 DMA 一致性内存

在 Linux 中分配 DMA 一致性内存的主要函数是 dma_alloc_coherent()：

```
C
void *dma_alloc_coherent(struct device *dev, size_t size, dma_addr_t *dma_handle, gfp_t flags);
```

- **dev**：与分配关联的设备。
- **size**：要分配的内存块的大小。
- **dma_handle**：用于存储已分配内存的 DMA 地址的指针。
- **flags**：分配标志，与 kmalloc() 类似。

## 使用 DMA 一致性内存

分配 DMA 一致性内存后，您可以使用返回的虚拟地址进行 CPU 访问，并使用 DMA 地址进行设备访问。

```
C
void *buffer = dma_alloc_coherent(dev, PAGE_SIZE, &dma_handle, GFP_KERNEL);
if (!buffer) {
    printk(KERN_ERR "Failed to allocate DMA-coherent memory\n");
    return -ENOMEM;
}

// 使用 buffer 进行 CPU 访问
memcpy(buffer, data, size);

// 配置设备使用 dma_handle 进行 DMA 传输

// ...

dma_free_coherent(dev, PAGE_SIZE, buffer, dma_handle);
```

## DMA 一致性内存和缓存管理

虽然 DMA 一致性内存简化了 DMA 编程的许多方面，但了解其底层的缓存机制至关重要。不同架构的缓存一致性程度各不相同。某些架构可能需要显式的缓存刷新或失效。dma_map_single()、dma_map_page() 和 dma_map_sg() 函数为复杂场景提供了对 DMA 映射和缓存一致性的更精细控制。

## DMA 池

对于频繁分配和释放小块 DMA 一致性缓冲区，可以使用 DMA 池来提高性能。它们预先分配一组缓冲区并高效管理。

```c
struct dma_pool *dma_pool_create(const char *name, struct device *dev,
                                 size_t size, size_t align, size_t boundary);
void *dma_pool_alloc(struct dma_pool *pool, gfp_t gfp_mask, dma_addr_t *dma_handle);
void dma_pool_free(struct dma_pool *pool, void *cpu_addr, dma_addr_t dma_handle);
```

## DMA 一致性内存的注意事项

- **性能：** 由于缓存行刷新或失效，DMA 一致性内存可能比非一致性内存更昂贵。
- **对齐：** 某些设备对 DMA 传输有严格的对齐要求。分配 DMA 一致性内存时确保正确对齐。
- **错误处理：** 优雅地处理分配失败并正确释放资源。
- **缓存一致性：** 意识到不同架构上的缓存一致性问题并采取必要的预防措施。

## 示例：使用 DMA 一致性内存的 DMA 传输

```c
struct my_device {
	void *buffer;
	dma_addr_t dma_handle;
	/* ... */
};

static int my_device_probe(struct platform_device *pdev) {
	struct my_device *dev = devm_kzalloc(&pdev->dev, sizeof(*dev), GFP_KERNEL);
	if (!dev)
		return -ENOMEM;

	dev->buffer = dma_alloc_coherent(&pdev->dev, BUFFER_SIZE, &dev->dma_handle, GFP_KERNEL);
	if (!dev->buffer) {
		devm_kfree(&pdev->dev, dev);
		return -ENOMEM;
	}

	// 配置设备使用 dev->dma_handle 进行 DMA 传输

	// ...

dma_free_coherent(&pdev->dev, BUFFER_SIZE, dev->buffer, dev->dma_handle);
	return 0;
}
```

通过有效使用 DMA 一致性内存，您可以优化数据传输性能并简化设备驱动开发。

## Linux 设备驱动中的自旋锁、信号量和互斥锁

在 Linux 设备驱动领域，共享资源的并发访问是一个常见挑战。为了确保数据完整性并防止竞争条件，同步机制至关重要。本文深入探讨了三种基本的同步原语：自旋锁、信号量和互斥锁，探索了它们在 Linux 设备驱动上下文中以 C++ 实现的特性、用途。

自旋锁是最基本的同步形式，其中线程会持续检查标志直到其可用。虽然简单，但它们对于短临界区非常高效。然而，如果锁被长时间持有，可能会导致 CPU 浪费。

```cpp
C++ Implementation:

#include <linux/spinlock.h>
spinlock_t my_spinlock;

void function_with_spinlock() {
 spin_lock(&my_spinlock);
 // Critical section
 spin_unlock(&my_spinlock);
}
```

- 保护短临界区。
- 在短时间内禁用中断。
- 保护从中断处理程序访问的共享数据。

## 信号量

信号量比自旋锁更灵活，允许最多指定数量的线程并发访问资源。当计数达到零时，后续线程会阻塞直到资源被释放。

```
C++ Implementation:

C++
#include <linux/semaphore.h>

struct semaphore my_semaphore;

void function_with_semaphore() {
    down(&my_semaphore);
    // Critical section
    up(&my_semaphore);
}
```

## 用例：

- 控制对有限数量资源的访问。
- 在不同进程之间同步任务。
- 实现生产者-消费者模式。

## 互斥锁

互斥锁（互斥锁）与信号量类似，但接口更简单，专门用于互斥。一次只有一个线程可以持有互斥锁。

