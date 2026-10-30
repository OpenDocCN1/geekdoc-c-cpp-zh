

在 `foo_alloc` 函数中将引用计数初始化为 1 时是必要的，因为此时分配线程是唯一对它的引用。如果我们在此阶段将结构放在列表上，它可能会被其他线程找到，因此我们需要先锁定它。

在使用对象之前，线程应通过调用 `foo_hold` 为其添加一个引用。完成后，它们必须调用 `foo_rele` 释放引用。当最后一个引用被释放时，对象的内存将被释放。

在此示例中，我们忽略了线程在调用 `foo_hold` 之前如何找到对象的问题。即使引用计数为零，如果另一个线程在调用 `foo_hold` 时被阻塞在互斥锁上，`foo_rele` 释放对象的内存也是错误的。我们可以通过确保在释放内存之前对象无法被找到来避免此问题。我们将在后面的示例中看到如何做到这一点。

## 11.6.2 死锁避免

如果线程尝试两次锁定同一个互斥锁，它会使自己死锁，但使用互斥锁创建死锁还有更不明显的方法。例如，当我们在程序中使用多个互斥锁时，如果允许一个线程持有互斥锁并在尝试锁定第二个互斥锁时被阻塞，同时另一个持有第二个互斥锁的线程尝试锁定第一个互斥锁，就会发生死锁。两个线程都无法继续，因为每个线程都需要另一个线程持有的资源，因此我们发生了死锁。

可以通过仔细控制互斥锁的锁定顺序来避免死锁。例如，假设你有两个互斥锁 A 和 B，需要同时锁定。如果所有线程始终先锁定互斥锁 A 再锁定互斥锁 B，就不会因使用这两个互斥锁而发生死锁（但仍可能在其他资源上死锁）。同样，如果所有线程始终先锁定互斥锁 B 再锁定互斥锁 A，也不会发生死锁。只有当一个线程尝试以与另一个线程相反的顺序锁定互斥锁时，才会出现死锁的可能性。

有时，应用程序的架构使得应用锁定顺序变得困难。如果涉及的锁和数据结构足够多，以至于你可用的函数无法塑造成简单的层次结构，那么你就必须尝试其他方法。在这种情况下，你可能能够释放你的锁并在稍后重试。你可以使用 `pthread_mutex_trylock` 接口来避免在此情况下发生死锁。如果你已经持有锁并且 `pthread_mutex_trylock` 成功，那么你可以继续。如果它无法获取锁，则可以释放你已持有的锁，清理并稍后再试。

### 示例

在此示例中，我们更新图 11.10 以显示使用两个互斥锁。我们通过确保当我们需要同时获取两个互斥锁时，始终以相同的顺序锁定它们来避免死锁。第二个互斥锁保护我们用于跟踪 foo 数据结构的哈希列表。因此 `hashlock` 互斥锁同时保护 `fh` 哈希表和 `foo` 结构中的 `f_next` 哈希链接字段。`foo` 结构中的 `f_lock` 互斥锁保护对 `foo` 结构其余字段的访问。

```
#include <stdlib.h>
#include <pthread.h>

#define NHASH 29
#define HASH(id) (((unsigned long)id)%NHASH)

struct foo *fh[NHASH];

pthread_mutex_t hashlock = PTHREAD_MUTEX_INITIALIZER;

struct foo {
    int f_count;
    pthread_mutex_t f_lock;
    int f_id;
    struct foo *f_next; /* protected by hashlock */
    /* ... more stuff here ... */
};

struct foo *
foo_alloc(int id) /* allocate the object */
{
    struct foo *fp;
    int idx;
    if ((fp = malloc(sizeof(struct foo))) != NULL) {
        fp->f_count = 1;
        fp->f_id = id;
        if (pthread_mutex_init(&fp->f_lock, NULL) != 0) {
            free(fp);
            return(NULL);
        }
        idx = HASH(id);
        pthread_mutex_lock(&hashlock);
        fp->f_next = fh[idx];
        fh[idx] = fp;
        pthread_mutex_lock(&fp->f_lock);
        pthread_mutex_unlock(&hashlock);
        /* ... continue initialization ... */
        pthread_mutex_unlock(&fp->f_lock);
    }
    return(fp);
}

void
foo_hold(struct foo *fp) /* add a reference to the object */
{
    pthread_mutex_lock(&fp->f_lock);
    fp->f_count++;
    pthread_mutex_unlock(&fp->f_lock);
}

struct foo *
foo_find(int id) /* find an existing object */
{
```

