

int pclose(FILE *fp);
<stdlib.h>
返回值：popen 所执行 cmdstring 命令的终止状态，出错返回 -1

void perror(const char *msg);
<stdlib.h>

int pipe(int fd[2]);
<unistd.h>
返回值：成功返回 0，出错返回 -1

int poll(struct pollfd farray[], nfds_t nfds, int timeout);
<poll.h>
返回值：就绪描述符的数量，超时返回 0，出错返回 -1

FILE *popen(const char *cmdstring, const char *type);
<stdlib.h>
type: "r", "w"
返回值：成功返回文件指针，出错返回 NULL

int posix_openpt(int oflag);
<stdlib.h>
<fcntl.h>
oflag: O_RDWR, O_NOCTTY
返回值：成功返回下一个可用 PTY 主设备的文件描述符，出错返回 -1

ssize_t pread(int fd, void *buf, size_t nbytes, off_t offset);
<unistd.h>
返回值：读到的字节数，若已到文件末尾返回 0，出错返回 -1

void psignal(int signo, const char *msg);
<signal.h>
<siginfo.h>    /* 在 Solaris 上 */
第 379 页

int pthread_atfork(void (*prepare)(void), void (*parent)(void), void (*child)(void));
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 458 页

int pthread_attr_destroy(pthread_attr_t *attr);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 427 页

int pthread_attr_getdetachstate(const pthread_attr_t *attr, int *detachstate);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 428 页

int pthread_attr_getguardsize(const pthread_attr_t *restrict attr, size_t *restrict guardsize);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 430 页

int pthread_attr_getstack(const pthread_attr_t *restrict attr, void **restrict stackaddr, size_t *restrict stacksize);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 429 页

int pthread_attr_getstacksize(const pthread_attr_t *restrict attr, size_t *restrict stacksize);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 430 页

int pthread_attr_init(pthread_attr_t *attr);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 427 页

int pthread_attr_setdetachstate(pthread_attr_t *attr, int detachstate);
<pthread.h>
detachstate: PTHREAD_CREATE_DETACHED, PTHREAD_CREATE_JOINABLE
返回值：成功返回 0，失败返回错误编号
第 428 页

int pthread_attr_setguardsize(pthread_attr_t *attr, size_t guardsize);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 430 页

int pthread_attr_setstack(const pthread_attr_t *attr, void *stackaddr, size_t *stacksize);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 429 页

int pthread_attr_setstacksize(pthread_attr_t *attr, size_t stacksize);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 430 页

int pthread_barrierattr_destroy(pthread_barrierattr_t *attr);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 441 页

int pthread_barrierattr_getshared(const pthread_barrierattr_t *restrict attr, int *restrict pshared);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 441 页

int pthread_barrierattr_init(pthread_barrierattr_t *attr);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 441 页

int pthread_barrierattr_setshared(pthread_barrierattr_t *attr, int pshared);
<pthread.h>
pshared: PTHREAD_PROCESS_PRIVATE, PTHREAD_PROCESS_SHARED
返回值：成功返回 0，失败返回错误编号
第 441 页

int pthread_barrier_destroy(pthread_barrier_t *barrier);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 418 页

int pthread_barrier_init(pthread_barrier_t *restrict barrier, const pthread_barrierattr_t * restrict attr, unsigned int count);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 418 页

int pthread_barrier_wait(pthread_barrier_t *barrier);
<pthread.h>
返回值：成功返回 0 或 PTHREAD_BARRIER_SERIAL_THREAD，失败返回错误编号

int pthread_cancel(pthread_t tid);
<pthread.h>
返回值：成功返回 0，失败返回错误编号

void pthread_cleanup_pop(int execute);
<pthread.h>

void pthread_cleanup_push(void (*rtn)(void *), void *arg);
<pthread.h>

int pthread_condattr_destroy(pthread_condattr_t *attr);
<pthread.h>
返回值：成功返回 0，失败返回错误编号

int pthread_condattr_getclock(const pthread_condattr_t *restrict attr, clockid_t *restrict clock_id);
<pthread.h>
返回值：成功返回 0，失败返回错误编号

int pthread_condattr_getpshared(const pthread_condattr_t *restrict attr, int *restrict pshared);
<pthread.h>
返回值：成功返回 0，失败返回错误编号

int pthread_condattr_init(pthread_condattr_t *attr);
<pthread.h>
返回值：成功返回 0，失败返回错误编号

int pthread_cond_broadcast(pthread_cond_t *cond);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 415 页

int pthread_cond_destroy(pthread_cond_t *cond);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 414 页

int pthread_cond_init(pthread_cond_t *restrict cond,
    const pthread_condattr_t *restrict attr);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 414 页

int pthread_cond_signal(pthread_cond_t *cond);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 415 页

