# 高速通用输入/输出 \(GPIOHS\)

## 概述 <a id="&#x6982;&#x8FF0;"></a>

芯片有32个高速GPIO。与普通GPIO相似，管脚反转能力更强。

## 功能描述 <a id="&#x529F;&#x80FD;&#x63CF;&#x8FF0;"></a>

GPIOHS模块具有以下功能：

* 可配置上下拉驱动模式
* 支持上升沿、下降沿和双沿触发

## API 参考 <a id="api-&#x53C2;&#x8003;"></a>

对应的头文件 `gpiohs.h`

为用户提供以下接口

* gpiohs\_set\_drive\_mode
* gpiohs\_set\_pin
* gpiohs\_get\_pin
* gpiohs\_set\_pin\_edge
* gpiohs\_set\_irq \(0.6.0后不再支持，请使用gpiohs\_irq\_register\)
* gpiohs\_irq\_register
* gpiohs\_irq\_unregister

### gpiohs\_set\_drive\_mode <a id="gpiohssetdrivemode"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置GPIO驱动模式。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void gpiohs_set_drive_mode(uint8_t pin, gpio_drive_mode_t mode)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| pin | GPIO管脚 | 输入 |
| mode | GPIO驱动模式 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### gpio\_set\_pin <a id="gpiosetpin"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置GPIO管脚值。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void gpiohs_set_pin(uint8_t pin, gpio_pin_value_t value)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| pin | GPIO管脚 | 输入 |
| value | GPIO值 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### gpio\_get\_pin <a id="gpiogetpin"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

获取GPIO管脚值。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
gpio_pin_value_t gpiohs_get_pin(uint8_t pin)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| pin | GPIO管脚 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

获取的GPIO管脚值。

### gpiohs\_set\_pin\_edge <a id="gpiohssetpinedge"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置高速GPIO中断触发模式。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void gpiohs_set_pin_edge(uint8_t pin, gpio_pin_edge_t edge)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| pin | GPIO管脚 | 输入 |
| edge | 中断触发方式 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### gpiohs\_set\_irq <a id="gpiohssetirq"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置高速GPIO的中断回调函数。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void gpiohs_set_irq(uint8_t pin, uint32_t priority, void(*func)());
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| pin | GPIO管脚 | 输入 |
| priority | 中断优先级 | 输入 |
| func | 中断回调函数 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### gpiohs\_irq\_register <a id="gpiohsirqregister"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置高速GPIO的中断回调函数。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void gpiohs_irq_register(uint8_t pin, uint32_t priority, plic_irq_callback_t callback, void *ctx)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| pin | GPIO管脚 | 输入 |
| priority | 中断优先级 | 输入 |
| plic\_irq\_callback\_t | 中断回调函数 | 输入 |
| ctx | 回调函数参数 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### gpiohs\_irq\_unregister <a id="gpiohsirqunregister"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

注销GPIOHS中断。

### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void gpiohs_irq_unregister(uint8_t pin)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| pin | GPIO管脚 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### 举例 <a id="&#x4E3E;&#x4F8B;"></a>

```text
void irq_gpiohs2(void *ctx)
{
    printf("Hello world\n");
}

fpioa_set_function(13, FUNC_GPIOHS3);
gpiohs_set_drive_mode(3, GPIO_DM_OUTPUT);
gpiohs_set_pin(3, GPIO_PV_High);

plic_init();
fpioa_set_function(14, FUNC_GPIOHS2);
gpiohs_set_drive_mode(2, GPIO_DM_INPUT);
gpiohs_set_pin_edge(2, GPIO_PE_BOTH);
gpiohs_irq_register(2, 1, irq_gpiohs2, NULL);
sysctl_enable_irq();
```

## 数据类型 <a id="&#x6570;&#x636E;&#x7C7B;&#x578B;"></a>

相关数据类型、数据结构定义如下：

* gpio\_drive\_mode\_t：GPIO驱动模式。
* gpio\_pin\_value\_t：GPIO值。
* gpio\_pin\_edge\_t：GPIO边沿触发模式。

### gpio\_drive\_mode\_t <a id="gpiodrivemodet"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

GPIO驱动模式。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _gpio_drive_mode
{
    GPIO_DM_INPUT,
    GPIO_DM_INPUT_PULL_DOWN,
    GPIO_DM_INPUT_PULL_UP,
    GPIO_DM_OUTPUT,
} gpio_drive_mode_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| GPIO\_DM\_INPUT | 输入 |
| GPIO\_DM\_INPUT\_PULL\_DOWN | 输入下拉 |
| GPIO\_DM\_INPUT\_PULL\_UP | 输入上拉 |
| GPIO\_DM\_OUTPUT | 输出 |

### gpio\_pin\_value\_t <a id="gpiopinvaluet"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

GPIO 值。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _gpio_pin_value
{
    GPIO_PV_LOW,
    GPIO_PV_HIGH
} gpio_pin_value_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| GPIO\_PV\_LOW | 低 |
| GPIO\_PV\_HIGH | 高 |

### gpio\_pin\_edge\_t <a id="gpiopinedget"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

高速GPIO边沿触发模式。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _gpio_pin_edge
{
    GPIO_PE_NONE,
    GPIO_PE_FALLING,
    GPIO_PE_RISING,
    GPIO_PE_BOTH,
    GPIO_PE_LOW,
    GPIO_PE_HIGH = 8,
} gpio_pin_edge_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| GPIO\_PE\_NONE | 不触发 |
| GPIO\_PE\_FALLING | 下降沿触发 |
| GPIO\_PE\_RISING | 上升沿触发 |
| GPIO\_PE\_BOTH | 双沿触发 |
| GPIO\_PE\_LOW | 低电平触发 |
| GPIO\_PE\_HIGH | 高电平触发 |

