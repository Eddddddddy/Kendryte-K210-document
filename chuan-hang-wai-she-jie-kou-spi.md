# 串行外设接口\(SPI\)

## 概述 <a id="&#x6982;&#x8FF0;"></a>

SPI 是一种高速的，全双工，同步的通信总线。

## 功能描述 <a id="&#x529F;&#x80FD;&#x63CF;&#x8FF0;"></a>

SPI 模块具有以下功能：

* 独立的 SPI 设备封装外设相关参数
* 自动处理多设备总线争用
* 支持标准、双线、四线、八线模式
* 支持先写后读和全双工读写
* 支持发送一串相同的数据帧，常用于清屏、填充存储扇区等场景

## API参考 <a id="api&#x53C2;&#x8003;"></a>

对应的头文件 `spi.h`

为用户提供以下接口

* spi\_init
* spi\_init\_non\_standard
* spi\_send\_data\_standard
* spi\_send\_data\_standard\_dma
* spi\_receive\_data\_standard
* spi\_receive\_data\_standard\_dma
* spi\_send\_data\_multiple
* spi\_send\_data\_multiple\_dma
* spi\_receive\_data\_multiple
* spi\_receive\_data\_multiple\_dma
* spi\_fill\_data\_dma
* spi\_send\_data\_normal\_dma
* spi\_set\_clk\_rate
* spi\_handle\_data\_dma
* spi\_dup\_send\_receive\_data\_dma
* spi\_slave\_config
* spi\_slave\_dual\_config

### spi\_init <a id="spiinit"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置SPI工作模式、多线模式和位宽。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void spi_init(spi_device_num_t spi_num, spi_work_mode_t work_mode, spi_frame_format_t frame_format, size_t data_bit_length, uint32_t endian)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| spi\_num | SPI号 | 输入 |
| work\_mode | 极性相位的四种模式 | 输入 |
| frame\_format | 多线模式 | 输入 |
| data\_bit\_length | 单次传输的数据的位宽 | 输入 |
| endian | 大小端 0：小端 1：大端 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### spi\_config\_non\_standard <a id="spiconfignonstandard"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

多线模式下设置指令长度、地址长度、等待时钟数、指令地址传输模式。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void spi_init_non_standard(spi_device_num_t spi_num, uint32_t instruction_length, uint32_t address_length, uint32_t wait_cycles, spi_instruction_address_trans_mode_t instruction_address_trans_mode)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| spi\_num | SPI号 | 输入 |
| instruction\_length | 发送指令的位数 | 输入 |
| address\_length | 发送地址的位数 | 输入 |
| wait\_cycles | 等待时钟个数 | 输入 |
| instruction\_address\_trans\_mode | 指令地址传输的方式 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无

### spi\_send\_data\_standard <a id="spisenddatastandard"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

SPI标准模式传输数据。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void spi_send_data_standard(spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint8_t *cmd_buff, size_t cmd_len, const uint8_t *tx_buff, size_t tx_len)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| spi\_num | SPI号 | 输入 |
| chip\_select | 片选信号 | 输入 |
| cmd\_buff | 外设指令地址数据，没有则设为NULL | 输入 |
| cmd\_len | 外设指令地址数据长度，没有则设为0 | 输入 |
| tx\_buff | 发送的数据 | 输入 |
| tx\_len | 发送数据的长度 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无

### spi\_send\_data\_standard\_dma <a id="spisenddatastandarddma"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

SPI标准模式下使用DMA传输数据。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void spi_send_data_standard_dma(dmac_channel_number_t channel_num, spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint8_t *cmd_buff, size_t cmd_len, const uint8_t *tx_buff, size_t tx_len)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| channel\_num | DMA通道号 | 输入 |
| spi\_num | SPI号 | 输入 |
| chip\_select | 片选信号 | 输入 |
| cmd\_buff | 外设指令地址数据，没有则设为NULL | 输入 |
| cmd\_len | 外设指令地址数据长度，没有则设为0 | 输入 |
| tx\_buff | 发送的数据 | 输入 |
| tx\_len | 发送数据的长度 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无

### spi\_receive\_data\_standard <a id="spireceivedatastandard"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

标准模式下接收数据。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void spi_receive_data_standard(spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint8_t *cmd_buff, size_t cmd_len, uint8_t *rx_buff, size_t rx_len)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| spi\_num | SPI号 | 输入 |
| chip\_select | 片选信号 | 输入 |
| cmd\_buff | 外设指令地址数据，没有则设为NULL | 输入 |
| cmd\_len | 外设指令地址数据长度，没有则设为0 | 输入 |
| rx\_buff | 接收的数据 | 输出 |
| rx\_len | 接收数据的长度 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无

### spi\_receive\_data\_standard\_dma <a id="spireceivedatastandarddma"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

