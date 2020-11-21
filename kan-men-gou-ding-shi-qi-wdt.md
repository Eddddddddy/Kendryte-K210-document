# 看门狗定时器 \(WDT\)

## 概述 <a id="&#x6982;&#x8FF0;"></a>

WDT 提供系统出错或无响应时的恢复功能。

## 功能描述 <a id="&#x529F;&#x80FD;&#x63CF;&#x8FF0;"></a>

WDT 模块具有以下功能：

* 配置超时时间
* 手动重启计时

## API 参考 <a id="api-&#x53C2;&#x8003;"></a>

对应的头文件 `wdt.h`

为用户提供以下接口

* wdt\_init
* wdt\_start\(0.6.0后不再支持，请使用wdt\_init\)
* wdt\_stop
* wdt\_feed
* wdt\_clear\_interrupt

### wdt\_init <a id="wdtinit"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

配置参数，启动看门狗。不使用中断的话，将on\_irq设置为NULL。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
uint32_t wdt_init(wdt_device_number_t id, uint64_t time_out_ms, plic_irq_callback_t on_irq, void *ctx)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| id | 看门狗编号 | 输入 |
| time\_out\_ms | 超时时间（毫秒） | 输入 |
| on\_irq | 中断回调函数 | 输入 |
| ctx | 回调函数参数 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

看门狗超时重启的实际时间（毫秒）。与time\_out\_ms有差异，一般情况会大于这个时间。在外部晶振26M的情况下，最大超时时间为330毫秒。

### wdt\_start <a id="wdtstart"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

启动看门狗。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void wdt_start(wdt_device_number_t id, uint64_t time_out_ms, plic_irq_callback_t on_irq)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| id | 看门狗编号 | 输入 |
| time\_out\_ms | 超时时间（毫秒） | 输入 |
| on\_irq | 中断回调函数 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无

### wdt\_stop <a id="wdtstop"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

关闭看门狗。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void wdt_stop(wdt_device_number_t id)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| id | 看门狗编号 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### wdt\_feed <a id="wdtfeed"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

喂狗。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void wdt_feed(wdt_device_number_t id)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| id | 看门狗编号 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### wdt\_clear\_interrupt <a id="wdtclearinterrupt"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

清除中断。如果在中断函数中清除中断，则看门狗不会重启。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void wdt_clear_interrupt(wdt_device_number_t id)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| id | 看门狗编号 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### 举例 <a id="&#x4E3E;&#x4F8B;"></a>

```text

int wdt0_irq(void *ctx)
{
    printf("Hello_world\n");
    return 0;
}
plic_init();
sysctl_enable_irq();
wdt_init(WDT_DEVICE_0, 2000, wdt0_irq, NULL);
```

## 数据类型 <a id="&#x6570;&#x636E;&#x7C7B;&#x578B;"></a>

相关数据类型、数据结构定义如下：

* wdt\_device\_number\_t

### wdt\_device\_number\_t <a id="wdtdevicenumbert"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

看门狗编号。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _wdt_device_number
{
    WDT_DEVICE_0,
    WDT_DEVICE_1,
    WDT_DEVICE_MAX,
} wdt_device_number_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| WDT\_DEVICE\_0 | 看门狗 0 |
| WDT\_DEVICE\_1 | 看门狗 1 |