int pthread_cond_timedwait(pthread_cond_t *restrict cond,
    pthread_mutex_t *restrict mutex,
    const struct timespec *restrict timeout);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 414 页

int pthread_cond_wait(pthread_cond_t *restrict cond,
    pthread_mutex_t *restrict mutex);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 414 页

int pthread_create(pthread_t *restrict tidp,
    const pthread_attr_t *restrict attr,
    void *(*start_routine)(void *),
    void *restrict arg);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 385 页

int pthread_detach(pthread_t tid);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 397 页

int pthread_equal(pthread_t tid1, pthread_t tid2);
<pthread.h>
返回值：相等返回非零值，不相等返回 0
第 385 页

void pthread_exit(void *real_ptr);
<pthread.h>
第 389 页

## 个人简历

![](img/244bf0c3b6d0288ae397336907e37851_905_0.png)

姓名：张三

出生年月：1998年6月

联系电话：138-0000-0000

电子邮箱：zhangsan@email.com

现居地：上海市浦东新区

求职意向：软件工程师

## 教育背景

2016.09 - 2020.06  上海大学  计算机科学与技术专业  本科

主修课程：数据结构、操作系统、计算机网络、数据库原理、软件工程等。成绩排名前15%，获得校二等奖学金两次。

## 工作经历

2020.07 - 至今  ABC科技有限公司  后端开发工程师

- 参与公司核心电商平台的后端开发和维护，负责订单、支付等关键模块。
- 使用 Java 和 Spring Boot 框架进行服务端开发，优化接口性能，将平均响应时间从 300ms 降低至 80ms。
- 参与数据库设计和优化，编写复杂 SQL 查询，并通过索引优化和分库分表策略支撑高并发场景。
- 协助团队完成 CI/CD 流程的搭建和 Docker 容器化部署，提升交付效率约 40%。

## 专业技能

- 熟练掌握 Java、Python 编程语言。
- 熟悉 Spring Boot、MyBatis、Spring Cloud 等主流开发框架。
- 熟悉 MySQL、Redis、Kafka 等常用中间件和数据库。
- 了解前端技术栈 HTML/CSS/JavaScript，能进行简单的前端开发。

int pthread_mutexattr_setpshared(pthread_mutexattr_t *attr, int pshared);

<pthread.h>
pshared: PTHREAD_PROCESS_PRIVATE, PTHREAD_PROCESS_SHARED
返回值：成功返回 0，失败返回错误编号

第 431 页

int pthread_mutexattr_setrobust(pthread_mutexattr_t *attr, int robust);

<pthread.h>
robust: PTHREAD_MUTEX_ROBUST, PTHREAD_MUTEX_STALLED
返回值：成功返回 0，失败返回错误编号

第 432 页

int pthread_mutexattr_settype(pthread_mutexattr_t *attr, int type);

<pthread.h>
type: PTHREAD_MUTEX_NORMAL, PTHREAD_MUTEX_ERRORCHECK, PTHREAD_MUTEX_RECURSIVE, PTHREAD_MUTEX_DEFAULT
返回值：成功返回 0，失败返回错误编号

第 434 页

int pthread_mutex_consistent(pthread_mutex_t *mutex);

<pthread.h>
返回值：成功返回 0，失败返回错误编号

第 433 页

int pthread_mutex_destroy(pthread_mutex_t *mutex);

<pthread.h>
返回值：成功返回 0，失败返回错误编号

第 400 页

int pthread_mutex_unlock(pthread_mutex_t *mutex);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 400 页

int pthread_once(pthread_once_t *initflag, void (*initfn)(void));
<pthread.h>
pthread_once_t initflag = PTHREAD_ONCE_INIT;
返回值：成功返回 0，失败返回错误编号
第 448 页

int pthread_rwlockattr_destroy(pthread_rwlockattr_t *attr);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 439 页

int pthread_rwlockattr_getpshared(const pthread_rwlockattr_t *restrict attr,
    int *restrict pshared);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 440 页

int pthread_rwlockattr_init(pthread_rwlockattr_t *attr);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 439 页

int pthread_rwlockattr_setpshared(pthread_rwlockattr_t *attr,
    int pshared);
<pthread.h>
pshared: PTHREAD_PROCESS_PRIVATE,
         PTHREAD_PROCESS_SHARED
返回值：成功返回 0，失败返回错误编号
第 440 页

int pthread_rwlock_destroy(pthread_rwlock_t *rwlock);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 409 页

int pthread_rwlock_init(pthread_rwlock_t *restrict rwlock,
    const pthread_rwlockattr_t *restrict attr);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 409 页

int pthread_rwlock_rdlock(pthread_rwlock_t *rwlock);
<pthread.h>
返回值：成功返回 0，失败返回错误编号
第 410 页