标准模式下通过DMA接收数据。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void spi_receive_data_standard_dma(dmac_channel_number_t dma_send_channel_num, dmac_channel_number_t dma_receive_channel_num, spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint8_t *cmd_buff, size_t cmd_len, uint8_t *rx_buff, size_t rx_len)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| dma\_send\_channel\_num | 发送指令地址使用的DMA通道号 | 输入 |
| dma\_receive\_channel\_num | 接收数据使用的DMA通道号 | 输入 |
| spi\_num | SPI号 | 输入 |
| chip\_select | 片选信号 | 输入 |
| cmd\_buff | 外设指令地址数据，没有则设为NULL | 输入 |
| cmd\_len | 外设指令地址数据长度，没有则设为0 | 输入 |
| rx\_buff | 接收的数据 | 输出 |
| rx\_len | 接收数据的长度 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无

### spi\_send\_data\_multiple <a id="spisenddatamultiple"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

多线模式发送数据。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void spi_send_data_multiple(spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint32_t *cmd_buff, size_t cmd_len, uint8_t *tx_buff, size_t tx_len)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| spi\_num | SPI号 | 输入 |
| chip\_select | 片选信号 | 输入 |
| cmd\_buff | 外设指令地址数据，没有则设为NULL | 输入 |
| cmd\_len | 外设指令地址数据长度，没有则设为0 | 输入 |
| tx\_buff | 发送的数据 | 输入 |
| tx\_len | 发送数据的长度 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无

### spi\_send\_data\_multiple\_dma <a id="spisenddatamultipledma"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

多线模式使用DMA发送数据。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void spi_send_data_multiple_dma(dmac_channel_number_t channel_num,spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint32_t *cmd_buff, size_t cmd_len, const uint8_t *tx_buff, size_t tx_len)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| channel\_num | DMA通道号 | 输入 |
| spi\_num | SPI号 | 输入 |
| chip\_select | 片选信号 | 输入 |
| cmd\_buff | 外设指令地址数据，没有则设为NULL | 输入 |
| cmd\_len | 外设指令地址数据长度，没有则设为0 | 输入 |
| tx\_buff | 发送的数据 | 输入 |
| tx\_len | 发送数据的长度 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无

### spi\_receive\_data\_multiple <a id="spireceivedatamultiple"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

多线模式接收数据。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void spi_receive_data_multiple(spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint32_t *cmd_buff, size_t cmd_len, uint8_t *rx_buff, size_t rx_len)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| spi\_num | SPI号 | 输入 |
| chip\_select | 片选信号 | 输入 |
| cmd\_buff | 外设指令地址数据，没有则设为NULL | 输入 |
| cmd\_len | 外设指令地址数据长度，没有则设为0 | 输入 |
| rx\_buff | 接收的数据 | 输出 |
| rx\_len | 接收数据的长度 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无

### spi\_receive\_data\_multiple\_dma <a id="spireceivedatamultipledma"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

多线模式通过DMA接收。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void spi_receive_data_multiple_dma(dmac_channel_number_t dma_send_channel_num, dmac_channel_number_t dma_receive_channel_num, spi_device_num_t spi_num, spi_chip_select_t chip_select, uint32_t const *cmd_buff, size_t cmd_len, uint8_t *rx_buff, size_t rx_len);
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| dma\_send\_channel\_num | 发送指令地址使用的DMA通道号 | 输入 |
| dma\_receive\_channel\_num | 接收数据使用的DMA通道号 | 输入 |
| spi\_num | SPI号 | 输入 |
| chip\_select | 片选信号 | 输入 |
| cmd\_buff | 外设指令地址数据，没有则设为NULL | 输入 |
| cmd\_len | 外设指令地址数据长度，没有则设为0 | 输入 |
| rx\_buff | 接收的数据 | 输出 |
| rx\_len | 接收数据的长度 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无

### spi\_fill\_data\_dma <a id="spifilldatadma"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

通过DMA始终发送同一个数据，可以用于刷新数据。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void spi_fill_data_dma(dmac_channel_number_t channel_num,spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint32_t *tx_buff, size_t tx_len);
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| channel\_num | DMA通道号 | 输入 |
| spi\_num | SPI号 | 输入 |
| chip\_select | 片选信号 | 输入 |
| tx\_buff | 发送的数据,仅发送tx\_buff这一个数据，不会自动增加 | 输入 |
| tx\_len | 发送数据的长度 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无

### spi\_send\_data\_normal\_dma <a id="spisenddatanormaldma"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

