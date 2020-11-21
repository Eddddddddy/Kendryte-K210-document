# 系统控制

## 概述 <a id="&#x6982;&#x8FF0;"></a>

系统控制模块提供对操作系统的配置功能。

## 功能描述 <a id="&#x529F;&#x80FD;&#x63CF;&#x8FF0;"></a>

系统控制模块具有以下功能：

* 设置 PLL CPU 时钟频率。
* 设置各个模块时钟的分频值。
* 获取各个模块的时钟频率。
* 使能、禁用、复位各个模块。
* 设置DMA请求源。
* 使能禁用系统中断。

## API 参考 <a id="api-&#x53C2;&#x8003;"></a>

对应的头文件 `sysctl.h`

为用户提供以下接口

* sysctl\_cpu\_set\_freq
* sysctl\_pll\_set\_freq
* sysctl\_pll\_get\_freq
* sysctl\_pll\_enable
* sysctl\_pll\_disable
* sysctl\_clock\_set\_threshold
* sysctl\_clock\_get\_threshold
* sysctl\_clock\_set\_clock\_select
* sysctl\_clock\_get\_clock\_select
* sysctl\_clock\_get\_freq
* sysctl\_clock\_enable
* sysctl\_clock\_disable
* sysctl\_reset
* sysctl\_dma\_select
* sysctl\_set\_power\_mode
* sysctl\_enable\_irq
* sysctl\_disable\_irq
* sysctl\_get\_time\_us
* sysctl\_get\_reset\_status

### sysctl\_cpu\_set\_freq <a id="sysctlcpusetfreq"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置CPU工作频率。是通过修改PLL0的频率实现的。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
uint32_t sysctl_cpu_set_freq(uint32_t freq)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| freq | 要设置的频率（Hz） | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

设置后的实际频率（Hz）。

### sysctl\_set\_pll\_frequency <a id="sysctlsetpllfrequency"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置PLL频率。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
uint32_t sysctl_pll_set_freq(sysctl_pll_t pll, uint32_t pll_freq)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| pll | PLL编号 | 输入 |
| pll\_freq | 要设置的频率（Hz） | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

设置后的实际频率（Hz）。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
uint32_t sysctl_pll_get_freq(sysctl_pll_t pll)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| pll | PLL编号 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

对应PLL的频率（Hz）。

### sysctl\_pll\_enable <a id="sysctlpllenable"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

使能对应的PLL。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int sysctl_pll_enable(sysctl_pll_t pll)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| pll | PLL编号 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### sysctl\_pll\_disable <a id="sysctlplldisable"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

禁用对应PLL。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int sysctl_pll_disable(sysctl_pll_t pll)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| pll | PLL编号 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### sysctl\_clock\_set\_threshold <a id="sysctlclocksetthreshold"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置对应时钟的分频值。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void sysctl_clock_set_threshold(sysctl_threshold_t which, int threshold)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| which | 设置的时钟 | 输入 |
| threshold | 分频值 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### sysctl\_clock\_get\_threshold <a id="sysctlclockgetthreshold"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

