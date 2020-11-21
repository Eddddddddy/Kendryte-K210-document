# 通用输入/输出 \(GPIO\)

## 概述 <a id="&#x6982;&#x8FF0;"></a>

芯片有8个通用GPIO。

## 功能描述 <a id="&#x529F;&#x80FD;&#x63CF;&#x8FF0;"></a>

GPIO 模块具有以下功能：

* 可配置上下拉驱动模式

## API 参考 <a id="api-&#x53C2;&#x8003;"></a>

对应的头文件 `gpio.h`

为用户提供以下接口

* gpio\_init
* gpio\_set\_drive\_mode
* gpio\_set\_pin
* gpio\_get\_pin

### gpio\_init <a id="gpioinit"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

初始化GPIO。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int gpio_init(void)
```

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### gpio\_set\_drive\_mode <a id="gpiosetdrivemode"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置GPIO驱动模式。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void gpio_set_drive_mode(uint8_t pin, gpio_drive_mode_t mode)
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
void gpio_set_pin(uint8_t pin, gpio_pin_value_t value)
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
gpio_pin_value_t gpio_get_pin(uint8_t pin)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| pin | GPIO管脚 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

获取的GPIO管脚值。

### 举例 <a id="&#x4E3E;&#x4F8B;"></a>

```text

gpio_init();
fpioa_set_function(13, FUNC_GPIO3);
gpio_set_drive_mode(3, GPIO_DM_OUTPUT);
gpio_set_pin(3, GPIO_PV_High);
```

## 数据类型 <a id="&#x6570;&#x636E;&#x7C7B;&#x578B;"></a>

相关数据类型、数据结构定义如下：

* gpio\_drive\_mode\_t：GPIO驱动模式。
* gpio\_pin\_value\_t：GPIO值。

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