通过DMA发送数据。不用设置指令地址。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void spi_send_data_normal_dma(dmac_channel_number_t channel_num, spi_device_num_t spi_num, spi_chip_select_t chip_select, const void *tx_buff, size_t tx_len, spi_transfer_width_t spi_transfer_width)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| channel\_num | DMA通道号 | 输入 |
| spi\_num | SPI号 | 输入 |
| chip\_select | 片选信号 | 输入 |
| tx\_buff | 发送的数据,仅发送tx\_buff这一个数据，不会自动增加 | 输入 |
| tx\_len | 发送数据的长度 | 输入 |
| spi\_transfer\_width | 发送数据的位宽 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无

### spi\_handle\_data\_dma <a id="spihandledatadma"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

SPI 通过DMA传输数据。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void spi_handle_data_dma(spi_device_num_t spi_num, spi_chip_select_t chip_select, spi_data_t data, plic_interrupt_t *cb)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| spi\_num | SPI号 | 输入 |
| data | SPI数据相关的参数，详见spi\_data\_t说明 | 输入 |
| cb | dma中断回调函数，如果设置为NULL则为阻塞模式，直至传输完毕后退出函数 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无

### spi\_slave\_config <a id="spislaveconfig"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

SPI slave 配置，K210的SPI slave是一条数据线复用为MOSI和MISO功能。请参考demo文件spi\_slave，以及README.md的硬件连接。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void spi_slave_config(uint8_t int_pin, uint8_t ready_pin, dmac_channel_number_t dmac_channel, size_t data_bit_length, uint8_t *data, uint32_t len, spi_slave_receive_callback_t callback);
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| spi\_num | SPI号 | 输入 |
| ready\_pin | spi slave准备好后会拉高改pin，master端触发中断。 | 输入 |
| dmac\_channel | 传输数据时用到的dma通道 | 输入 |
| data\_bit\_length | 设置spi传输数据时的数据宽度 | 输入 |
| data | spi slave 接收数据的buffer | 输入 |
| len | spi slave 接收数据的buffer的大小 | 输入 |
| callback | spi slave 接收数据后的回调函数 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无

### spi\_slave\_dual\_config <a id="spislavedualconfig"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

SPI slave 配置，驱动通过iomux内部切换MOSI和MISO功能。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void spi_slave_dual_config(uint8_t int_pin,
                           uint8_t ready_pin,
                           uint8_t mosi_pin,
                           uint8_t miso_pin,
                           dmac_channel_number_t dmac_channel,
                           size_t data_bit_length,
                           uint8_t *data,
                           uint32_t len,
                           spi_slave_receive_callback_t callback);
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| spi\_num | SPI号 | 输入 |
| ready\_pin | spi slave准备好后会拉高改pin，master端触发中断。 | 输入 |
| mosi\_pin | MOSI的IO号 | 输入 |
| miso\_pin | MISO的IO号 | 输入 |
| dmac\_channel | 传输数据时用到的dma通道 | 输入 |
| data\_bit\_length | 设置spi传输数据时的数据宽度 | 输入 |
| data | spi slave 接收数据的buffer | 输入 |
| len | spi slave 接收数据的buffer的大小 | 输入 |
| callback | spi slave 接收数据后的回调函数 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无

### 举例 <a id="&#x4E3E;&#x4F8B;"></a>

```text

spi_init(SPI_DEVICE_0, SPI_WORK_MODE_0, SPI_FF_STANDARD, 8, 0);
uint8_t cmd[4];
cmd[0] = 0x06;
cmd[1] = 0x01;
cmd[2] = 0x02;
cmd[3] = 0x04;
uint8_t data_buf[4] = {0,1,2,3};

spi_send_data_standard(SPI_DEVICE_0, SPI_CHIP_SELECT_0, cmd, 4, data_buf, 4);

spi_receive_data_standard(SPI_DEVICE_0, SPI_CHIP_SELECT_0, cmd, 4, data_buf, 4);


spi_init(SPI_DEVICE_0, SPI_WORK_MODE_0, SPI_FF_QUAD, 8, 0);

spi_init_non_standard(SPI_DEVICE_0, 8, 32, 4, SPI_AITM_ADDR_STANDARD);
uint32 cmd[2];
cmd[0] = 0x06;
cmd[1] = 0x010204;
uint8_t data_buf[4] = {0,1,2,3};

spi_send_data_multiple(SPI_DEVICE_0, SPI_CHIP_SELECT_0, cmd, 2, data_buf, 4);

spi_receive_data_multiple(SPI_DEVICE_0, SPI_CHIP_SELECT_0, cmd, 2, data_buf, 4);


spi_init(SPI_DEVICE_0, SPI_WORK_MODE_2, SPI_FF_OCTAL, 32, 0);

spi_init_non_standard(SPI_DEVICE_0, 0, 32, 0, SPI_AITM_AS_FRAME_FORMAT);
uint32_t data_buf[256] = {0};

spi_send_data_normal_dma(DMAC_CHANNEL0, SPI_DEVICE_0, SPI_CHIP_SELECT_0, data_buf, 256, SPI_TRANS_INT);
uint32_t data = 0x55AA55AA;

spi_fill_data_dma(DMAC_CHANNEL0, SPI_DEVICE_0, SPI_CHIP_SELECT_0,&data, 256);
```

