# 外部中断\(INTERRUPT\)

## 概述 <a id="&#x6982;&#x8FF0;"></a>

可以将任一外部中断源单独分配到每个 CPU 的外部中断上。这提供了强大的灵活性，能适应不同的应用需求。

## 功能描述 <a id="&#x529F;&#x80FD;&#x63CF;&#x8FF0;"></a>

PLIC 模块具有以下功能：

* 启用或禁用中断
* 设置中断处理程序
* 配置中断优先级

## API参考 <a id="api&#x53C2;&#x8003;"></a>

对应头文件 `plic.h`

为用户提供以下接口

* plic\_init
* plic\_irq\_enable
* plic\_irq\_disable
* plic\_set\_priority
* plic\_get\_priority
* plic\_irq\_register
* plic\_irq\_deregister

### plic\_init <a id="plicinit"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

PLIC初始化外部中断。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void plic_init(void)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

无。

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### plic\_irq\_enable <a id="plicirqenable"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

使能外部中断。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int plic_irq_enable(plic_irq_t irq_number)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| irq\_number | 中断号 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### plic\_irq\_disable <a id="plicirqdisable"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

禁用外部中断。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int plic_irq_disable(plic_irq_t irq_number)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| irq\_number | 中断号 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### plic\_set\_priority <a id="plicsetpriority"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置中断优先级。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int plic_set_priority(plic_irq_t irq_number, uint32_t priority)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| irq\_number | 中断号 | 输入 |
| priority | 中断优先级 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### plic\_get\_priority <a id="plicgetpriority"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

获取中断优先级。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
uint32_t plic_get_priority(plic_irq_t irq_number)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| irq\_number | 中断号 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

irq\_number中断的优先级。

### plic\_irq\_register <a id="plicirqregister"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

注册外部中断函数。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int plic_irq_register(plic_irq_t irq, plic_irq_callback_t callback, void* ctx)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| irq | 中断号 | 输入 |
| callback | 中断回调函数 | 输入 |
| ctx | 回调函数的参数 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### plic\_irq\_deregister <a id="plicirqderegister"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

注销外部中断函数。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int plic_irq_deregister(plic_irq_t irq)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| irq | 中断号 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### 举例 <a id="&#x4E3E;&#x4F8B;"></a>

```text

int count = 0;
int gpiohs_pin_onchange_isr(void *ctx)
{
    int *userdata = (int *)ctx;
    *userdata++;
}
plic_init();
plic_set_priority(IRQN_GPIOHS0_INTERRUPT, 1);
plic_irq_register(IRQN_GPIOHS0_INTERRUPT, gpiohs_pin_onchange_isr, &count);
plic_irq_enable(IRQN_GPIOHS0_INTERRUPT);
sysctl_enable_irq();
```

## 数据类型 <a id="&#x6570;&#x636E;&#x7C7B;&#x578B;"></a>

相关数据类型、数据结构定义如下：

* plic\_irq\_t：外部中断号。
* plic\_irq\_callback\_t：外部中断回调函数。

### plic\_irq\_t <a id="plicirqt"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

