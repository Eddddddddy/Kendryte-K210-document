# 脉冲宽度调制器\(PWM\)

## 概述 <a id="&#x6982;&#x8FF0;"></a>

PWM 用于控制脉冲输出的占空比。其本质是一个定时器，所以注意设置PWM号与通道时不要与TIMER定时器冲突。

## 功能描述 <a id="&#x529F;&#x80FD;&#x63CF;&#x8FF0;"></a>

PWM 模块具有以下功能：

* 配置 PWM 输出频率
* 配置 PWM 每个管脚的输出占空比

## API参考 <a id="api&#x53C2;&#x8003;"></a>

对应头文件 `pwm.h`

为用户提供以下接口

* pwm\_init
* pwm\_set\_frequency
* pwm\_set\_enable

### pwm\_init <a id="pwminit"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

初始化PWM。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void pwm_init(pwm_device_number_t pwm_number)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| pwm\_number | pwm号 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### pwm\_set\_frequency <a id="pwmsetfrequency"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置频率及占空比。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
double pwm_set_frequency(pwm_device_number_t pwm_number, pwm_channel_number_t channel, double frequency, double duty)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| pwm\_number | PWM号 | 输入 |
| channel | PWM通道号 | 输入 |
| frequency | PWM输出频率 | 输入 |
| duty | 占空比 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

实际输出频率。

### pwm\_set\_enable <a id="pwmsetenable"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

使能禁用PWM。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void pwm_set_enable(pwm_device_number_t pwm_number, uint32_t channel, int enable)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| pwm\_number | PWM号 | 输入 |
| channel | PWM通道号 | 输入 |
| enable | 使能禁用PWM 0：禁用 1：使能 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### 举例 <a id="&#x4E3E;&#x4F8B;"></a>

```text


fpioa_set_function(13, FUNC_TIMER0_TOGGLE1);
pwm_init(PWM_DEVICE_0);
pwm_set_frequency(PWM_DEVICE_0, PWM_CHANNEL_1, 200000, 0.5);
pwm_set_enable(PWM_DEVICE_0, PWM_CHANNEL_1, 1);
```

## 数据类型 <a id="&#x6570;&#x636E;&#x7C7B;&#x578B;"></a>

* pwm\_device\_number\_t：pwm号。
* pwm\_channel\_number\_t：pwm通道号。

### pwm\_device\_number\_t <a id="pwmdevicenumbert"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

pwm号。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _pwm_device_number
{
    PWM_DEVICE_0,
    PWM_DEVICE_1,
    PWM_DEVICE_2,
    PWM_DEVICE_MAX,
} pwm_device_number_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| PWM\_DEVICE\_0 | PWM0 |
| PWM\_DEVICE\_1 | PWM1 |
| PWM\_DEVICE\_2 | PWM2 |

### pwm\_channel\_number\_t <a id="pwmchannelnumbert"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

pwm通道号。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _pwm_channel_number
{
    PWM_CHANNEL_0,
    PWM_CHANNEL_1,
    PWM_CHANNEL_2,
    PWM_CHANNEL_3,
    PWM_CHANNEL_MAX,
} pwm_channel_number_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| PWM\_CHANNEL\_0 | PWM通道0 |
| PWM\_CHANNEL\_1 | PWM通道1 |
| PWM\_CHANNEL\_2 | PWM通道2 |
| PWM\_CHANNEL\_3 | PWM通道3 |

