# 现场可编程IO阵列\(FPIOA\)

## 概述 <a id="&#x6982;&#x8FF0;"></a>

FPIOA（现场可编程IO阵列）允许用户将255个内部功能映射到芯片外围的48个自由IO上。

## 功能描述 <a id="&#x529F;&#x80FD;&#x63CF;&#x8FF0;"></a>

* 支持IO的可编程功能选择
* 支持IO输出的8种驱动能力选择
* 支持IO的内部上拉电阻选择
* 支持IO的内部下拉电阻选择
* 支持IO输入的内部施密特触发器设置
* 支持IO输出的斜率控制
* 支持内部输入逻辑的电平设置

## API 参考 <a id="api-&#x53C2;&#x8003;"></a>

对应的头文件 `fpioa.h`

为用户提供以下接口

* fpioa\_set\_function
* fpioa\_get\_io\_by\_function
* fpioa\_set\_io
* fpioa\_get\_io
* fpioa\_set\_tie\_enable
* fpioa\_set\_tie\_value
* fpioa\_set\_io\_pull
* fpioa\_get\_io\_pull
* fpioa\_set\_io\_driving
* fpioa\_get\_io\_driving

### fpioa\_set\_function <a id="fpioasetfunction"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置IO0-IO47管脚复用功能。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int fpioa_set_function(int number, fpioa_function_t function)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| number | IO管脚号 | 输入 |
| function | FPIOA功能号 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### fpioa\_get\_io\_by\_function <a id="fpioagetiobyfunction"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

根据功能号获取IO管脚号。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int fpioa_get_io_by_function(fpioa_function_t function)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| function | FPIOA功能号 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 大于等于0 | IO管脚号 |
| 小于0 | 失败 |

### fpioa\_get\_io <a id="fpioagetio"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

获得IO管脚的配置。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int fpioa_get_io(int number, fpioa_io_config_t *cfg)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| number | IO管脚号 | 输入 |
| cfg | 管脚功能结构体 | 输出 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### fpioa\_set\_io <a id="fpioasetio"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置IO管脚的配置。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int fpioa_set_io(int number, fpioa_io_config_t *cfg)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| number | IO管脚号 | 输入 |
| cfg | 管脚功能结构体 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### fpioa\_set\_tie\_enable <a id="fpioasettieenable"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

使能或禁用FPIOA功能输入信号的强制输入电平功能。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int fpioa_set_tie_enable(fpioa_function_t function, int enable)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| function | FPIOA功能号 | 输入 |
| enable | 强制输入电平使能位 0：禁用 1：使能 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### fpioa\_set\_tie\_value <a id="fpioasettievalue"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置FPIOA功能输入信号的强制输入电平高或者低，仅在强制输入电平功能启用时生效。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int fpioa_set_tie_value(fpioa_function_t function, int value)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| function | FPIOA功能号 | 输入 |
| value | 强制输入电平值 0：低 1：高 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### fpioa\_set\_pull <a id="fpioasetpull"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置IO的上拉下拉。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int fpioa_set_io_pull(int number, fpioa_pull_t pull)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| number | IO编号 | 输入 |
| pull | 上下拉值 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### fpioa\_get\_pull <a id="fpioagetpull"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

获取IO管脚上下拉值。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int fpioa_get_io_pull(int number)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| number | IO编号 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 无上下拉 |
| 1 | 下拉 |
| 2 | 上拉 |

### fpioa\_set\_io\_driving <a id="fpioasetiodriving"></a>

### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置IO管脚的驱动能力。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int fpioa_set_io_driving(int number, fpioa_driving_t driving)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| number | IO编号 | 输入 |
| driving | 驱动能力 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### fpioa\_get\_io\_driving <a id="fpioagetiodriving"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

获取驱动能力。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int fpioa_get_io_driving(int number)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| number | IO编号 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 大于等于0 | 驱动能力 |
| 小于0 | 失败 |

## 数据类型 <a id="&#x6570;&#x636E;&#x7C7B;&#x578B;"></a>

相关数据类型、数据结构定义如下：

* fpioa\_function\_t：管脚的功能编号。
* fpioa\_io\_config\_t：FPIOA的配置。
* fpioa\_pull\_t：FPIOA上拉或者下拉特性。
* fpioa\_driving\_t：FPIOA驱动能力编号。

### fpioa\_io\_config\_t <a id="fpioaioconfigt"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