获取对应时钟的分频值。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int sysctl_clock_get_threshold(sysctl_threshold_t which)
```

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| which | 时钟 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

对应时钟的分频值。

### sysctl\_clock\_set\_clock\_select <a id="sysctlclocksetclockselect"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置时钟源。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int sysctl_clock_set_clock_select(sysctl_clock_select_t which, int select)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| which | 时钟 | 输入 |
| select | 时钟源 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### sysctl\_clock\_get\_clock\_select <a id="sysctlclockgetclockselect"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

获取时钟对应的时钟源。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int sysctl_clock_get_clock_select(sysctl_clock_select_t which)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| which | 时钟 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

时钟对应的时钟源。

### sysctl\_clock\_get\_freq <a id="sysctlclockgetfreq"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

获取时钟的频率。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
uint32_t sysctl_clock_get_freq(sysctl_clock_t clock)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| clock | 时钟 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

时钟的频率（Hz）

### sysctl\_clock\_enable <a id="sysctlclockenable"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

使能时钟。PLL要使用sysctl\_pll\_enable。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int sysctl_clock_enable(sysctl_clock_t clock)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| clock | 时钟 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### sysctl\_clock\_disable <a id="sysctlclockdisable"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

禁用时钟，PLL使用sysctl\_pll\_disable。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int sysctl_clock_disable(sysctl_clock_t clock)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| clock | 时钟 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### sysctl\_reset <a id="sysctlreset"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

复位各个模块。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void sysctl_reset(sysctl_reset_t reset)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| reset | 预复位模块 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### sysctl\_dma\_select <a id="sysctldmaselect"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置DMA请求源。与DMAC的API配合使用。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int sysctl_dma_select(sysctl_dma_channel_t channel, sysctl_dma_select_t select)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| channel | DMA通道号 | 输入 |
| select | DMA请求源 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### sysctl\_set\_power\_mode <a id="sysctlsetpowermode"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置FPIOA的对应电源域的电压。

#### 原型 <a id="&#x539F;&#x578B;"></a>

```text
void sysctl_set_power_mode(sysctl_power_bank_t power_bank, sysctl_io_power_mode_t io_power_mode)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| power\_bank | IO电源域编号 | 输入 |
| io\_power\_mode | 设置的电压值1.8V或3.3V | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### sysctl\_enable\_irq <a id="sysctlenableirq"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

使能系统中断，如果使用中断一定要开启系统中断。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void sysctl_enable_irq(void)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

无。

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### sysctl\_disable\_irq <a id="sysctldisableirq"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

禁用系统中断。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void sysctl_disable_irq(void)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

无。

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### sysctl\_get\_time\_us <a id="sysctlgettimeus"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

开机至今的时间（微秒）。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
uint64_t sysctl_get_time_us(void)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

无。

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

开机至今的时间（微秒）。

### sysctl\_get\_reset\_status <a id="sysctlgetresetstatus"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

获取复位状态。参见sysctl\_reset\_enum\_status\_t说明。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
sysctl_reset_enum_status_t sysctl_get_reset_status(void)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

无。

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

复位状态。

## 数据类型 <a id="&#x6570;&#x636E;&#x7C7B;&#x578B;"></a>

相关数据类型、数据结构定义如下：

* sysctl\_pll\_t：PLL编号。
* sysctl\_threshold\_t：设置分频值时各模块编号。
* sysctl\_clock\_select\_t：设置时钟源时各模块编号。
* sysctl\_clock\_t：各个模块的编号。
* sysctl\_reset\_t：复位时各个模块的编号。
* sysctl\_dma\_channel\_t：DMA通道号。
* sysctl\_dma\_select\_t：DMA请求源编号。
* sysctl\_power\_bank\_t：电源域编号。
* sysctl\_io\_power\_mode\_t：IO输出电压值。
* sysctl\_reset\_enum\_status\_t：复位状态。

### sysctl\_pll\_t <a id="sysctlpllt"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

PLL编号。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _sysctl_pll_t
{
    SYSCTL_PLL0,
    SYSCTL_PLL1,
    SYSCTL_PLL2,
    SYSCTL_PLL_MAX
} sysctl_pll_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| SYSCTL\_PLL0 | PLL0 |
| SYSCTL\_PLL1 | PLL1 |
| SYSCTL\_PLL2 | PLL2 |

