# 定时器 \(TIMER\)

## 概述 <a id="&#x6982;&#x8FF0;"></a>

芯片有3个定时器，每个定时器有4路通道。可以配置为PWM，详见PWM说明。

## 功能描述 <a id="&#x529F;&#x80FD;&#x63CF;&#x8FF0;"></a>

TIMER 模块具有以下功能：

* 启用或禁用定时器
* 配置定时器触发间隔
* 配置定时器触发处理程序

## API 参考 <a id="api-&#x53C2;&#x8003;"></a>

对应的头文件 `timer.h`

为用户提供以下接口

* timer\_init
* timer\_set\_interval
* timer\_set\_irq \(0.6.0后不再支持，请使用timer\_irq\_register\)
* timer\_set\_enable
* timer\_irq\_register
* timer\_irq\_deregister

### timer\_init <a id="timerinit"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

初始化定时器。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void timer_init(timer_device_number_t timer_number)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| timer\_number | 定时器号 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### timer\_set\_interval <a id="timersetinterval"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置定时间隔。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
size_t timer_set_interval(timer_device_number_t timer_number, timer_channel_number_t channel, size_t nanoseconds)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| timer\_number | 定时器号 | 输入 |
| channel | 定时器通道号 | 输入 |
| nanoseconds | 时间间隔（纳秒） | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

实际的触发间隔（纳秒）。

### timer\_set\_irq <a id="timersetirq"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置定时器触发中断回调函数，该函数已废弃，替代函数为timer\_irq\_register。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void timer_set_irq(timer_device_number_t timer_number, timer_channel_number_t channel, void(*func)(),  uint32_t priority)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| timer\_number | 定时器号 | 输入 |
| channel | 定时器通道号 | 输入 |
| func | 回调函数 | 输入 |
| priority | 中断优先级 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### timer\_set\_enable <a id="timersetenable"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

使能禁用定时器。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void timer_set_enable(timer_device_number_t timer_number, timer_channel_number_t channel, uint32_t enable)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| timer\_number | 定时器号 | 输入 |
| channel | 定时器通道号 | 输入 |
| enable | 使能禁用定时器 0：禁用 1：使能 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### timer\_irq\_register <a id="timerirqregister"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

注册定时器触发中断回调函数。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int timer_irq_register(timer_device_number_t device, timer_channel_number_t channel, int is_single_shot, uint32_t priority, timer_callback_t callback, void *ctx);
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| device | 定时器号 | 输入 |
| channel | 定时器通道号 | 输入 |
| is\_single\_shot | 是否单次中断 | 输入 |
| priority | 中断优先级 | 输入 |
| callback | 中断回调函数 | 输入 |
| ctx | 回调函数参数 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### timer\_irq\_deregister <a id="timerirqderegister"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

注销定时器中断函数。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int timer_irq_deregister(timer_device_number_t device, timer_channel_number_t channel)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| device | 定时器号 | 输入 |
| channel | 定时器通道号 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### 举例 <a id="&#x4E3E;&#x4F8B;"></a>

```text

void irq_time(void)
{
    printf("Time OK!\n");
}
plic_init();
timer_init(TIMER_DEVICE_0);
timer_set_interval(TIMER_DEVICE_0, TIMER_CHANNEL_0, 1e9);
timer_set_irq(TIMER_DEVICE_0, TIMER_CHANNEL_0, irq_time, 1);
timer_set_enable(TIMER_DEVICE_0, TIMER_CHANNEL_0, 1);
sysctl_enable_irq();
```

## 数据类型 <a id="&#x6570;&#x636E;&#x7C7B;&#x578B;"></a>

相关数据类型、数据结构定义如下：

* timer\_device\_number\_t：定时器编号。
* timer\_channel\_number\_t：定时器通道号。
* timer\_callback\_t：定时器回调函数。

### timer\_device\_number\_t <a id="timerdevicenumbert"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

定时器编号

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _timer_deivce_number
{
    TIMER_DEVICE_0,
    TIMER_DEVICE_1,
    TIMER_DEVICE_2,
    TIMER_DEVICE_MAX,
} timer_device_number_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| TIMER\_DEVICE\_0 | 定时器 0 |
| TIMER\_DEVICE\_1 | 定时器 1 |
| TIMER\_DEVICE\_2 | 定时器 2 |

### timer\_channel\_number\_t <a id="timerchannelnumbert"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

定时器通道号。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _timer_channel_number
{
    TIMER_CHANNEL_0,
    TIMER_CHANNEL_1,
    TIMER_CHANNEL_2,
    TIMER_CHANNEL_3,
    TIMER_CHANNEL_MAX,
} timer_channel_number_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| TIMER\_CHANNEL\_0 | 定时器通道 0 |
| TIMER\_CHANNEL\_1 | 定时器通道 1 |
| TIMER\_CHANNEL\_2 | 定时器通道 2 |
| TIMER\_CHANNEL\_3 | 定时器通道 3 |

### timer\_callback\_t <a id="timercallbackt"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

定时器回调函数。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef int (*timer_callback_t)(void *ctx);
```

