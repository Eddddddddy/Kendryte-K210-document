# 神经网络处理器 \(KPU\)

## 概述 <a id="&#x6982;&#x8FF0;"></a>

KPU 是通用的神经网络处理器，它可以在低功耗的情况下实现卷积神经网络计算，实时获取被检测目标的大小、坐标和种类，对人脸或者物体进行检测和分类。 使用kpu时，必须结合model compiler。

## 功能描述 <a id="&#x529F;&#x80FD;&#x63CF;&#x8FF0;"></a>

KPU 具备以下几个特点：

* 支持主流训练框架按照特定限制规则训练出来的定点化模型
* 对网络层数无直接限制，支持每层卷积神经网络参数单独配置，包括输入输出通道数目、输入输出行宽列高
* 支持两种卷积内核 1x1 和 3x3
* 支持任意形式的激活函数
* 实时工作时最大支持神经网络参数大小为 5.5MiB 到 5.9MiB
* 非实时工作时最大支持网络参数大小为（Flash 容量-软件体积）

## API 参考 <a id="api-&#x53C2;&#x8003;"></a>

对应的头文件 `kpu.h`

为用户提供以下接口

* kpu\_task\_init \(0.6.0以后不再支持，请使用kpu\_single\_task\_init\)
* kpu\_run \(0.6.0以后不再支持，请使用kpu\_start\)
* kpu\_get\_output\_buf \(0.6.0以后不再支持\)
* kpu\_release\_output\_buf \(0.6.0以后不再支持\)
* kpu\_start
* kpu\_single\_task\_init
* kpu\_single\_task\_deinit
* kpu\_model\_load\_from\_buffer
* kpu\_load\_kmodel
* kpu\_model\_free
* kpu\_get\_output
* kpu\_run\_kmodel

### kpu\_task\_init <a id="kputaskinit"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

初始化kpu任务句柄，该函数具体实现在model compiler生成的gencode\_output.c中。

#### 函数定义 <a id="&#x51FD;&#x6570;&#x5B9A;&#x4E49;"></a>

```text
kpu_task_t* kpu_task_init(kpu_task_t* task)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| task | KPU任务句柄 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

KPU任务句柄。

### kpu\_run <a id="kpurun"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

启动KPU，进行AI运算。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int kpu_run(kpu_task_t* v_task, dmac_channel_number_t dma_ch, const void *src, void* dest, plic_irq_callback_t callback)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| task | KPU任务句柄 | 输入 |
| dma\_ch | DMA通道 | 输入 |
| src | 输入图像数据 | 输入 |
| dest | 运算输出结果 | 输出 |
| callback | 运算完成回调函数 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | KPU忙，失败 |

### kpu\_get\_output\_buf <a id="kpugetoutputbuf"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

获取KPU输出结果的缓存。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
uint8_t *kpu_get_output_buf(kpu_task_t* task)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| task | KPU任务句柄 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

KPU输出结果的缓存的指针。

### kpu\_release\_output\_buf <a id="kpureleaseoutputbuf"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

释放KPU输出结果缓存。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void kpu_release_output_buf(uint8_t *output_buf)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| output\_buf | KPU输出结果缓存 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无

### kpu\_start <a id="kpustart"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

启动KPU，进行AI运算。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int kpu_start(kpu_task_t *task)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| task | KPU任务句柄 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | KPU忙，失败 |

### kpu\_single\_task\_init <a id="kpusingletaskinit"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

初始化kpu任务句柄。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int kpu_single_task_init(kpu_task_t *task)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| task | KPU任务句柄 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### kpu\_single\_task\_deinit <a id="kpusingletaskdeinit"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

注销kpu任务。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int kpu_single_task_deinit(kpu_task_t *task)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| task | KPU任务句柄 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### kpu\_model\_load\_from\_buffer <a id="kpumodelloadfrombuffer"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

解析kmodel并初始化kpu句柄。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int kpu_model_load_from_buffer(kpu_task_t *task, uint8_t *buffer, kpu_model_layer_metadata_t **meta);
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| task | KPU任务句柄 | 输入 |
| buffer | kmodel数据 | 输入 |
| meta | 内部测试数据，用户设置为NULL | 输出 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### kpu\_load\_kmodel <a id="kpuloadkmodel"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

加载kmodel，需要与nncase配合使用。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int kpu_load_kmodel(kpu_model_context_t *ctx, const uint8_t *buffer)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| ctx | KPU任务句柄 | 输入 |
| buffer | kmodel数据 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### kpu\_model\_free <a id="kpumodelfree"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

释放kpu资源。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void kpu_model_free(kpu_model_context_t *ctx)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| ctx | KPU任务句柄 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### kpu\_get\_output <a id="kpugetoutput"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

获取KPU最终处理的结果。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int kpu_get_output(kpu_model_context_t *ctx, uint32_t index, uint8_t **data, size_t *size)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| ctx | KPU任务句柄 | 输入 |
| index | 结果的索引值，如kmodel有关 | 输入 |
| data | 结果 | 输入 |
| size | 大小（字节） | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### kpu\_run\_kmodel <a id="kpurunkmodel"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

运行kmodel。

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
int kpu_run_kmodel(kpu_model_context_t *ctx, const uint8_t *src, dmac_channel_number_t dma_ch, kpu_done_callback_t done_callback, void *userdata)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| ctx | KPU任务句柄 | 输入 |
| src | 源数据 | 输入 |
| dma\_ch | DMA通道 | 输入 |
| done\_callback | 完成后回调函数 | 输入 |
| userdata | 回调的参数 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

| 返回值 | 描述 |
| :--- | :--- |
| 0 | 成功 |
| 非0 | 失败 |

### 举例 <a id="&#x4E3E;&#x4F8B;"></a>

```text