### sysctl\_threshold\_t <a id="sysctlthresholdt"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置分频值各模块编号。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _sysctl_threshold_t
{
    SYSCTL_THRESHOLD_ACLK,
    SYSCTL_THRESHOLD_APB0,
    SYSCTL_THRESHOLD_APB1,
    SYSCTL_THRESHOLD_APB2,
    SYSCTL_THRESHOLD_SRAM0,
    SYSCTL_THRESHOLD_SRAM1,
    SYSCTL_THRESHOLD_AI,
    SYSCTL_THRESHOLD_DVP,
    SYSCTL_THRESHOLD_ROM,
    SYSCTL_THRESHOLD_SPI0,
    SYSCTL_THRESHOLD_SPI1,
    SYSCTL_THRESHOLD_SPI2,
    SYSCTL_THRESHOLD_SPI3,
    SYSCTL_THRESHOLD_TIMER0,
    SYSCTL_THRESHOLD_TIMER1,
    SYSCTL_THRESHOLD_TIMER2,
    SYSCTL_THRESHOLD_I2S0,
    SYSCTL_THRESHOLD_I2S1,
    SYSCTL_THRESHOLD_I2S2,
    SYSCTL_THRESHOLD_I2S0_M,
    SYSCTL_THRESHOLD_I2S1_M,
    SYSCTL_THRESHOLD_I2S2_M,
    SYSCTL_THRESHOLD_I2C0,
    SYSCTL_THRESHOLD_I2C1,
    SYSCTL_THRESHOLD_I2C2,
    SYSCTL_THRESHOLD_WDT0,
    SYSCTL_THRESHOLD_WDT1,
    SYSCTL_THRESHOLD_MAX = 28
} sysctl_threshold_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| SYSCTL\_THRESHOLD\_ACLK | ACLK |
| SYSCTL\_THRESHOLD\_APB0 | APB0 |
| SYSCTL\_THRESHOLD\_APB1 | APB1 |
| SYSCTL\_THRESHOLD\_APB2 | ACLK |
| SYSCTL\_THRESHOLD\_SRAM0 | SRAM0 |
| SYSCTL\_THRESHOLD\_SRAM1 | SRAM1 |
| SYSCTL\_THRESHOLD\_AI | AI |
| SYSCTL\_THRESHOLD\_DVP | DVP |
| SYSCTL\_THRESHOLD\_ROM | ROM |
| SYSCTL\_THRESHOLD\_SPI0 | SPI0 |
| SYSCTL\_THRESHOLD\_SPI1 | SPI1 |
| SYSCTL\_THRESHOLD\_SPI2 | SPI2 |
| SYSCTL\_THRESHOLD\_SPI3 | SPI3 |
| SYSCTL\_THRESHOLD\_TIMER0 | TIMER0 |
| SYSCTL\_THRESHOLD\_TIMER1 | TIMER1 |
| SYSCTL\_THRESHOLD\_TIMER2 | TIMER2 |
| SYSCTL\_THRESHOLD\_I2S0 | I2S0 |
| SYSCTL\_THRESHOLD\_I2S1 | I2S1 |
| SYSCTL\_THRESHOLD\_I2S2 | I2S2 |
| SYSCTL\_THRESHOLD\_I2S0\_M | I2S0 MCLK |
| SYSCTL\_THRESHOLD\_I2S1\_M | I2S1 MCLK |
| SYSCTL\_THRESHOLD\_I2S2\_M | I2S2 MCLK |
| SYSCTL\_THRESHOLD\_I2C0 | I2C0 |
| SYSCTL\_THRESHOLD\_I2C1 | I2C1 |
| SYSCTL\_THRESHOLD\_I2C2 | I2C2 |
| SYSCTL\_THRESHOLD\_WDT0 | WDT0 |
| SYSCTL\_THRESHOLD\_WDT1 | WDT1 |