FPIOA的配置。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef struct _fpioa_io_config
{
    uint32_t ch_sel : 8;
    uint32_t ds : 4;
    uint32_t oe_en : 1;
    uint32_t oe_inv : 1;
    uint32_t do_sel : 1;
    uint32_t do_inv : 1;
    uint32_t pu : 1;
    uint32_t pd : 1;
    uint32_t resv0 : 1;
    uint32_t sl : 1;
    uint32_t ie_en : 1;
    uint32_t ie_inv : 1;
    uint32_t di_inv : 1;
    uint32_t st : 1;
    uint32_t resv1 : 7;
    uint32_t pad_di : 1;
} __attribute__((packed, aligned(4))) fpioa_io_config_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| ch\_sel | FPIOA功能编号，从256种功能里选择一种。 |
| ds | 驱动电流强度选择，参照驱动电流强度表。 |
| oe\_en | 输出使能\(OE\)（手动模式）。1:使能 0:禁用 |
| oe\_inv | 输出使能取反。 1:使能 0:禁用 |
| do\_sel | 输出信号选择。1:输出OE信号 0:输出原始信号 |
| do\_inv | 输出信号取反。1:使能 0:禁用 |
| pu | 上拉使能。1:使能 0:禁用 |
| pd | 下拉使能。1:使能 0:禁用 |
| resv0 | 保留位 |
| sl | 输出摆率控制。1:低摆率，稳定 0: 高摆率，快 |
| ie\_en | 输入使能\(IE\)（手动模式）。 1:使能 0:禁用 |
| ie\_inv | 输入使能取反。1:使能 0:禁用 |
| di\_inv | 输入信号取反。1:使能 0:禁用 |
| st | 输入施密特触发器。1:使能 0:禁用 |
| resv1 | 保留位。 |
| pad\_di | 当前引脚的输入电平。 |

### 驱动能力选择表 <a id="&#x9A71;&#x52A8;&#x80FD;&#x529B;&#x9009;&#x62E9;&#x8868;"></a>

#### 低电平输入电流 <a id="&#x4F4E;&#x7535;&#x5E73;&#x8F93;&#x5165;&#x7535;&#x6D41;"></a>

| ds | Min\(mA\) | Typ\(mA\) | Max\(mA\) |
| :--- | :--- | :--- | :--- |
| 0 | 3.2 | 5.4 | 8.3 |
| 1 | 4.7 | 8.0 | 12.3 |
| 2 | 6.3 | 10.7 | 16.4 |
| 3 | 7.8 | 13.2 | 20.2 |
| 4 | 9.4 | 15.9 | 24.2 |
| 5 | 10.9 | 18.4 | 28.1 |
| 6 | 12.4 | 20.9 | 31.8 |
| 7 | 13.9 | 23.4 | 35.5 |

#### 高电平输出电流 <a id="&#x9AD8;&#x7535;&#x5E73;&#x8F93;&#x51FA;&#x7535;&#x6D41;"></a>

| ds | Min\(mA\) | Typ\(mA\) | Max\(mA\) |
| :--- | :--- | :--- | :--- |
| 0 | 5.0 | 7.6 | 11.2 |
| 1 | 7.5 | 11.4 | 16.8 |
| 2 | 10.0 | 15.2 | 22.3 |
| 3 | 12.4 | 18.9 | 27.8 |
| 4 | 14.9 | 22.6 | 33.3 |
| 5 | 17.4 | 26.3 | 38.7 |
| 6 | 19.8 | 30.0 | 44.1 |
| 7 | 22.3 | 33.7 | 49.5 |

### fpioa\_pull\_t <a id="fpioapullt"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

FPIOA上拉或者下拉特性。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _fpioa_pull
{
    FPIOA_PULL_NONE,
    FPIOA_PULL_DOWN,
    FPIOA_PULL_UP,
    FPIOA_PULL_MAX
} fpioa_pull_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| FPIOA\_PULL\_NONE | 无上下拉 |
| FPIOA\_PULL\_DOWN | 下拉 |
| FPIOA\_PULL\_UP | 上拉 |

> 禁止同时启用芯片内部的上拉与下拉

### fpioa\_driving\_t <a id="fpioadrivingt"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

FPIOA驱动能力编号，参见驱动能力选择表。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _fpioa_driving
{
    FPIOA_DRIVING_0,
    FPIOA_DRIVING_1,
    FPIOA_DRIVING_2,
    FPIOA_DRIVING_3,
    FPIOA_DRIVING_4,
    FPIOA_DRIVING_5,
    FPIOA_DRIVING_6,
    FPIOA_DRIVING_7,
} fpioa_driving_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| FPIOA\_DRIVING\_0 | 驱动能力0 |
| FPIOA\_DRIVING\_1 | 驱动能力1 |
| FPIOA\_DRIVING\_2 | 驱动能力2 |
| FPIOA\_DRIVING\_3 | 驱动能力3 |
| FPIOA\_DRIVING\_4 | 驱动能力4 |
| FPIOA\_DRIVING\_5 | 驱动能力5 |
| FPIOA\_DRIVING\_6 | 驱动能力6 |
| FPIOA\_DRIVING\_7 | 驱动能力7 |

### fpioa\_function\_t <a id="fpioafunctiont"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