kpu_task_t task;
volatile uint8_t g_ai_done_flag;
static int ai_done(void *ctx)
{
    g_ai_done_flag = 1;
    return 0;
}


kpu_task_gencode_output_init(&task); 
task.src = g_ai_buf;
task.dma_ch = 5;
task.callback = ai_done;
kpu_single_task_init(&task);


kpu_start(&task);
```

## 数据类型 <a id="&#x6570;&#x636E;&#x7C7B;&#x578B;"></a>

相关数据类型、数据结构定义如下：

* kpu\_task\_t：kpu任务结构体。

### kpu\_task\_t <a id="kputaskt"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

kpu任务结构体。

#### 定义 <a id="&#x5B9A;&#x4E49;"></a>

```text
typedef struct
{
    kpu_layer_argument_t *layers;
    kpu_layer_argument_t *remain_layers;
    plic_irq_callback_t callback;
    void *ctx;
    uint64_t *src;
    uint64_t *dst;
    uint32_t src_length;
    uint32_t dst_length;
    uint32_t layers_length;
    uint32_t remain_layers_length;
    dmac_channel_number_t dma_ch;
    uint32_t eight_bit_mode;
    float output_scale;
    float output_bias;
    float input_scale;
    float input_bias;
} kpu_task_t;
```

#### 成员 <a id="&#x6210;&#x5458;"></a>

| 成员名称 | 描述 |
| :--- | :--- |
| layers | KPU参数指针\(MC初始化，用户不必关心\) |
| remain\_layers | KPU参数指针（运算过程中使用，用户不必关心） |
| callback | 运算完成回调函数（需要用户设置） |
| ctx | 回调函数的参数（非空需要用户设置） |
| src | 运算源数据（需要用户设置） |
| dst | 运算结果输出指针（KPU初始化赋值，用户不必关心） |
| src\_length | 源数据长度\(MC初始化，用户不必关心\) |
| dst\_length | 运算结果长度\(MC初始化，用户不必关心\) |
| layers\_length | 层数\(MC初始化，用户不必关心\) |
| remain\_layers\_length | 剩余层数（运算过程中使用，用户不必关心） |
| dma\_ch | 使用的DMA通道号（需要用户设置） |
| eight\_bit\_mode | 是否是8比特模式\(MC初始化，用户不必关心\) |
| output\_scale | 输出scale值\(MC初始化，用户不必关心\) |
| output\_bias | 输出bias值\(MC初始化，用户不必关心\) |
| input\_scale | 输入scale值\(MC初始化，用户不必关心\) |
| input\_bias | 输入bias值\(MC初始化，用户不必关心\) |