### sysctl\_clock\_select\_t <a id="sysctlclockselectt"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置时钟源时各模块编号。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _sysctl_clock_select_t
{
    SYSCTL_CLOCK_SELECT_PLL0_BYPASS,
    SYSCTL_CLOCK_SELECT_PLL1_BYPASS,
    SYSCTL_CLOCK_SELECT_PLL2_BYPASS,
    SYSCTL_CLOCK_SELECT_PLL2,
    SYSCTL_CLOCK_SELECT_ACLK,
    SYSCTL_CLOCK_SELECT_SPI3,
    SYSCTL_CLOCK_SELECT_TIMER0,
    SYSCTL_CLOCK_SELECT_TIMER1,
    SYSCTL_CLOCK_SELECT_TIMER2,
    SYSCTL_CLOCK_SELECT_SPI3_SAMPLE,
    SYSCTL_CLOCK_SELECT_MAX = 11
} sysctl_clock_select_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| SYSCTL\_CLOCK\_SELECT\_PLL0\_BYPASS | PLL0\_BYPASS |
| SYSCTL\_CLOCK\_SELECT\_PLL1\_BYPASS | PLL1\_BYPASS |
| SYSCTL\_CLOCK\_SELECT\_PLL2\_BYPASS | PLL2\_BYPASS |
| SYSCTL\_CLOCK\_SELECT\_PLL2 | PLL2 |
| SYSCTL\_CLOCK\_SELECT\_ACLK | ACLK |
| SYSCTL\_CLOCK\_SELECT\_SPI3 | SPI3 |
| SYSCTL\_CLOCK\_SELECT\_TIMER0 | TIMER0 |
| SYSCTL\_CLOCK\_SELECT\_TIMER1 | TIMER1 |
| SYSCTL\_CLOCK\_SELECT\_TIMER2 | TIMER2 |
| SYSCTL\_CLOCK\_SELECT\_SPI3\_SAMPLE | SPI3数据采样时钟沿选择 |

### sysctl\_clock\_t <a id="sysctlclockt"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