管脚的功能编号。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _fpioa_function
{
    FUNC_JTAG_TCLK        = 0,      
    FUNC_JTAG_TDI         = 1,      
    FUNC_JTAG_TMS         = 2,      
    FUNC_JTAG_TDO         = 3,      
    FUNC_SPI0_D0          = 4,      
    FUNC_SPI0_D1          = 5,      
    FUNC_SPI0_D2          = 6,      
    FUNC_SPI0_D3          = 7,      
    FUNC_SPI0_D4          = 8,      
    FUNC_SPI0_D5          = 9,      
    FUNC_SPI0_D6          = 10,     
    FUNC_SPI0_D7          = 11,     
    FUNC_SPI0_SS0         = 12,     
    FUNC_SPI0_SS1         = 13,     
    FUNC_SPI0_SS2         = 14,     
    FUNC_SPI0_SS3         = 15,     
    FUNC_SPI0_ARB         = 16,     
    FUNC_SPI0_SCLK        = 17,     
    FUNC_UARTHS_RX        = 18,     
    FUNC_UARTHS_TX        = 19,     
    FUNC_CLK_IN1          = 20,     
    FUNC_CLK_IN2          = 21,     
    FUNC_CLK_SPI1         = 22,     
    FUNC_CLK_I2C1         = 23,     
    FUNC_GPIOHS0          = 24,     
    FUNC_GPIOHS1          = 25,     
    FUNC_GPIOHS2          = 26,     
    FUNC_GPIOHS3          = 27,     
    FUNC_GPIOHS4          = 28,     
    FUNC_GPIOHS5          = 29,     
    FUNC_GPIOHS6          = 30,     
    FUNC_GPIOHS7          = 31,     
    FUNC_GPIOHS8          = 32,     
    FUNC_GPIOHS9          = 33,     
    FUNC_GPIOHS10         = 34,     
    FUNC_GPIOHS11         = 35,     
    FUNC_GPIOHS12         = 36,     
    FUNC_GPIOHS13         = 37,     
    FUNC_GPIOHS14         = 38,     
    FUNC_GPIOHS15         = 39,     
    FUNC_GPIOHS16         = 40,     
    FUNC_GPIOHS17         = 41,     
    FUNC_GPIOHS18         = 42,     
    FUNC_GPIOHS19         = 43,     
    FUNC_GPIOHS20         = 44,     
    FUNC_GPIOHS21         = 45,     
    FUNC_GPIOHS22         = 46,     
    FUNC_GPIOHS23         = 47,     
    FUNC_GPIOHS24         = 48,     
    FUNC_GPIOHS25         = 49,     
    FUNC_GPIOHS26         = 50,     
    FUNC_GPIOHS27         = 51,     
    FUNC_GPIOHS28         = 52,     
    FUNC_GPIOHS29         = 53,     
    FUNC_GPIOHS30         = 54,     
    FUNC_GPIOHS31         = 55,     
    FUNC_GPIO0            = 56,     
    FUNC_GPIO1            = 57,     
    FUNC_GPIO2            = 58,     
    FUNC_GPIO3            = 59,     
    FUNC_GPIO4            = 60,     
    FUNC_GPIO5            = 61,     
    FUNC_GPIO6            = 62,     
    FUNC_GPIO7            = 63,     
    FUNC_UART1_RX         = 64,     
    FUNC_UART1_TX         = 65,     
    FUNC_UART2_RX         = 66,     
    FUNC_UART2_TX         = 67,     
    FUNC_UART3_RX         = 68,     
    FUNC_UART3_TX         = 69,     
    FUNC_SPI1_D0          = 70,     
    FUNC_SPI1_D1          = 71,     
    FUNC_SPI1_D2          = 72,     
    FUNC_SPI1_D3          = 73,     
    FUNC_SPI1_D4          = 74,     
    FUNC_SPI1_D5          = 75,     
    FUNC_SPI1_D6          = 76,     
    FUNC_SPI1_D7          = 77,     
    FUNC_SPI1_SS0         = 78,     
    FUNC_SPI1_SS1         = 79,     
    FUNC_SPI1_SS2         = 80,     
    FUNC_SPI1_SS3         = 81,     
    FUNC_SPI1_ARB         = 82,     
    FUNC_SPI1_SCLK        = 83,     
    FUNC_SPI_SLAVE_D0     = 84,     
    FUNC_SPI_SLAVE_SS     = 85,     
    FUNC_SPI_SLAVE_SCLK   = 86,     
    FUNC_I2S0_MCLK        = 87,     
    FUNC_I2S0_SCLK        = 88,     
    FUNC_I2S0_WS          = 89,     
    FUNC_I2S0_IN_D0       = 90,     
    FUNC_I2S0_IN_D1       = 91,     
    FUNC_I2S0_IN_D2       = 92,     
    FUNC_I2S0_IN_D3       = 93,     
    FUNC_I2S0_OUT_D0      = 94,     
    FUNC_I2S0_OUT_D1      = 95,     
    FUNC_I2S0_OUT_D2      = 96,     
    FUNC_I2S0_OUT_D3      = 97,     
    FUNC_I2S1_MCLK        = 98,     
    FUNC_I2S1_SCLK        = 99,     
    FUNC_I2S1_WS          = 100,    
    FUNC_I2S1_IN_D0       = 101,    
    FUNC_I2S1_IN_D1       = 102,    
    FUNC_I2S1_IN_D2       = 103,    
    FUNC_I2S1_IN_D3       = 104,    
    FUNC_I2S1_OUT_D0      = 105,    
    FUNC_I2S1_OUT_D1      = 106,    
    FUNC_I2S1_OUT_D2      = 107,    
    FUNC_I2S1_OUT_D3      = 108,    
    FUNC_I2S2_MCLK        = 109,    
    FUNC_I2S2_SCLK        = 110,    
    FUNC_I2S2_WS          = 111,    
    FUNC_I2S2_IN_D0       = 112,    
    FUNC_I2S2_IN_D1       = 113,    
    FUNC_I2S2_IN_D2       = 114,    
    FUNC_I2S2_IN_D3       = 115,    
    FUNC_I2S2_OUT_D0      = 116,    
    FUNC_I2S2_OUT_D1      = 117,    
    FUNC_I2S2_OUT_D2      = 118,    
    FUNC_I2S2_OUT_D3      = 119,    
    FUNC_RESV0            = 120,    
    FUNC_RESV1            = 121,    
    FUNC_RESV2            = 122,    
    FUNC_RESV3            = 123,    
    FUNC_RESV4            = 124,    
    FUNC_RESV5            = 125,    
    FUNC_I2C0_SCLK        = 126,    
    FUNC_I2C0_SDA         = 127,    
    FUNC_I2C1_SCLK        = 128,    
    FUNC_I2C1_SDA         = 129,    
    FUNC_I2C2_SCLK        = 130,    
    FUNC_I2C2_SDA         = 131,    
    FUNC_CMOS_XCLK        = 132,    
    FUNC_CMOS_RST         = 133,    
    FUNC_CMOS_PWND        = 134,    
    FUNC_CMOS_VSYNC       = 135,    
    FUNC_CMOS_HREF        = 136,    
    FUNC_CMOS_PCLK        = 137,    
    FUNC_CMOS_D0          = 138,    
    FUNC_CMOS_D1          = 139,    
    FUNC_CMOS_D2          = 140,    
    FUNC_CMOS_D3          = 141,    
    FUNC_CMOS_D4          = 142,    
    FUNC_CMOS_D5          = 143,    
    FUNC_CMOS_D6          = 144,    
    FUNC_CMOS_D7          = 145,    
    FUNC_SCCB_SCLK        = 146,    
    FUNC_SCCB_SDA         = 147,    
    FUNC_UART1_CTS        = 148,    
    FUNC_UART1_DSR        = 149,    
    FUNC_UART1_DCD        = 150,    
    FUNC_UART1_RI         = 151,    
    FUNC_UART1_SIR_IN     = 152,    
    FUNC_UART1_DTR        = 153,    
    FUNC_UART1_RTS        = 154,    
    FUNC_UART1_OUT2       = 155,    
    FUNC_UART1_OUT1       = 156,    
    FUNC_UART1_SIR_OUT    = 157,    
    FUNC_UART1_BAUD       = 158,    
    FUNC_UART1_RE         = 159,    
    FUNC_UART1_DE         = 160,    
    FUNC_UART1_RS485_EN   = 161,    
    FUNC_UART2_CTS        = 162,    
    FUNC_UART2_DSR        = 163,    
    FUNC_UART2_DCD        = 164,    
    FUNC_UART2_RI         = 165,    
    FUNC_UART2_SIR_IN     = 166,    
    FUNC_UART2_DTR        = 167,    
    FUNC_UART2_RTS        = 168,    
    FUNC_UART2_OUT2       = 169,    
    FUNC_UART2_OUT1       = 170,    
    FUNC_UART2_SIR_OUT    = 171,    
    FUNC_UART2_BAUD       = 172,    
    FUNC_UART2_RE         = 173,    
    FUNC_UART2_DE         = 174,    
    FUNC_UART2_RS485_EN   = 175,    
    FUNC_UART3_CTS        = 176,    
    FUNC_UART3_DSR        = 177,    
    FUNC_UART3_DCD        = 178,    
    FUNC_UART3_RI         = 179,    
    FUNC_UART3_SIR_IN     = 180,    
    FUNC_UART3_DTR        = 181,    
    FUNC_UART3_RTS        = 182,    
    FUNC_UART3_OUT2       = 183,    
    FUNC_UART3_OUT1       = 184,    
    FUNC_UART3_SIR_OUT    = 185,    
    FUNC_UART3_BAUD       = 186,    
    FUNC_UART3_RE         = 187,    
    FUNC_UART3_DE         = 188,    
    FUNC_UART3_RS485_EN   = 189,    
    FUNC_TIMER0_TOGGLE1   = 190,    
    FUNC_TIMER0_TOGGLE2   = 191,    
    FUNC_TIMER0_TOGGLE3   = 192,    
    FUNC_TIMER0_TOGGLE4   = 193,    
    FUNC_TIMER1_TOGGLE1   = 194,    
    FUNC_TIMER1_TOGGLE2   = 195,    
    FUNC_TIMER1_TOGGLE3   = 196,    
    FUNC_TIMER1_TOGGLE4   = 197,    
    FUNC_TIMER2_TOGGLE1   = 198,    
    FUNC_TIMER2_TOGGLE2   = 199,    
    FUNC_TIMER2_TOGGLE3   = 200,    
    FUNC_TIMER2_TOGGLE4   = 201,    
    FUNC_CLK_SPI2         = 202,    
    FUNC_CLK_I2C2         = 203,    
    FUNC_INTERNAL0        = 204,    
    FUNC_INTERNAL1        = 205,    
    FUNC_INTERNAL2        = 206,    
    FUNC_INTERNAL3        = 207,    
    FUNC_INTERNAL4        = 208,    
    FUNC_INTERNAL5        = 209,    
    FUNC_INTERNAL6        = 210,    
    FUNC_INTERNAL7        = 211,    
    FUNC_INTERNAL8        = 212,    
    FUNC_INTERNAL9        = 213,    
    FUNC_INTERNAL10       = 214,    
    FUNC_INTERNAL11       = 215,    
    FUNC_INTERNAL12       = 216,    
    FUNC_INTERNAL13       = 217,    
    FUNC_INTERNAL14       = 218,    
    FUNC_INTERNAL15       = 219,    
    FUNC_INTERNAL16       = 220,    
    FUNC_INTERNAL17       = 221,    
    FUNC_CONSTANT         = 222,    
    FUNC_INTERNAL18       = 223,    
    FUNC_DEBUG0           = 224,    
    FUNC_DEBUG1           = 225,    
    FUNC_DEBUG2           = 226,    
    FUNC_DEBUG3           = 227,    
    FUNC_DEBUG4           = 228,    
    FUNC_DEBUG5           = 229,    
    FUNC_DEBUG6           = 230,    
    FUNC_DEBUG7           = 231,    
    FUNC_DEBUG8           = 232,    
    FUNC_DEBUG9           = 233,    
    FUNC_DEBUG10          = 234,    
    FUNC_DEBUG11          = 235,    
    FUNC_DEBUG12          = 236,    
    FUNC_DEBUG13          = 237,    
    FUNC_DEBUG14          = 238,    
    FUNC_DEBUG15          = 239,    
    FUNC_DEBUG16          = 240,    
    FUNC_DEBUG17          = 241,    
    FUNC_DEBUG18          = 242,    
    FUNC_DEBUG19          = 243,    
    FUNC_DEBUG20          = 244,    
    FUNC_DEBUG21          = 245,    
    FUNC_DEBUG22          = 246,    
    FUNC_DEBUG23          = 247,    
    FUNC_DEBUG24          = 248,    
    FUNC_DEBUG25          = 249,    
    FUNC_DEBUG26          = 250,    
    FUNC_DEBUG27          = 251,    
    FUNC_DEBUG28          = 252,    
    FUNC_DEBUG29          = 253,    
    FUNC_DEBUG30          = 254,    
    FUNC_DEBUG31          = 255,    
    FUNC_MAX              = 256,    
} fpioa_function_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| FUNC\_JTAG\_TCLK | JTAG时钟接口 |
| FUNC\_JTAG\_TDI | JTAG数据输入接口 |
| FUNC\_JTAG\_TMS | JTAG控制TAP状态机的转换 |
| FUNC\_JTAG\_TDO | JTAG数据输出接口 |
| FUNC\_SPI0\_D0 | SPI0数据线0 |
| FUNC\_SPI0\_D1 | SPI0数据线1 |
| FUNC\_SPI0\_D2 | SPI0数据线2 |
| FUNC\_SPI0\_D3 | SPI0数据线3 |
| FUNC\_SPI0\_D4 | SPI0数据线4 |
| FUNC\_SPI0\_D5 | SPI0数据线5 |
| FUNC\_SPI0\_D6 | SPI0数据线6 |
| FUNC\_SPI0\_D7 | SPI0数据线7 |
| FUNC\_SPI0\_SS0 | SPI0片选信号0 |
| FUNC\_SPI0\_SS1 | SPI0片选信号1 |
| FUNC\_SPI0\_SS2 | SPI0片选信号2 |
| FUNC\_SPI0\_SS3 | SPI0片选信号3 |
| FUNC\_SPI0\_ARB | SPI0仲裁信号 |
| FUNC\_SPI0\_SCLK | SPI0时钟 |
| FUNC\_UARTHS\_RX | UART高速接收数据接口 |
| FUNC\_UARTHS\_TX | UART高速发送数据接口 |
| FUNC\_RESV6 | 保留功能 |
| FUNC\_RESV7 | 保留功能 |
| FUNC\_CLK\_SPI1 | SPI1时钟 |
| FUNC\_CLK\_I2C1 | I2C1时钟 |
| FUNC\_GPIOHS0 | 高速GPIO0 |
| FUNC\_GPIOHS1 | 高速GPIO1 |
| FUNC\_GPIOHS2 | 高速GPIO2 |
| FUNC\_GPIOHS3 | 高速GPIO3 |
| FUNC\_GPIOHS4 | 高速GPIO4 |
| FUNC\_GPIOHS5 | 高速GPIO5 |
| FUNC\_GPIOHS6 | 高速GPIO6 |
| FUNC\_GPIOHS7 | 高速GPIO7 |
| FUNC\_GPIOHS8 | 高速GPIO8 |
| FUNC\_GPIOHS9 | 高速GPIO9 |
| FUNC\_GPIOHS10 | 高速GPIO10 |
| FUNC\_GPIOHS11 | 高速GPIO11 |
| FUNC\_GPIOHS12 | 高速GPIO12 |
| FUNC\_GPIOHS13 | 高速GPIO13 |
| FUNC\_GPIOHS14 | 高速GPIO14 |
| FUNC\_GPIOHS15 | 高速GPIO15 |
| FUNC\_GPIOHS16 | 高速GPIO16 |
| FUNC\_GPIOHS17 | 高速GPIO17 |
| FUNC\_GPIOHS18 | 高速GPIO18 |
| FUNC\_GPIOHS19 | 高速GPIO19 |
| FUNC\_GPIOHS20 | 高速GPIO20 |
| FUNC\_GPIOHS21 | 高速GPIO21 |
| FUNC\_GPIOHS22 | 高速GPIO22 |
| FUNC\_GPIOHS23 | 高速GPIO23 |
| FUNC\_GPIOHS24 | 高速GPIO24 |
| FUNC\_GPIOHS25 | 高速GPIO25 |
| FUNC\_GPIOHS26 | 高速GPIO26 |
| FUNC\_GPIOHS27 | 高速GPIO27 |
| FUNC\_GPIOHS28 | 高速GPIO28 |
| FUNC\_GPIOHS29 | 高速GPIO29 |
| FUNC\_GPIOHS30 | 高速GPIO30 |
| FUNC\_GPIOHS31 | 高速GPIO31 |
| FUNC\_GPIO0 | GPIO0 |
| FUNC\_GPIO1 | GPIO1 |
| FUNC\_GPIO2 | GPIO2 |
| FUNC\_GPIO3 | GPIO3 |
| FUNC\_GPIO4 | GPIO4 |
| FUNC\_GPIO5 | GPIO5 |
| FUNC\_GPIO6 | GPIO6 |
| FUNC\_GPIO7 | GPIO7 |
| FUNC\_UART1\_RX | UART1接收数据接口 |
| FUNC\_UART1\_TX | UART1发送数据接口 |
| FUNC\_UART2\_RX | UART2接收数据接口 |
| FUNC\_UART2\_TX | UART2发送数据接口 |
| FUNC\_UART3\_RX | UART3接收数据接口 |
| FUNC\_UART3\_TX | UART3发送数据接口 |
| FUNC\_SPI1\_D0 | SPI1数据线0 |
| FUNC\_SPI1\_D1 | SPI1数据线1 |
| FUNC\_SPI1\_D2 | SPI1数据线2 |
| FUNC\_SPI1\_D3 | SPI1数据线3 |
| FUNC\_SPI1\_D4 | SPI1数据线4 |
| FUNC\_SPI1\_D5 | SPI1数据线5 |
| FUNC\_SPI1\_D6 | SPI1数据线6 |
| FUNC\_SPI1\_D7 | SPI1数据线7 |
| FUNC\_SPI1\_SS0 | SPI1片选信号0 |
| FUNC\_SPI1\_SS1 | SPI1片选信号1 |
| FUNC\_SPI1\_SS2 | SPI1片选信号2 |
| FUNC\_SPI1\_SS3 | SPI1片选信号3 |
| FUNC\_SPI1\_ARB | SPI1仲裁信号 |
| FUNC\_SPI1\_SCLK | SPI1时钟 |
| FUNC\_SPI\_SLAVE\_D0 | SPI从模式数据线0 |
| FUNC\_SPI\_SLAVE\_SS | SPI从模式片选信号 |
| FUNC\_SPI\_SLAVE\_SCLK | SPI从模式时钟 |
| FUNC\_I2S0\_MCLK | I2S0主时钟（系统时钟） |
| FUNC\_I2S0\_SCLK | I2S0串行时钟（位时钟） |
| FUNC\_I2S0\_WS | I2S0帧时钟 |
| FUNC\_I2S0\_IN\_D0 | I2S0串行输入数据接口0 |
| FUNC\_I2S0\_IN\_D1 | I2S0串行输入数据接口1 |
| FUNC\_I2S0\_IN\_D2 | I2S0串行输入数据接口2 |
| FUNC\_I2S0\_IN\_D3 | I2S0串行输入数据接口3 |
| FUNC\_I2S0\_OUT\_D0 | I2S0串行输出数据接口0 |
| FUNC\_I2S0\_OUT\_D1 | I2S0串行输出数据接口1 |
| FUNC\_I2S0\_OUT\_D2 | I2S0串行输出数据接口2 |
| FUNC\_I2S0\_OUT\_D3 | I2S0串行输出数据接口3 |
| FUNC\_I2S1\_MCLK | I2S1主时钟（系统时钟） |
| FUNC\_I2S1\_SCLK | I2S1串行时钟（位时钟） |
| FUNC\_I2S1\_WS | I2S1帧时钟 |
| FUNC\_I2S1\_IN\_D0 | I2S1串行输入数据接口0 |
| FUNC\_I2S1\_IN\_D1 | I2S1串行输入数据接口1 |
| FUNC\_I2S1\_IN\_D2 | I2S1串行输入数据接口2 |
| FUNC\_I2S1\_IN\_D3 | I2S1串行输入数据接口3 |
| FUNC\_I2S1\_OUT\_D0 | I2S1串行输出数据接口0 |
| FUNC\_I2S1\_OUT\_D1 | I2S1串行输出数据接口1 |
| FUNC\_I2S1\_OUT\_D2 | I2S1串行输出数据接口2 |
| FUNC\_I2S1\_OUT\_D3 | I2S1串行输出数据接口3 |
| FUNC\_I2S2\_MCLK | I2S2主时钟（系统时钟） |
| FUNC\_I2S2\_SCLK | I2S2串行时钟（位时钟） |
| FUNC\_I2S2\_WS | I2S2帧时钟 |
| FUNC\_I2S2\_IN\_D0 | I2S2串行输入数据接口0 |
| FUNC\_I2S2\_IN\_D1 | I2S2串行输入数据接口1 |
| FUNC\_I2S2\_IN\_D2 | I2S2串行输入数据接口2 |
| FUNC\_I2S2\_IN\_D3 | I2S2串行输入数据接口3 |
| FUNC\_I2S2\_OUT\_D0 | I2S2串行输出数据接口0 |
| FUNC\_I2S2\_OUT\_D1 | I2S2串行输出数据接口1 |
| FUNC\_I2S2\_OUT\_D2 | I2S2串行输出数据接口2 |
| FUNC\_I2S2\_OUT\_D3 | I2S2串行输出数据接口3 |
| FUNC\_RESV0 | 保留功能 |
| FUNC\_RESV1 | 保留功能 |
| FUNC\_RESV2 | 保留功能 |
| FUNC\_RESV3 | 保留功能 |
| FUNC\_RESV4 | 保留功能 |
| FUNC\_RESV5 | 保留功能 |
| FUNC\_I2C0\_SCLK | I2C0串行时钟 |
| FUNC\_I2C0\_SDA | I2C0串行数据接口 |
| FUNC\_I2C1\_SCLK | I2C1串行时钟 |
| FUNC\_I2C1\_SDA | I2C1串行数据接口 |
| FUNC\_I2C2\_SCLK | I2C2串行时钟 |
| FUNC\_I2C2\_SDA | I2C2串行数据接口 |
| FUNC\_CMOS\_XCLK | DVP系统时钟 |
| FUNC\_CMOS\_RST | DVP系统复位信号 |
| FUNC\_CMOS\_PWDN | DVP使能信号 |
| FUNC\_CMOS\_VSYNC | DVP场同步 |
| FUNC\_CMOS\_HREF | DVP行参考信号 |
| FUNC\_CMOS\_PCLK | 像素时钟 |
| FUNC\_CMOS\_D0 | 像素数据0 |
| FUNC\_CMOS\_D1 | 像素数据1 |
| FUNC\_CMOS\_D2 | 像素数据2 |
| FUNC\_CMOS\_D3 | 像素数据3 |
| FUNC\_CMOS\_D4 | 像素数据4 |
| FUNC\_CMOS\_D5 | 像素数据5 |
| FUNC\_CMOS\_D6 | 像素数据6 |
| FUNC\_CMOS\_D7 | 像素数据7 |
| FUNC\_SCCB\_SCLK | SCCB时钟 |
| FUNC\_SCCB\_SDA | SCCB串行数据信号 |
| FUNC\_UART1\_CTS | UART1清除发送信号 |
| FUNC\_UART1\_DSR | UART1数据设备准备信号 |
| FUNC\_UART1\_DCD | UART1数据载波检测 |
| FUNC\_UART1\_RI | UART1振铃指示 |
| FUNC\_UART1\_SIR\_IN | UART1串行红外输入信号 |
| FUNC\_UART1\_DTR | UART1数据终端准备信号 |
| FUNC\_UART1\_RTS | UART1发送请求信号 |
| FUNC\_UART1\_OUT2 | UART1用户指定输出信号2 |
| FUNC\_UART1\_OUT1 | UART1用户指定输出信号1 |
| FUNC\_UART1\_SIR\_OUT | UART1串行红外输出信号 |
| FUNC\_UART1\_BAUD | UART1时钟 |
| FUNC\_UART1\_RE | UART1接收使能 |
| FUNC\_UART1\_DE | UART1发送使能 |
| FUNC\_UART1\_RS485\_EN | UART1使能RS485 |
| FUNC\_UART2\_CTS | UART2清除发送信号 |
| FUNC\_UART2\_DSR | UART2数据设备准备信号 |
| FUNC\_UART2\_DCD | UART2数据载波检测 |
| FUNC\_UART2\_RI | UART2振铃指示 |
| FUNC\_UART2\_SIR\_IN | UART2串行红外输入信号 |
| FUNC\_UART2\_DTR | UART2数据终端准备信号 |
| FUNC\_UART2\_RTS | UART2发送请求信号 |
| FUNC\_UART2\_OUT2 | UART2用户指定输出信号2 |
| FUNC\_UART2\_OUT1 | UART2用户指定输出信号1 |
| FUNC\_UART2\_SIR\_OUT | UART2串行红外输出信号 |
| FUNC\_UART2\_BAUD | UART2时钟 |
| FUNC\_UART2\_RE | UART2接收使能 |
| FUNC\_UART2\_DE | UART2发送使能 |
| FUNC\_UART2\_RS485\_EN | UART2使能RS485 |
| FUNC\_UART3\_CTS | 清除发送信号 |
| FUNC\_UART3\_DSR | 数据设备准备信号 |
| FUNC\_UART3\_DCD | UART3数据载波检测 |
| FUNC\_UART3\_RI | UART3振铃指示 |
| FUNC\_UART3\_SIR\_IN | UART3串行红外输入信号 |
| FUNC\_UART3\_DTR | UART3数据终端准备信号 |
| FUNC\_UART3\_RTS | UART3发送请求信号 |
| FUNC\_UART3\_OUT2 | UART3用户指定输出信号2 |
| FUNC\_UART3\_OUT1 | UART3用户指定输出信号1 |
| FUNC\_UART3\_SIR\_OUT | UART3串行红外输出信号 |
| FUNC\_UART3\_BAUD | UART3时钟 |
| FUNC\_UART3\_RE | UART3接收使能 |
| FUNC\_UART3\_DE | UART3发送使能 |
| FUNC\_UART3\_RS485\_EN | UART3使能RS485 |
| FUNC\_TIMER0\_TOGGLE1 | TIMER0输出信号1 |
| FUNC\_TIMER0\_TOGGLE2 | TIMER0输出信号2 |
| FUNC\_TIMER0\_TOGGLE3 | TIMER0输出信号3 |
| FUNC\_TIMER0\_TOGGLE4 | TIMER0输出信号4 |
| FUNC\_TIMER1\_TOGGLE1 | TIMER1输出信号1 |
| FUNC\_TIMER1\_TOGGLE2 | TIMER1输出信号2 |
| FUNC\_TIMER1\_TOGGLE3 | TIMER1输出信号3 |
| FUNC\_TIMER1\_TOGGLE4 | TIMER1输出信号4 |
| FUNC\_TIMER2\_TOGGLE1 | TIMER2输出信号1 |
| FUNC\_TIMER2\_TOGGLE2 | TIMER2输出信号2 |
| FUNC\_TIMER2\_TOGGLE3 | TIMER2输出信号3 |
| FUNC\_TIMER2\_TOGGLE4 | TIMER2输出信号4 |
| FUNC\_CLK\_SPI2 | SPI2时钟 |
| FUNC\_CLK\_I2C2 | I2C2时钟 |
| FUNC\_INTERNAL0 | 内部功能0 |
| FUNC\_INTERNAL1 | 内部功能1 |
| FUNC\_INTERNAL2 | 内部功能2 |
| FUNC\_INTERNAL3 | 内部功能3 |
| FUNC\_INTERNAL4 | 内部功能4 |
| FUNC\_INTERNAL5 | 内部功能5 |
| FUNC\_INTERNAL6 | 内部功能6 |
| FUNC\_INTERNAL7 | 内部功能7 |
| FUNC\_INTERNAL8 | 内部功能8 |
| FUNC\_INTERNAL9 | 内部功能9 |
| FUNC\_INTERNAL10 | 内部功能10 |
| FUNC\_INTERNAL11 | 内部功能11 |
| FUNC\_INTERNAL12 | 内部功能12 |
| FUNC\_INTERNAL13 | 内部功能13 |
| FUNC\_INTERNAL14 | 内部功能14 |
| FUNC\_INTERNAL15 | 内部功能15 |
| FUNC\_INTERNAL16 | 内部功能16 |
| FUNC\_INTERNAL17 | 内部功能17 |
| FUNC\_CONSTANT | 常量 |
| FUNC\_INTERNAL18 | 内部功能18 |
| FUNC\_DEBUG0 | 调试功能0 |
| FUNC\_DEBUG1 | 调试功能1 |
| FUNC\_DEBUG2 | 调试功能2 |
| FUNC\_DEBUG3 | 调试功能3 |
| FUNC\_DEBUG4 | 调试功能4 |
| FUNC\_DEBUG5 | 调试功能5 |
| FUNC\_DEBUG6 | 调试功能6 |
| FUNC\_DEBUG7 | 调试功能7 |
| FUNC\_DEBUG8 | 调试功能8 |
| FUNC\_DEBUG9 | 调试功能9 |
| FUNC\_DEBUG10 | 调试功能10 |
| FUNC\_DEBUG11 | 调试功能11 |
| FUNC\_DEBUG12 | 调试功能12 |
| FUNC\_DEBUG13 | 调试功能13 |
| FUNC\_DEBUG14 | 调试功能14 |
| FUNC\_DEBUG15 | 调试功能15 |
| FUNC\_DEBUG16 | 调试功能16 |
| FUNC\_DEBUG17 | 调试功能17 |
| FUNC\_DEBUG18 | 调试功能18 |
| FUNC\_DEBUG19 | 调试功能19 |
| FUNC\_DEBUG20 | 调试功能20 |
| FUNC\_DEBUG21 | 调试功能21 |
| FUNC\_DEBUG22 | 调试功能22 |
| FUNC\_DEBUG23 | 调试功能23 |
| FUNC\_DEBUG24 | 调试功能24 |
| FUNC\_DEBUG25 | 调试功能25 |
| FUNC\_DEBUG26 | 调试功能26 |
| FUNC\_DEBUG27 | 调试功能27 |
| FUNC\_DEBUG28 | 调试功能28 |
| FUNC\_DEBUG29 | 调试功能29 |
| FUNC\_DEBUG30 | 调试功能30 |
| FUNC\_DEBUG31 | 调试功能31 |