```
struct foo *fp;
pthread_mutex_lock(&hashlock);
for (fp = fh[HASH(id)]; fp != NULL; fp = fp->f_next) {
    if (fp->f_id == id) {
        foo_hold(fp);
        break;
    }
}
pthread_mutex_unlock(&hashlock);
return(fp);
}

void
foo_rele(struct foo *fp) /* release a reference to the object */
{
    struct foo *tfp;
    int idx;
    pthread_mutex_lock(&fp->f_lock);
    if (fp->f_count == 1) { /* last reference */
        pthread_mutex_unlock(&fp->f_lock);
        pthread_mutex_lock(&hashlock);
        pthread_mutex_lock(&fp->f_lock);
        /* need to recheck the condition */
        if (fp->f_count != 1) {
            fp->f_count--;
            pthread_mutex_unlock(&fp->f_lock);
            pthread_mutex_unlock(&hashlock);
            return;
        }
        /* remove from list */
        idx = HASH(fp->f_id);
        tfp = fh[idx];
        if (tfp == fp) {
            fh[idx] = fp->f_next;
        } else {
            while (tfp->f_next != fp)
                tfp = tfp->f_next;
            tfp->f_next = fp->f_next;
        }
        pthread_mutex_unlock(&hashlock);
        pthread_mutex_unlock(&fp->f_lock);
        pthread_mutex_destroy(&fp->f_lock);
        free(fp);
    } else {
        fp->f_count--;
        pthread_mutex_unlock(&fp->f_lock);
    }
}
```

将图 11.11 与图 11.10 进行比较，我们看到我们的分配函数现在锁定哈希列表锁，将新结构添加到哈希桶中，并在解锁哈希列表锁之前锁定新结构中的互斥锁。由于新结构被放置在全局列表上，其他线程可以找到它，因此如果它们尝试访问新结构，我们需要阻止它们，直到我们完成对其的初始化。

`foo_find` 函数锁定哈希列表锁并搜索请求的<|message|> 结构。如果找到，我们增加引用计数并返回指向该结构的指针。请注意，我们通过在 `foo_find` 中先锁定哈希列表锁，然后在 `foo_hold` 中锁定 `foo` 结构的 `f_lock` 互斥锁来遵守锁定顺序。

现在有了两个锁，`foo_rele` 函数变得更复杂。如果这是最后一个引用，我们需要解锁结构互斥锁，以便我们能够获取哈希列表锁，因为我们需要从哈希列表中删除该结构。然后我们重新获取结构互斥锁。由于我们自上次持有结构互斥锁以来可能已被阻塞，因此我们需要重新检查条件以查看是否仍需要释放该结构。如果另一个线程在我们为了遵守锁定顺序而阻塞时找到了该结构并为其添加了引用，我们只需递减引用计数，解锁所有内容并返回即可。

这种锁定方法很复杂，因此我们需要重新审视我们的设计。我们可以通过使用哈希列表锁来保护结构引用计数，从而大大简化事情。结构互斥锁可用于保护 `foo` 结构中的其他所有内容。图 11.12 反映了这一更改。

```
#include <stdlib.h>
#include <pthread.h>

#define NHASH 29
#define HASH(id) (((unsigned long)id)%NHASH)

struct foo *f[NHASH];
pthread_mutex_t hashlock = PTHREAD_MUTEX_INITIALIZER;

struct foo {
    int          f_count;  /* protected by hashlock */
    pthread_mutex_t f_lock;
    int          f_id;
    struct foo   *f_next;  /* protected by hashlock */
    /* ... more stuff here ... */
};

struct foo *
foo_alloc(int id) /* allocate the object */
{
    struct foo *fp;
    int idx;

    if ((fp = malloc(sizeof(struct foo))) != NULL) {
        fp->f_count = 1;
        fp->f_id = id;
        if (pthread_mutex_init(&fp->f_lock, NULL) != 0) {
            free(fp);
```