各个模块的编号。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _sysctl_clock_t
{
    SYSCTL_CLOCK_PLL0,
    SYSCTL_CLOCK_PLL1,
    SYSCTL_CLOCK_PLL2,
    SYSCTL_CLOCK_CPU,
    SYSCTL_CLOCK_SRAM0,
    SYSCTL_CLOCK_SRAM1,
    SYSCTL_CLOCK_APB0,
    SYSCTL_CLOCK_APB1,
    SYSCTL_CLOCK_APB2,
    SYSCTL_CLOCK_ROM,
    SYSCTL_CLOCK_DMA,
    SYSCTL_CLOCK_AI,
    SYSCTL_CLOCK_DVP,
    SYSCTL_CLOCK_FFT,
    SYSCTL_CLOCK_GPIO,
    SYSCTL_CLOCK_SPI0,
    SYSCTL_CLOCK_SPI1,
    SYSCTL_CLOCK_SPI2,
    SYSCTL_CLOCK_SPI3,
    SYSCTL_CLOCK_I2S0,
    SYSCTL_CLOCK_I2S1,
    SYSCTL_CLOCK_I2S2,
    SYSCTL_CLOCK_I2C0,
    SYSCTL_CLOCK_I2C1,
    SYSCTL_CLOCK_I2C2,
    SYSCTL_CLOCK_UART1,
    SYSCTL_CLOCK_UART2,
    SYSCTL_CLOCK_UART3,
    SYSCTL_CLOCK_AES,
    SYSCTL_CLOCK_FPIOA,
    SYSCTL_CLOCK_TIMER0,
    SYSCTL_CLOCK_TIMER1,
    SYSCTL_CLOCK_TIMER2,
    SYSCTL_CLOCK_WDT0,
    SYSCTL_CLOCK_WDT1,
    SYSCTL_CLOCK_SHA,
    SYSCTL_CLOCK_OTP,
    SYSCTL_CLOCK_RTC,
    SYSCTL_CLOCK_ACLK = 40,
    SYSCTL_CLOCK_HCLK,
    SYSCTL_CLOCK_IN0,
    SYSCTL_CLOCK_MAX
} sysctl_clock_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| SYSCTL\_CLOCK\_PLL0 | PLL0 |
| SYSCTL\_CLOCK\_PLL1 | PLL1 |
| SYSCTL\_CLOCK\_PLL2 | PLL2 |
| SYSCTL\_CLOCK\_CPU | CPU |
| SYSCTL\_CLOCK\_SRAM0 | SRAM0 |
| SYSCTL\_CLOCK\_SRAM1 | SRAM1 |
| SYSCTL\_CLOCK\_APB0 | APB0 |
| SYSCTL\_CLOCK\_APB1 | APB1 |
| SYSCTL\_CLOCK\_APB2 | APB2 |
| SYSCTL\_CLOCK\_ROM | ROM |
| SYSCTL\_CLOCK\_DMA | DMA |
| SYSCTL\_CLOCK\_AI | AI |
| SYSCTL\_CLOCK\_DVP | DVP |
| SYSCTL\_CLOCK\_FFT | FFT |
| SYSCTL\_CLOCK\_GPIO | GPIO |
| SYSCTL\_CLOCK\_SPI0 | SPI0 |
| SYSCTL\_CLOCK\_SPI1 | SPI1 |
| SYSCTL\_CLOCK\_SPI2 | SPI2 |
| SYSCTL\_CLOCK\_SPI3 | SPI3 |
| SYSCTL\_CLOCK\_I2S0 | I2S0 |
| SYSCTL\_CLOCK\_I2S1 | I2S1 |
| SYSCTL\_CLOCK\_I2S2 | I2S2 |
| SYSCTL\_CLOCK\_I2C0 | I2C0 |
| SYSCTL\_CLOCK\_I2C1 | I2C1 |
| SYSCTL\_CLOCK\_I2C2 | I2C2 |
| SYSCTL\_CLOCK\_UART1 | UART1 |
| SYSCTL\_CLOCK\_UART2 | UART2 |
| SYSCTL\_CLOCK\_UART3 | UART3 |
| SYSCTL\_CLOCK\_AES | AES |
| SYSCTL\_CLOCK\_FPIOA | FPIOA |
| SYSCTL\_CLOCK\_TIMER0 | TIMER0 |
| SYSCTL\_CLOCK\_TIMER1 | TIMER1 |
| SYSCTL\_CLOCK\_TIMER2 | TIMER2 |
| SYSCTL\_CLOCK\_WDT0 | WDT0 |
| SYSCTL\_CLOCK\_WDT1 | WDT1 |
| SYSCTL\_CLOCK\_SHA | SHA |
| SYSCTL\_CLOCK\_OTP | OTP |
| SYSCTL\_CLOCK\_RTC | RTC |
| SYSCTL\_CLOCK\_ACLK | ACLK |
| SYSCTL\_CLOCK\_HCLK | HCLK |
| SYSCTL\_CLOCK\_IN0 | 外部输入时钟IN0 |

### sysctl\_reset\_t <a id="sysctlresett"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