### spi\_set\_clk\_rate <a id="spisetclkrate"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

设置 SPI 的时钟频率

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
uint32_t spi_set_clk_rate(spi_device_num_t spi_num, uint32_t spi_clk)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| spi\_num | SPI号 | 输入 |
| spi\_clk | 目标SPI设备的时钟频率 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

设置完后的SPI设备的时钟频率

## 数据类型 <a id="&#x6570;&#x636E;&#x7C7B;&#x578B;"></a>

相关数据类型、数据结构定义如下：

* spi\_device\_num\_t：SPI编号。
* spi\_mode\_t：SPI 模式。
* spi\_frame\_format\_t：SPI 帧格式。
* spi\_instruction\_address\_trans\_mode\_t：SPI 指令和地址的传输模式。
* spi\_data\_t：使用dma传输时数据相关的参数。
* spi\_transfer\_mode\_t：SPI传输的方式。

### spi\_device\_num\_t <a id="spidevicenumt"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

SPI编号。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _spi_device_num
{
    SPI_DEVICE_0,
    SPI_DEVICE_1,
    SPI_DEVICE_2,
    SPI_DEVICE_3,
    SPI_DEVICE_MAX,
} spi_device_num_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| SPI\_DEVICE\_0 | SPI 0 做为主设备 |
| SPI\_DEVICE\_1 | SPI 1 做为主设备 |
| SPI\_DEVICE\_2 | SPI 2 做为从设备 |
| SPI\_DEVICE\_3 | SPI 3 做为主设备 |

### spi\_mode\_t <a id="spimodet"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

SPI 模式。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _spi_mode
{
    SPI_WORK_MODE_0,
    SPI_WORK_MODE_1,
    SPI_WORK_MODE_2,
    SPI_WORK_MODE_3,
} spi_mode_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| SPI\_WORK\_MODE\_0 | SPI 模式 0 |
| SPI\_WORK\_MODE\_1 | SPI 模式 1 |
| SPI\_WORK\_MODE\_2 | SPI 模式 2 |
| SPI\_WORK\_MODE\_3 | SPI 模式 3 |

### spi\_frame\_format\_t <a id="spiframeformatt"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

SPI 帧格式。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _spi_frame_format
{
    SPI_FF_STANDARD,
    SPI_FF_DUAL,
    SPI_FF_QUAD,
    SPI_FF_OCTAL
} spi_frame_format_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| SPI\_FF\_STANDARD | 标准 |
| SPI\_FF\_DUAL | 双线 |
| SPI\_FF\_QUAD | 四线 |
| SPI\_FF\_OCTAL | 八线（SPI3 不支持） |

### spi\_instruction\_address\_trans\_mode\_t <a id="spiinstructionaddresstransmodet"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

SPI 指令和地址的传输模式。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _spi_instruction_address_trans_mode
{
    SPI_AITM_STANDARD,
    SPI_AITM_ADDR_STANDARD,
    SPI_AITM_AS_FRAME_FORMAT
} spi_instruction_address_trans_mode_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| SPI\_AITM\_STANDARD | 均使用标准帧格式 |
| SPI\_AITM\_ADDR\_STANDARD | 指令使用配置的值，地址使用标准帧格式 |
| SPI\_AITM\_AS\_FRAME\_FORMAT | 均使用配置的值 |

### spi\_data\_t <a id="spidatat"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

使用dma传输时数据相关的参数。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef struct _spi_data_t
{
    dmac_channel_number_t tx_channel;
    dmac_channel_number_t rx_channel;
    uint32_t *tx_buf;
    size_t tx_len;
    uint32_t *rx_buf;
    size_t rx_len;
    spi_transfer_mode_t transfer_mode;
    bool fill_mode;
} spi_data_t;
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
| fill\_mode | 是否以填充方式传输数据，此种情况下DMA传输的源地址地址不会自增加 |

### spi\_transfer\_mode\_t <a id="spitransfermodet"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

SPI传输的方式。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef enum _spi_transfer_mode
{
    SPI_TMOD_TRANS_RECV,
    SPI_TMOD_TRANS,
    SPI_TMOD_RECV,
    SPI_TMOD_EEROM
} spi_transfer_mode_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| SPI\_TMOD\_TRANS\_RECV | 全双工，边发边收 |
| SPI\_TMOD\_TRANS | 只发送 |
| SPI\_TMOD\_RECV | 只接收 |
| SPI\_TMOD\_EEROM | 先发送后接收 |

