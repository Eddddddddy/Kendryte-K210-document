# 集成电路内置总线\(I2C\)

## 概述 <a id="&#x6982;&#x8FF0;"></a>

I2C 总线用于和多个外部设备进行通信。多个外部设备可以共用一个 I2C 总线。

## 功能描述 <a id="&#x529F;&#x80FD;&#x63CF;&#x8FF0;"></a>

I2C 模块具有以下功能：

* 独立的 I2C 设备封装外设相关参数
* 自动处理多设备总线争用

## API参考 <a id="api&#x53C2;&#x8003;"></a>

对应的头文件 `i2c.h`

为用户提供以下接口

* i2c\_init
* i2c\_init\_as\_slave
* i2c\_send\_data
* i2c\_send\_data\_dma
* i2c\_recv\_data
* i2c\_recv\_data\_dma
* i2c\_handle\_data\_dma

### i2c\_init <a id="i2cinit"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

配置 I²C 器件从地址、寄存器位宽度和 I²C 速率。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void i2c_init(i2c_device_number_t i2c_num, uint32_t slave_address, uint32_t address_width, uint32_t i2c_clk)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| i2c\_num | I²C号 | 输入 |
| slave\_address | I²C 器件从地址 | 输入 |
| address\_width | I²C 器件寄存器宽度\(7或10\) | 输入 |
| i2c\_clk | I²C 速率 \(Hz\) | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### i2c\_init\_as\_slave <a id="i2cinitasslave"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

配置 I²C 为从模式。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void i2c_init_as_slave(i2c_device_number_t i2c_num, uint32_t slave_address, uint32_t address_width, const i2c_slave_handler_t *handler)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| i2c\_num | I²C号 | 输入 |
| slave\_address | I²C 从模式的地址 | 输入 |
| address\_width | I²C 器件寄存器宽度\(7或10\) | 输入 |
| handler | I²C 从模式的中断处理函数 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### i2c\_send\_data <a id="i2csenddata"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

写数据。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int i2c_send_data(i2c_device_number_t i2c_num, const uint8_t *send_buf, size_t send_buf_len)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| i2c\_num | I²C号 | 输入 |
| send\_buf | 待传输数据 | 输入 |
| send\_buf\_len | 待传输数据长度 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### i2c\_send\_data\_dma <a id="i2csenddatadma"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

通过DMA写数据。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void i2c_send_data_dma(dmac_channel_number_t dma_channel_num, i2c_device_number_t i2c_num, const uint8_t *send_buf, size_t send_buf_len)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| dma\_channel\_num | 使用的dma通道号 | 输入 |
| i2c\_num | I²C号 | 输入 |
| send\_buf | 待传输数据 | 输入 |
| send\_buf\_len | 待传输数据长度 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无

### i2c\_recv\_data <a id="i2crecvdata"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

通过CPU读数据。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int i2c_recv_data(i2c_device_number_t i2c_num, const uint8_t *send_buf, size_t send_buf_len, uint8_t *receive_buf, size_t receive_buf_len)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| i2c\_num | I²C 总线号 | 输入 |
| send\_buf | 待传输数据，一般情况是i2c外设的寄存器，如果没有设置为NULL | 输入 |
| send\_buf\_len | 待传输数据长度，如果没有则写0 | 输入 |
| receive\_buf | 接收数据内存 | 输出 |
| receive\_buf\_len | 接收数据的长度 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### i2c\_recv\_data\_dma <a id="i2crecvdatadma"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

通过dma读数据。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void i2c_recv_data_dma(dmac_channel_number_t dma_send_channel_num, dmac_channel_number_t dma_receive_channel_num,
    i2c_device_number_t i2c_num, const uint8_t *send_buf, size_t send_buf_len, uint8_t *receive_buf, size_t receive_buf_len)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| dma\_send\_channel\_num | 发送数据使用的dma通道 | 输入 |