复位时各个模块的编号。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _sysctl_reset_t
{
    SYSCTL_RESET_SOC,
    SYSCTL_RESET_ROM,
    SYSCTL_RESET_DMA,
    SYSCTL_RESET_AI,
    SYSCTL_RESET_DVP,
    SYSCTL_RESET_FFT,
    SYSCTL_RESET_GPIO,
    SYSCTL_RESET_SPI0,
    SYSCTL_RESET_SPI1,
    SYSCTL_RESET_SPI2,
    SYSCTL_RESET_SPI3,
    SYSCTL_RESET_I2S0,
    SYSCTL_RESET_I2S1,
    SYSCTL_RESET_I2S2,
    SYSCTL_RESET_I2C0,
    SYSCTL_RESET_I2C1,
    SYSCTL_RESET_I2C2,
    SYSCTL_RESET_UART1,
    SYSCTL_RESET_UART2,
    SYSCTL_RESET_UART3,
    SYSCTL_RESET_AES,
    SYSCTL_RESET_FPIOA,
    SYSCTL_RESET_TIMER0,
    SYSCTL_RESET_TIMER1,
    SYSCTL_RESET_TIMER2,
    SYSCTL_RESET_WDT0,
    SYSCTL_RESET_WDT1,
    SYSCTL_RESET_SHA,
    SYSCTL_RESET_RTC,
    SYSCTL_RESET_MAX = 31
} sysctl_reset_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| SYSCTL\_RESET\_SOC | 芯片复位 |
| SYSCTL\_RESET\_ROM | ROM |
| SYSCTL\_RESET\_DMA | DMA |
| SYSCTL\_RESET\_AI | AI |
| SYSCTL\_RESET\_DVP | DVP |
| SYSCTL\_RESET\_FFT | FFT |
| SYSCTL\_RESET\_GPIO | GPIO |
| SYSCTL\_RESET\_SPI0 | SPI0 |
| SYSCTL\_RESET\_SPI1 | SPI1 |
| SYSCTL\_RESET\_SPI2 | SPI2 |
| SYSCTL\_RESET\_SPI3 | SPI3 |
| SYSCTL\_RESET\_I2S0 | I2S0 |
| SYSCTL\_RESET\_I2S1 | I2S1 |
| SYSCTL\_RESET\_I2S2 | I2S2 |
| SYSCTL\_RESET\_I2C0 | I2C0 |
| SYSCTL\_RESET\_I2C1 | I2C1 |
| SYSCTL\_RESET\_I2C2 | I2C2 |
| SYSCTL\_RESET\_UART1 | UART1 |
| SYSCTL\_RESET\_UART2 | UART2 |
| SYSCTL\_RESET\_UART3 | UART3 |
| SYSCTL\_RESET\_AES | AES |
| SYSCTL\_RESET\_FPIOA | FPIOA |
| SYSCTL\_RESET\_TIMER0 | TIMER0 |
| SYSCTL\_RESET\_TIMER1 | TIMER1 |
| SYSCTL\_RESET\_TIMER2 | TIMER2 |
| SYSCTL\_RESET\_WDT0 | WDT0 |
| SYSCTL\_RESET\_WDT1 | WDT1 |
| SYSCTL\_RESET\_SHA | SHA |
| SYSCTL\_RESET\_RTC | RTC |

### sysctl\_dma\_channel\_t <a id="sysctldmachannelt"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

DMA通道号。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _sysctl_dma_channel_t
{
    SYSCTL_DMA_CHANNEL_0,
    SYSCTL_DMA_CHANNEL_1,
    SYSCTL_DMA_CHANNEL_2,
    SYSCTL_DMA_CHANNEL_3,
    SYSCTL_DMA_CHANNEL_4,
    SYSCTL_DMA_CHANNEL_5,
    SYSCTL_DMA_CHANNEL_MAX
} sysctl_dma_channel_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| SYSCTL\_DMA\_CHANNEL\_0 | DMA通道0 |
| SYSCTL\_DMA\_CHANNEL\_1 | DMA通道1 |
| SYSCTL\_DMA\_CHANNEL\_2 | DMA通道2 |
| SYSCTL\_DMA\_CHANNEL\_3 | DMA通道3 |
| SYSCTL\_DMA\_CHANNEL\_4 | DMA通道4 |
| SYSCTL\_DMA\_CHANNEL\_5 | DMA通道5 |

### sysctl\_dma\_select\_t <a id="sysctldmaselectt"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

