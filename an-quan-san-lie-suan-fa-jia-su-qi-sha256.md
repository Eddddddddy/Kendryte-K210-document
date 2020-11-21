# 安全散列算法加速器\(SHA256\)

## 功能描述 <a id="&#x529F;&#x80FD;&#x63CF;&#x8FF0;"></a>

* 支持 SHA-256 的计算

## API参考 <a id="api&#x53C2;&#x8003;"></a>

对应的头文件 `sha256.h`

为用户提供以下接口

* sha256\_init
* sha256\_update
* sha256\_final
* sha256\_hard\_calculate

### sha256\_init <a id="sha256init"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

初始化 SHA256 加速器外设.

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void sha256_init(sha256_context_t *context, size_t input_len)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| context | SHA256的上下文对象 | 输入 |
| input\_len | 待计算SHA256 hash的消息的长度 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### 举例 <a id="&#x4E3E;&#x4F8B;"></a>

```text
sha256_context_t context;
sha256_init(&context, 128U);
```

### sha256\_update <a id="sha256update"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

传入一个数据块参与SHA256 Hash计算

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void sha256_update(sha256_context_t *context, const void *input, size_t input_len)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| context | SHA256的上下文对象 | 输入 |
| input | 待加入计算的SHA256计算的数据块 | 输入 |
| buf\_len | 待加入计算的SHA256计算数据块的长度 | 输入 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### sha256\_final <a id="sha256final"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

结束对数据的 SHA256 Hash 计算

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void sha256_final(sha256_context_t *context, uint8_t *output)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| context | SHA256的上下文对象 | 输入 |
| output | 存放SHA256计算的结果，需保证传入这个buffer的大小为32Bytes以上 | 输出 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### sha256\_hard\_calculate <a id="sha256hardcalculate"></a>

#### 描述 <a id="&#x63CF;&#x8FF0;"></a>

一次性对连续的数据计算它的 SHA256 Hash

#### 函数原型 <a id="&#x51FD;&#x6570;&#x539F;&#x578B;"></a>

```text
void sha256_hard_calculate(const uint8_t *input, size_t input_len, uint8_t *output)
```

#### 参数 <a id="&#x53C2;&#x6570;"></a>

| 参数名称 | 描述 | 输入输出 |
| :--- | :--- | :--- |
| input | 待SHA256计算的数据 | 输入 |
| input\_len | 待SHA256计算数据的长度 | 输入 |
| output | 存放SHA256计算的结果，需保证传入这个buffer的大小为32Bytes以上 | 输出 |

#### 返回值 <a id="&#x8FD4;&#x56DE;&#x503C;"></a>

无。

### 举例 <a id="&#x4E3E;&#x4F8B;"></a>

```text
uint8_t hash[32];
sha256_hard_calculate((uint8_t *)"abc", 3, hash);
```

## 例程 <a id="&#x4F8B;&#x7A0B;"></a>

### 进行一次计算 <a id="&#x8FDB;&#x884C;&#x4E00;&#x6B21;&#x8BA1;&#x7B97;"></a>

```text
sha256_context_t context;
sha256_init(&context, input_len);
sha256_update(&context, input, input_len);
sha256_final(&context, output);
```

或者可以直接调用 `sha256_hard_calculate` 函数

```text
sha256_hard_calculate(input, input_len, output);
```

### 进行分块计算 <a id="&#x8FDB;&#x884C;&#x5206;&#x5757;&#x8BA1;&#x7B97;"></a>

```text
sha256_context_t context;
sha256_init(&context, input_piece1_len + input_piece2_len);
sha256_update(&context, input_piece1, input_piece1_len);
sha256_update(&context, input_piece2, input_piece2_len);
sha256_final(&context, output);
```