| dma\_receive\_channel\_num | 接收数据使用的dma通道 | 输入 |
| i2c\_num | I²C 总线号 | 输入 |
| send\_buf | 待传输数据，一般情况是i2c外设的寄存器，如果没有设置为NULL | 输入 |
| send\_buf\_len | 待传输数据长度，如果没有则写0 | 输入 |
| receive\_buf | 接收数据内存 | 输出 |
| receive\_buf\_len | 接收数据的长度 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无

### i2c\_handle\_data\_dma <a id="i2chandledatadma"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

I2C 使用dma传输数据。

**函数原型**

```text
void i2c_handle_data_dma(i2c_device_number_t i2c_num, i2c_data_t data, plic_interrupt_t *cb);
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| i2c\_num | I²C 总线号 | 输入 |
| data | I2C数据相关的参数，详见i2c\_data\_t说明 | 输入 |
| cb | dma中断回调函数，如果设置为NULL则为阻塞模式，直至传输完毕后退出函数 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无

### 举例 <a id="&#x4E3E;&#x4F8B;"></a>

```text

i2c_init(I2C_DEVICE_0, 0x32, 7, 200000);
uint8_t reg = 0;
uint8_t data_buf[2] = {0x00,0x01}
data_buf[0] = reg;

i2c_send_data(I2C_DEVICE_0, data_buf, 2);
i2c_send_data_dma(DMAC_CHANNEL0, I2C_DEVICE_0, data_buf, 4);

i2c_receive_data(I2C_DEVICE_0, &reg, 1, data_buf, 1);
i2c_receive_data_dma(DMAC_CHANNEL0, DMAC_CHANNEL1, I2C_DEVICE_0,&reg, 1, data_buf, 1);
```

## 数据类型 <a id="&#x6570;&#x636E;&#x7C7B;&#x578B;"></a>

相关数据类型、数据结构定义如下：

* i2c\_device\_number\_t：i2c号。
* i2c\_slave\_handler\_t：i2c从模式的中断处理函数句柄
* i2c\_data\_t：使用dma传输时数据相关的参数。
* i2c\_transfer\_mode\_t：使用DMA传输数据的模式，发送或接收。

### i2c\_device\_number\_t <a id="i2cdevicenumbert"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

i2c编号。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _i2c_device_number
{
    I2C_DEVICE_0,
    I2C_DEVICE_1,
    I2C_DEVICE_2,
    I2C_DEVICE_MAX,
} i2c_device_number_t;
```

### i2c\_slave\_handler\_t <a id="i2cslavehandlert"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

i2c从模式的中断处理函数句柄。根据不同的中断状态执行相应的函数操作。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef struct _i2c_slave_handler
{
    void(*on_receive)(uint32_t data);
    uint32_t(*on_transmit)();
    void(*on_event)(i2c_event_t event);
} i2c_slave_handler_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| I2C\_DEVICE\_0 | I2C 0 |
| I2C\_DEVICE\_1 | I2C 1 |
| I2C\_DEVICE\_2 | I2C 2 |

### i2c\_data\_t <a id="i2cdatat"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

使用dma传输时数据相关的参数。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef struct _i2c_data_t
{
    dmac_channel_number_t tx_channel;
    dmac_channel_number_t rx_channel;
    uint32_t *tx_buf;
    size_t tx_len;
    uint32_t *rx_buf;
    size_t rx_len;
    i2c_transfer_mode_t transfer_mode;
} i2c_data_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| tx\_channel | 发送时使用的DMA通道号 |
| rx\_channel | 发送时使用的DMA通道号 |
| tx\_buf | 发送的数据 |
| tx\_len | 发送数据的长度 |
| rx\_buf | 接收的数据 |
| rx\_len | 接收数据长度 |
| transfer\_mode | 传输模式，发送或接收 |

### i2c\_transfer\_mode\_t <a id="i2ctransfermodet"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

使用DMA传输数据的模式，发送或接收。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _i2c_transfer_mode
{
    I2C_SEND,
    I2C_RECEIVE,
} i2c_transfer_mode_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| I2C\_SEND | 发送 |
| I2C\_RECEIVE | 接收 |