DMA请求源编号。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _sysctl_dma_select_t
{
    SYSCTL_DMA_SELECT_SSI0_RX_REQ,
    SYSCTL_DMA_SELECT_SSI0_TX_REQ,
    SYSCTL_DMA_SELECT_SSI1_RX_REQ,
    SYSCTL_DMA_SELECT_SSI1_TX_REQ,
    SYSCTL_DMA_SELECT_SSI2_RX_REQ,
    SYSCTL_DMA_SELECT_SSI2_TX_REQ,
    SYSCTL_DMA_SELECT_SSI3_RX_REQ,
    SYSCTL_DMA_SELECT_SSI3_TX_REQ,
    SYSCTL_DMA_SELECT_I2C0_RX_REQ,
    SYSCTL_DMA_SELECT_I2C0_TX_REQ,
    SYSCTL_DMA_SELECT_I2C1_RX_REQ,
    SYSCTL_DMA_SELECT_I2C1_TX_REQ,
    SYSCTL_DMA_SELECT_I2C2_RX_REQ,
    SYSCTL_DMA_SELECT_I2C2_TX_REQ,
    SYSCTL_DMA_SELECT_UART1_RX_REQ,
    SYSCTL_DMA_SELECT_UART1_TX_REQ,
    SYSCTL_DMA_SELECT_UART2_RX_REQ,
    SYSCTL_DMA_SELECT_UART2_TX_REQ,
    SYSCTL_DMA_SELECT_UART3_RX_REQ,
    SYSCTL_DMA_SELECT_UART3_TX_REQ,
    SYSCTL_DMA_SELECT_AES_REQ,
    SYSCTL_DMA_SELECT_SHA_RX_REQ,
    SYSCTL_DMA_SELECT_AI_RX_REQ,
    SYSCTL_DMA_SELECT_FFT_RX_REQ,
    SYSCTL_DMA_SELECT_FFT_TX_REQ,
    SYSCTL_DMA_SELECT_I2S0_TX_REQ,
    SYSCTL_DMA_SELECT_I2S0_RX_REQ,
    SYSCTL_DMA_SELECT_I2S1_TX_REQ,
    SYSCTL_DMA_SELECT_I2S1_RX_REQ,
    SYSCTL_DMA_SELECT_I2S2_TX_REQ,
    SYSCTL_DMA_SELECT_I2S2_RX_REQ,
    SYSCTL_DMA_SELECT_MAX
} sysctl_dma_select_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| SYSCTL\_DMA\_SELECT\_SSI0\_RX\_REQ | SPI0接收 |
| SYSCTL\_DMA\_SELECT\_SSI0\_TX\_REQ | SPI0发送 |
| SYSCTL\_DMA\_SELECT\_SSI1\_RX\_REQ | SPI1接收 |
| SYSCTL\_DMA\_SELECT\_SSI1\_TX\_REQ | SPI1发送 |
| SYSCTL\_DMA\_SELECT\_SSI2\_RX\_REQ | SPI2接收 |
| SYSCTL\_DMA\_SELECT\_SSI2\_TX\_REQ | SPI2发送 |
| SYSCTL\_DMA\_SELECT\_SSI3\_RX\_REQ | SPI3接收 |
| SYSCTL\_DMA\_SELECT\_SSI3\_TX\_REQ | SPI3发送 |
| SYSCTL\_DMA\_SELECT\_I2C0\_RX\_REQ | I2C0接收 |
| SYSCTL\_DMA\_SELECT\_I2C0\_TX\_REQ | I2C0发送 |
| SYSCTL\_DMA\_SELECT\_I2C1\_RX\_REQ | I2C1接收 |
| SYSCTL\_DMA\_SELECT\_I2C1\_TX\_REQ | I2C1发送 |
| SYSCTL\_DMA\_SELECT\_I2C2\_RX\_REQ | I2C2接收 |
| SYSCTL\_DMA\_SELECT\_I2C2\_TX\_REQ | I2C2发送 |
| SYSCTL\_DMA\_SELECT\_UART1\_RX\_REQ | UART1接收 |
| SYSCTL\_DMA\_SELECT\_UART1\_TX\_REQ | UART1发送 |
| SYSCTL\_DMA\_SELECT\_UART2\_RX\_REQ | UART2接收 |
| SYSCTL\_DMA\_SELECT\_UART2\_TX\_REQ | UART2发送 |
| SYSCTL\_DMA\_SELECT\_UART3\_RX\_REQ | UART3接收 |
| SYSCTL\_DMA\_SELECT\_UART3\_TX\_REQ | UART3发送 |
| SYSCTL\_DMA\_SELECT\_AES\_REQ | AES |
| SYSCTL\_DMA\_SELECT\_SHA\_RX\_REQ | SHA接收 |
| SYSCTL\_DMA\_SELECT\_AI\_RX\_REQ | AI接收 |
| SYSCTL\_DMA\_SELECT\_FFT\_RX\_REQ | FFT接收 |
| SYSCTL\_DMA\_SELECT\_FFT\_TX\_REQ | FFT发送 |
| SYSCTL\_DMA\_SELECT\_I2S0\_TX\_REQ | I2S0发送 |
| SYSCTL\_DMA\_SELECT\_I2S0\_RX\_REQ | I2S0接收 |
| SYSCTL\_DMA\_SELECT\_I2S1\_TX\_REQ | I2S1发送 |
| SYSCTL\_DMA\_SELECT\_I2S1\_RX\_REQ | I2S1接收 |
| SYSCTL\_DMA\_SELECT\_I2S2\_TX\_REQ | I2S2发送 |
| SYSCTL\_DMA\_SELECT\_I2S2\_RX\_REQ | I2S2接收 |

