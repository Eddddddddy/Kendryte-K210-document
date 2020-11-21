# 高速通用异步收发传输器 \(UARTHS\)

## 概述 <a id="&#x6982;&#x8FF0;"></a>

嵌入式应用通常要求一个简单的并且占用系统资源少的方法来传输数据。高速通用异步收发传输器 \(UARTHS\) 即可以满足这些要求，它能够灵活地与外部设备进行全双工数据交换。 目前系统使用该串口做为调试串口，printf时会调用该串口输出。

## 功能描述 <a id="&#x529F;&#x80FD;&#x63CF;&#x8FF0;"></a>

UARTHS 模块具有以下功能：

* 配置 UARTHS 参数
* 自动收取数据到缓冲区

## API 参考 <a id="api-&#x53C2;&#x8003;"></a>

对应的头文件 `uarths.h`

为用户提供以下接口

* uarths\_init
* uarths\_config
* uarths\_receive\_data
* uarths\_send\_data
* uarths\_set\_irq
* uarths\_get\_interrupt\_mode
* uarths\_set\_interrupt\_cnt

### uarths\_init <a id="uarthsinit"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

初始化UARTHS，系统默认波特率为115200 8bit 1位停止位 无检验位。因为uarths时钟源为PLL0，在设置PLL0后需要重新调用该函数设置波特率，否则会打印乱码。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void uarths_init(void)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

无。

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### uarths\_config <a id="uarthsconfig"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置UARTHS的参数。默认8bit数据，无校验位。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void uarths_config(uint32_t baud_rate, uarths_stopbit_t stopbit)
```

### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| baud\_rate | 波特率 | 输入 |
| stopbit | 停止位 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### uarths\_receive\_data <a id="uarthsreceivedata"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

通过UARTHS读取数据。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
size_t uarths_receive_data(uint8_t *buf, size_t buf_len)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| buf | 接收数据 | 输出 |
| buf\_len | 接收数据的长度 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

已接收到的数据长度。

### uarths\_send\_data <a id="uarthssenddata"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

通过UART发送数据。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
size_t uarths_send_data(const uint8_t *buf, size_t buf_len)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| buf | 待发送数据 | 输入 |
| buf\_len | 待发送数据的长度 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

已发送数据的长度。

### uarths\_set\_irq <a id="uarthssetirq"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置UARTHS中断回调函数。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void uarths_set_irq(uarths_interrupt_mode_t interrupt_mode, plic_irq_callback_t uarths_callback, void *ctx, uint32_t priority)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| interrupt\_mode | 中断类型 | 输入 |
| uarths\_callback | 中断回调函数 | 输入 |
| ctx | 回调函数的参数 | 输入 |
| priority | 中断优先级 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### uarths\_get\_interrupt\_mode <a id="uarthsgetinterruptmode"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

获取UARTHS的中断类型。接收、发送或接收发送同时中断。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
uarths_interrupt_mode_t uarths_get_interrupt_mode(void)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

无

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

当前中断的类型。

### uarths\_set\_interrupt\_cnt <a id="uarthssetinterruptcnt"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置UARTHS中断时的FIFO深度。 当中断类型为UARTHS\_SEND\_RECEIVE，发送接收FIFO中断深度均为cnt;

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void uarths_set_interrupt_cnt(uarths_interrupt_mode_t interrupt_mode, uint8_t cnt)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| interrupt\_mode | 中断类型 | 输入 |
| cnt | FIFO深度 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### 举例 <a id="&#x4E3E;&#x4F8B;"></a>

```text

    int uarths_irq(void *ctx)
    {
        if(!uarths_receive_data((uint8_t *)&receive_char, 1))
            printf("Uarths receive ERR!\n");
        return 0;
    }

    plic_init();
    uarths_set_interrupt_cnt(UARTHS_RECEIVE , 0);
    uarths_set_irq(UARTHS_RECEIVE ,uarths_irq, NULL, 4);
    sysctl_enable_irq();
```

## 数据类型 <a id="&#x6570;&#x636E;&#x7C7B;&#x578B;"></a>

相关数据类型、数据结构定义如下：

* uarths\_interrupt\_mode\_t：中断类型。
* uarths\_stopbit\_t：停止位。

### uarths\_interrupt\_mode\_t <a id="uarthsinterruptmodet"></a>

### 描述 <a id="&#x63CF;&#x8FF0;"></a>

UARTHS中断类型。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _uarths_interrupt_mode
{
    UARTHS_SEND = 1,
    UARTHS_RECEIVE = 2,
    UARTHS_SEND_RECEIVE = 3,
} uarths_interrupt_mode_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| UARTHS\_SEND | 发送中断 |
| UARTHS\_RECEIVE | 接收中断 |
| UARTHS\_SEND\_RECEIVE | 发送接收中断 |

### uarths\_stopbit\_t <a id="uarthsstopbitt"></a>

#### 描述： <a id="&#x63CF;&#x8FF0;&#xFF1A;"></a>

UARTHS停止位。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _uarths_stopbit
{
    UART_STOP_1,
    UART_STOP_2
} uarths_stopbit_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| UART\_STOP\_1 | 1位停止位 |
| UART\_STOP\_2 | 2位停止位 |

