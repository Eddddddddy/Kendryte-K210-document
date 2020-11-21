# 平台相关\(BSP\)

## 概述 <a id="&#x6982;&#x8FF0;"></a>

平台相关的通用函数，核之间锁的相关操作。

## 功能描述 <a id="&#x529F;&#x80FD;&#x63CF;&#x8FF0;"></a>

提供获取当前运行程序的CPU核编号的接口以及启动第二个核的入口。

## API 参考 <a id="api-&#x53C2;&#x8003;"></a>

对应的头文件 `bsp.h`

为用户提供以下接口

* register\_core1
* current\_coreid
* read\_cycle
* spinlock\_lock
* spinlock\_unlock
* spinlock\_trylock
* corelock\_lock
* corelock\_trylock
* corelock\_unlock
* sys\_register\_putchar
* sys\_register\_getchar
* sys\_stdin\_flush
* get\_free\_heap\_size
* printk

### register\_core1 <a id="registercore1"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

向1核注册函数，并启动1核。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int register_core1(core_function func, void *ctx)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| func | 向1核注册的函数 | 输入 |
| ctx | 函数的参数，没有设置为NULL | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### current\_coreid <a id="currentcoreid"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

获取当前CPU核编号。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
#define current_coreid()       read_csr(mhartid)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

无。

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

当前所在CPU核的编号。

#### read\_cycle <a id="readcycle"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

获取CPU开机至今的时钟数。可以用使用这个函数精准的确定程序运行时钟。可以配合sysctl\_clock\_get\_freq\(SYSCTL\_CLOCK\_CPU\)计算运行的时间。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
#define read_cycle()        read_csr(mcycle)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

无。

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

开机至今的CPU时钟数。

### spinlock\_lock <a id="spinlocklock"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

自旋锁，不可嵌套，不建议在中断使用，中断中可以使用spinlock\_trylock。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void spinlock_lock(spinlock_t *lock)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

自旋锁，要使用全局变量。

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### spinlock\_trylock <a id="spinlocktrylock"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

获取自旋锁，成功获取锁会返回0，失败返回-1。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int spinlock_trylock(spinlock_t *lock)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

自旋锁，要使用全局变量。

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### spinlock\_unlock <a id="spinlockunlock"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

自旋锁解锁。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void spinlock_unlock(spinlock_t *lock)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

核间锁，要使用全局变量，参见举例。

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### corelock\_lock <a id="corelocklock"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

获取核间锁，核之间互斥的锁，同核内该锁会嵌套，只有异核之间会阻塞。不建议在中断使用该函数，中断中可以使用corelock\_trylock。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void corelock_lock(corelock_t *lock)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

核间锁，要使用全局变量，参见举例。

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### corelock\_trylock <a id="corelocktrylock"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

获取核间锁，同核时锁会嵌套，异核时非阻塞。成功获取锁会返回0，失败返回-1。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
corelock_trylock(corelock_t *lock)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

核间锁，要使用全局变量，参见举例。

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### corelock\_unlock <a id="corelockunlock"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

核间锁解锁。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void corelock_unlock(corelock_t *lock)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

核间锁，要使用全局变量，参见举例。

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### sys\_register\_getchar <a id="sysregistergetchar"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

注册系统输入回调函数，scanf时会调用该函数。系统默认使用UART3，如果需要修改UART则调用uart\_debug\_init函数，具体请到uart章节查看该函数。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void sys_register_getchar(sys_getchar_t getchar);
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| getchar | 回调函数 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### sys\_register\_putchar <a id="sysregisterputchar"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

注册系统输出回调函数，printf时会调用该函数。系统默认使用UART3，如果需要修改UART则调用uart\_debug\_init函数，具体请到uart章节查看该函数。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void sys_register_putchar(sys_putchar_t putchar)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| putchar | 回调函数 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### sys\_stdin\_flush <a id="sysstdinflush"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

清理stdin缓存。

#### 参数 <a id="&#x53C2;&#x6570;"></a>

无。

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### get\_free\_heap\_size <a id="getfreeheapsize"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

获取空闲内存大小。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
size_t get_free_heap_size(void)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

无。

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

空闲内存大小。

### 举例 <a id="&#x4E3E;&#x4F8B;"></a>

```text

#include 
#include "bsp.h"
#include 
#include "sysctl.h"

corelock_t lock;

uint64_t get_time(void)
{
    uint64_t v_cycle = read_cycle();
    return v_cycle * 1000000 / sysctl_clock_get_freq(SYSCTL_CLOCK_CPU);
}

int core1_function(void *ctx)
{
    uint64_t core = current_coreid();
    printf("Core %ld Hello world\n", core);
    while(1)
    {
        uint64_t start = get_time();
        corelock_lock(&lock);
        printf("Core %ld Hello world\n", core);
        sleep(1);
        corelock_unlock(&lock);
        uint64_t stop = get_time();
        printf("Core %ld lock time is %ld us\n",core, stop - start);
        usleep(10);
    }
}

int main(void)
{
    uint64_t core = current_coreid();
    printf("Core %ld Hello world\n", core);
    register_core1(core1_function, NULL);
    while(1)
    {
        corelock_lock(&lock);
        sleep(1);
        printf("1> Core %ld sleep 1\n", core);
        corelock_lock(&lock);
        sleep(2);
        printf("2> Core %ld sleep 2\n", core);
        printf("2> Core unlock\n");
        corelock_unlock(&lock);
        sleep(1);
        printf("1> Core unlock\n");
        corelock_unlock(&lock);
        usleep(10);
    }
}
```

## 数据类型 <a id="&#x6570;&#x636E;&#x7C7B;&#x578B;"></a>

相关数据类型、数据结构定义如下：

* core\_function：CPU核调用的函数。
* spinlock\_t：自旋锁。
* corelock\_t：核间锁。

### core\_function <a id="corefunction"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

CPU核调用的函数。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef int (*core_function)(void *ctx);
```

### spinlock\_t <a id="spinlockt"></a>

自旋锁。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef struct _spinlock
{
    int lock;
} spinlock_t;
```

### corelock\_t <a id="corelockt"></a>

核间锁。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef struct _corelock
{
    spinlock_t lock;
    int count;
    int core;
} corelock_t;
```