### sysctl\_power\_bank\_t <a id="sysctlpowerbankt"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

电源域编号。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _sysctl_power_bank
{
    SYSCTL_POWER_BANK0,
    SYSCTL_POWER_BANK1,
    SYSCTL_POWER_BANK2,
    SYSCTL_POWER_BANK3,
    SYSCTL_POWER_BANK4,
    SYSCTL_POWER_BANK5,
    SYSCTL_POWER_BANK6,
    SYSCTL_POWER_BANK7,
    SYSCTL_POWER_BANK_MAX,
} sysctl_power_bank_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| SYSCTL\_POWER\_BANK0 | 电源域0，控制IO0-IO5 |
| SYSCTL\_POWER\_BANK1 | 电源域1，控制IO6-IO11 |
| SYSCTL\_POWER\_BANK2 | 电源域2，控制IO12-IO17 |
| SYSCTL\_POWER\_BANK3 | 电源域3，控制IO18-IO23 |
| SYSCTL\_POWER\_BANK4 | 电源域4，控制IO24-IO29 |
| SYSCTL\_POWER\_BANK5 | 电源域5，控制IO30-IO35 |
| SYSCTL\_POWER\_BANK6 | 电源域6，控制IO36-IO41 |
| SYSCTL\_POWER\_BANK7 | 电源域7，控制IO42-IO47 |

### sysctl\_io\_power\_mode\_t <a id="sysctliopowermodet"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

IO输出电压值。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _sysctl_io_power_mode
{
    SYSCTL_POWER_V33,
    SYSCTL_POWER_V18
} sysctl_io_power_mode_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| SYSCTL\_POWER\_V33 | 设置为3.3V |
| SYSCTL\_POWER\_V18 | 设置为1.8V |

### sysctl\_reset\_enum\_status\_t <a id="sysctlresetenumstatust"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

复位状态。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _sysctl_reset_enum_status
{
    SYSCTL_RESET_STATUS_HARD,
    SYSCTL_RESET_STATUS_SOFT,
    SYSCTL_RESET_STATUS_WDT0,
    SYSCTL_RESET_STATUS_WDT1,
    SYSCTL_RESET_STATUS_MAX,
} sysctl_reset_enum_status_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| SYSCTL\_RESET\_STATUS\_HARD | 硬件复位，重新上电或触发reset管脚 |
| SYSCTL\_RESET\_STATUS\_SOFT | 软件复位 |
| SYSCTL\_RESET\_STATUS\_WDT0 | 看门狗0复位 |
| SYSCTL\_RESET\_STATUS\_WDT1 | 看门狗1复位 |