外部中断号。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _plic_irq
{
    IRQN_NO_INTERRUPT        = 0, 
    IRQN_SPI0_INTERRUPT      = 1, 
    IRQN_SPI1_INTERRUPT      = 2, 
    IRQN_SPI_SLAVE_INTERRUPT = 3, 
    IRQN_SPI3_INTERRUPT      = 4, 
    IRQN_I2S0_INTERRUPT      = 5, 
    IRQN_I2S1_INTERRUPT      = 6, 
    IRQN_I2S2_INTERRUPT      = 7, 
    IRQN_I2C0_INTERRUPT      = 8, 
    IRQN_I2C1_INTERRUPT      = 9, 
    IRQN_I2C2_INTERRUPT      = 10, 
    IRQN_UART1_INTERRUPT     = 11, 
    IRQN_UART2_INTERRUPT     = 12, 
    IRQN_UART3_INTERRUPT     = 13, 
    IRQN_TIMER0A_INTERRUPT   = 14, 
    IRQN_TIMER0B_INTERRUPT   = 15, 
    IRQN_TIMER1A_INTERRUPT   = 16, 
    IRQN_TIMER1B_INTERRUPT   = 17, 
    IRQN_TIMER2A_INTERRUPT   = 18, 
    IRQN_TIMER2B_INTERRUPT   = 19, 
    IRQN_RTC_INTERRUPT       = 20, 
    IRQN_WDT0_INTERRUPT      = 21, 
    IRQN_WDT1_INTERRUPT      = 22, 
    IRQN_APB_GPIO_INTERRUPT  = 23, 
    IRQN_DVP_INTERRUPT       = 24, 
    IRQN_AI_INTERRUPT        = 25, 
    IRQN_FFT_INTERRUPT       = 26, 
    IRQN_DMA0_INTERRUPT      = 27, 
    IRQN_DMA1_INTERRUPT      = 28, 
    IRQN_DMA2_INTERRUPT      = 29, 
    IRQN_DMA3_INTERRUPT      = 30, 
    IRQN_DMA4_INTERRUPT      = 31, 
    IRQN_DMA5_INTERRUPT      = 32, 
    IRQN_UARTHS_INTERRUPT    = 33, 
    IRQN_GPIOHS0_INTERRUPT   = 34, 
    IRQN_GPIOHS1_INTERRUPT   = 35, 
    IRQN_GPIOHS2_INTERRUPT   = 36, 
    IRQN_GPIOHS3_INTERRUPT   = 37, 
    IRQN_GPIOHS4_INTERRUPT   = 38, 
    IRQN_GPIOHS5_INTERRUPT   = 39, 
    IRQN_GPIOHS6_INTERRUPT   = 40, 
    IRQN_GPIOHS7_INTERRUPT   = 41, 
    IRQN_GPIOHS8_INTERRUPT   = 42, 
    IRQN_GPIOHS9_INTERRUPT   = 43, 
    IRQN_GPIOHS10_INTERRUPT  = 44, 
    IRQN_GPIOHS11_INTERRUPT  = 45, 
    IRQN_GPIOHS12_INTERRUPT  = 46, 
    IRQN_GPIOHS13_INTERRUPT  = 47, 
    IRQN_GPIOHS14_INTERRUPT  = 48, 
    IRQN_GPIOHS15_INTERRUPT  = 49, 
    IRQN_GPIOHS16_INTERRUPT  = 50, 
    IRQN_GPIOHS17_INTERRUPT  = 51, 
    IRQN_GPIOHS18_INTERRUPT  = 52, 
    IRQN_GPIOHS19_INTERRUPT  = 53, 
    IRQN_GPIOHS20_INTERRUPT  = 54, 
    IRQN_GPIOHS21_INTERRUPT  = 55, 
    IRQN_GPIOHS22_INTERRUPT  = 56, 
    IRQN_GPIOHS23_INTERRUPT  = 57, 
    IRQN_GPIOHS24_INTERRUPT  = 58, 
    IRQN_GPIOHS25_INTERRUPT  = 59, 
    IRQN_GPIOHS26_INTERRUPT  = 60, 
    IRQN_GPIOHS27_INTERRUPT  = 61, 
    IRQN_GPIOHS28_INTERRUPT  = 62, 
    IRQN_GPIOHS29_INTERRUPT  = 63, 
    IRQN_GPIOHS30_INTERRUPT  = 64, 
    IRQN_GPIOHS31_INTERRUPT  = 65, 
    IRQN_MAX
} plic_irq_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| IRQN\_NO\_INTERRUPT | 不存在 |
| IRQN\_SPI0\_INTERRUPT | SPI0中断 |
| IRQN\_SPI1\_INTERRUPT | SPI1中断 |
| IRQN\_SPI\_SLAVE\_INTERRUPT | 从SPI中断 |
| IRQN\_SPI3\_INTERRUPT | SPI3中断 |
| IRQN\_I2S0\_INTERRUPT | I2S0 中断 |
| IRQN\_I2S1\_INTERRUPT | I2S1 中断 |
| IRQN\_I2S2\_INTERRUPT | I2S2 中断 |
| IRQN\_I2C0\_INTERRUPT | I2C0 中断 |
| IRQN\_I2C1\_INTERRUPT | I2C1 中断 |
| IRQN\_I2C2\_INTERRUPT | I2C2 中断 |
| IRQN\_UART1\_INTERRUPT | UART1中断 |
| IRQN\_UART2\_INTERRUPT | UART2中断 |
| IRQN\_UART3\_INTERRUPT | UART3中断 |
| IRQN\_TIMER0A\_INTERRUPT | TIMER0通道0和1中断 |
| IRQN\_TIMER0B\_INTERRUPT | TIMER0通道2和3中断 |
| IRQN\_TIMER1A\_INTERRUPT | TIMER1通道0和1中断 |
| IRQN\_TIMER1B\_INTERRUPT | TIMER1通道2和3中断 |
| IRQN\_TIMER2A\_INTERRUPT | TIMER2通道0和1中断 |
| IRQN\_TIMER2B\_INTERRUPT | TIMER2通道2和3中断 |
| IRQN\_RTC\_INTERRUPT | RTC 滴答中断和报警中断 |
| IRQN\_WDT0\_INTERRUPT | 看门狗0中断 |
| IRQN\_WDT1\_INTERRUPT | 看门狗1中断 |
| IRQN\_APB\_GPIO\_INTERRUPT | 普通GPIO中断 |
| IRQN\_DVP\_INTERRUPT | 数字摄像头（DVP）中断 |
| IRQN\_AI\_INTERRUPT | AI 加速器中断 |
| IRQN\_FFT\_INTERRUPTFFT | 傅里叶加速器中断 |
| IRQN\_DMA0\_INTERRUPT | DMA 通道0中断 |
| IRQN\_DMA1\_INTERRUPT | DMA 通道1中断 |
| IRQN\_DMA2\_INTERRUPT | DMA 通道2中断 |
| IRQN\_DMA3\_INTERRUPT | DMA 通道3中断 |
| IRQN\_DMA4\_INTERRUPT | DMA 通道4中断 |
| IRQN\_DMA5\_INTERRUPT | DMA 通道5中断 |
| IRQN\_UARTHS\_INTERRUPT | 高速UART中断 |
| IRQN\_GPIOHS0\_INTERRUPT | 高速GPIO0中断 |
| IRQN\_GPIOHS1\_INTERRUPT | 高速GPIO1中断 |
| IRQN\_GPIOHS2\_INTERRUPT | 高速GPIO2中断 |
| IRQN\_GPIOHS3\_INTERRUPT | 高速GPIO3中断 |
| IRQN\_GPIOHS4\_INTERRUPT | 高速GPIO4中断 |
| IRQN\_GPIOHS5\_INTERRUPT | 高速GPIO5中断 |
| IRQN\_GPIOHS6\_INTERRUPT | 高速GPIO6中断 |
| IRQN\_GPIOHS7\_INTERRUPT | 高速GPIO7中断 |
| IRQN\_GPIOHS8\_INTERRUPT | 高速GPIO8中断 |
| IRQN\_GPIOHS9\_INTERRUPT | 高速GPIO9中断 |
| IRQN\_GPIOHS10\_INTERRUPT | 高速GPIO10中断 |
| IRQN\_GPIOHS11\_INTERRUPT | 高速GPIO11中断 |
| IRQN\_GPIOHS12\_INTERRUPT | 高速GPIO12中断 |
| IRQN\_GPIOHS13\_INTERRUPT | 高速GPIO13中断 |
| IRQN\_GPIOHS14\_INTERRUPT | 高速GPIO14中断 |
| IRQN\_GPIOHS15\_INTERRUPT | 高速GPIO15中断 |
| IRQN\_GPIOHS16\_INTERRUPT | 高速GPIO16中断 |
| IRQN\_GPIOHS17\_INTERRUPT | 高速GPIO17中断 |
| IRQN\_GPIOHS18\_INTERRUPT | 高速GPIO18中断 |
| IRQN\_GPIOHS19\_INTERRUPT | 高速GPIO19中断 |
| IRQN\_GPIOHS20\_INTERRUPT | 高速GPIO20中断 |
| IRQN\_GPIOHS21\_INTERRUPT | 高速GPIO21中断 |
| IRQN\_GPIOHS22\_INTERRUPT | 高速GPIO22中断 |
| IRQN\_GPIOHS23\_INTERRUPT | 高速GPIO23中断 |
| IRQN\_GPIOHS24\_INTERRUPT | 高速GPIO24中断 |
| IRQN\_GPIOHS25\_INTERRUPT | 高速GPIO25中断 |
| IRQN\_GPIOHS26\_INTERRUPT | 高速GPIO26中断 |
| IRQN\_GPIOHS27\_INTERRUPT | 高速GPIO27中断 |
| IRQN\_GPIOHS28\_INTERRUPT | 高速GPIO28中断 |
| IRQN\_GPIOHS29\_INTERRUPT | 高速GPIO29中断 |
| IRQN\_GPIOHS30\_INTERRUPT | 高速GPIO30中断 |
| IRQN\_GPIOHS31\_INTERRUPT | 高速GPIO31中断 |

### plic\_irq\_callback\_t <a id="plicirqcallbackt"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

外部中断回调函数。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef int (*plic_irq_callback_t)(void *ctx);
```

