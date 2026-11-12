

```cpp
CUDA_CALL(cudaMemcpyAsync(cipher_data_device, cipher_data_host,
size_of_cipher_data_in_bytes, cudaMemcpyHostToDevice, aes_async_stream));

CUDA_CALL(cudaMemcpyAsync(cipher_key_device, cipher_key_host,
size_of_cipher_key_size_in_bytes, cudaMemcpyHostToDevice, aes_async_stream));
```

请注意，新创建的流被用作每个调用中的最后一个参数。流参数是一个可选参数。然后我们需要将内核启动到正确的流中，我们同样通过指定流来实现。由于流参数实际上是第四个参数，我们需要将零作为第3个参数。第3个参数是内核将使用的动态共享内存的大小。由于我们没有使用动态分配的共享内存，我们将其设置为零。因此，

```cpp
AES_encrypt_gpu<<<num_blocks, num_threads>>> (cipher_data_device, cipher_key_device,
num_cipher_blocks, num_cipher_keys);
```

变为

```cpp
AES_encrypt_gpu<<<num_blocks, num_threads, 0, aes_async_stream>>> (cipher_data_device,
cipher_key_device, num_cipher_blocks, num_cipher_keys);
```

我们对拷贝回主机和停止计时器事件也做同样的处理。由于停止计时器事件位于内核的末尾，我们还需要确保等待此事件。

```cpp
CUDA_CALL(cudaEventSynchronize(stop_round_timer));
```

由于内核、拷贝和事件操作现在完全是异步的，因此至关重要的是，在内核实际完成之前，不得使用从内核返回的数据。在将最终内存拷贝回主机后忘记添加此类同步操作，往往是迁移到异步操作时导致失败的原因。

此更改有何帮助？运行测试程序显示，时间从1070 ms下降到仅940 ms，执行时间下降了12%以上。这确实非常显著，考虑到我们所做的只是移除CUDA驱动程序在使用流0时插入的隐式同步步骤。

## 我们如何与CPU进行比较

Intel为AVX指令集提供了一种名为AES-NI的特殊扩展。它基于对整个AES密钥状态和密钥扩展的128位宽处理。这相当于我们迄今为止用于内存加载/存储的u4类型。AES-NI对编码/解码和扩展密钥操作都提供了硬件支持。因此，让我们看看如何利用这一点。

Intel提供了一个AES-NI示例库，可从 http://software.intel.com/en-us/articles/download-the-intel-aesni-sample-library/ 获取。下载库后，需要对其进行构建，因为没有预编译的二进制库可供链接。这仍然是通过旧的命令行界面完成的。运行Microsoft Visual Studio的人需要运行命令 vcvars32.bat，该命令为命令行版本设置多个命令行环境变量。在实践中，这映射到 vsvars32.bat 文件，该文件实际设置环境变量。

库构建完成后，您需要将库搜索路径添加到Visual Studio项目中，并将包含搜索路径和库添加到其他库中。

Intel版本的AES与我们迄今开发的GPU版本有一个关键区别。AES的原始规范以列格式布局数据，因此A、B、C和D都位于同一列。Intel AES-NI期望将其转置，因此A、B、C和D都在同一行。AES-NI还由于Intel的字节顺序，要求内存中的字节顺序与我们当前的顺序相反。

因此，我们有两种选择：要么重构代码以匹配Intel AES-NI的顺序，要么对数据进行转换以将一种格式转换为另一种格式。为了允许在主机上直接比较内存块，我们将调整当前解决方案以匹配AES-NI格式。由于我们还需要AES-NI支持，我们将把所有未来开发转移到我们的Sandybridge-E（Core i7 3930 K @ 3.2 Ghz）平台，配备GTX470 GPU。因此，任何进一步的计时将不再与我们迄今为此开发所使用的基于Atom的ION系统可比。

此时我们应注意的另一个主要问题是，uint4类型在GPU上编码为x、y、z、w，而不是w、x、y、z。我们的GPU和CPU版本都给出了相同的错误答案，因为它们基于相同的错误代码。一旦我们理解了uint4类型相当奇怪的顺序（这通常是红、绿、蓝、Alpha表示，其中w是Alpha通道），这很容易纠正。显然，我们本应将CPU版本基于现有库，或者更早使用AES-NI库来检测此类问题。AES-NI代码非常简单，如下所示：

```cpp
void aes_encode_block_aes_ni(const u32 num_cipher_blocks,
                                     const u32 num_cipher_keys,
                                     const u8 * initial_keys,
                                     u8 * src_data_blocks,
                                     u8 * dest_data_blocks)
{
  // Encode the data blocks
  TIMER_T encode_key_time = get_time();

  // Encode using one or more blocks and single key
  intel_AES_enc128( (AES_NI_UCHAR *) src_data_blocks,
                    (AES_OUT UCHAR *) dest_data_blocks,
                    (AES_IN UCHAR *) initial_keys,
                    (AES_IN size_t) num_cipher_blocks );

  encode_key_time = (get_time() - encode_key_time);
  if (num_cipher_blocks > 1)
  {
    printf("\n\nEncrypting using AES-NI : %u blocks", num_cipher_blocks);
    printf("\n\nEncrypt Encode : %.3fms", encode_key_time);
  }
}
```

AES代码的接口需要是基于字节的接口。这里我们展示一些示例代码，用于基于单个密钥对单个数据块num_cipher_blocks进行编码。类似的代码集用于解码操作。

```cpp
void aes_decode_block_aes_ni(const u32 num_src_cipher_blocks,
                                     const u32 num_cipher_keys,
                                     const u8 * key,
const u8 * src_data_blocks,
    u8 * const dest_data_blocks)

{
// Decode one or more blocks using a single key
TIMER_T decode_key_time = get_time();
intel_AES_dec128 ( (AES_IN UCHAR *) src_data_blocks,
    (AES_OUT UCHAR *) dest_data_blocks,
    (AES_IN UCHAR *) key,
    (AES_IN size_t) num_src_cipher_blocks );
decode_key_time = (get_time() - decode_key_time);

if (num_src_cipher_blocks > 1) {
printf("\nDecrypting using AES-NI : %u blocks", num_src_cipher_blocks);
printf("\nDecrypt Decode : %.3fms", decode_key_time);
}
}
```

密钥扩展操作在此操作中是隐式的，因为我们传递一个仅16字节的未扩展密钥。但是，它在内部每个加密/解密阶段只执行一次。

我们将开发一个程序，生成一组四百万个随机数据块（约64 MB的数据），并使用单个密钥对其进行编码。然后我们将解码此数据并检查解码后的数据是否与原始数据相同。我们将运行AES-NI、串行和CUDA版本的这些操作，并交叉检查每个结果，以确保所有实现都一致。

一旦GPU和CPU版本与AES-NI库匹配，我们就能看到AES-NI指令集有多快了。在我们的Sandybridge-E系统上，基于软件的串行扩展密钥和解码块操作耗时3880 ms，而启用硬件的AES-NI版本仅耗时20 ms。相比之下，CUDA版本耗时103 ms（不包括与设备之间的任何传输时间）。事实上，向设备和从设备复制操作分别耗时27 ms和26 ms。鉴于我们使用GTX470作为测试设备，而不是Tesla，我们将无法同时重叠传入和传出传输，因为该设备只启用了一个内存传输引擎。因此，我们可能实现的绝对最佳情况是将内核执行时间完全隐藏在这些传输中的一个之后，从而有效地消除它。然而，要做到这一点，我们需要内核执行时间提高5倍。因此，让我们来看看修订后的解码内核，使其与AES-NI输出字节对字节兼容。

```cpp
#define AES_UB_DECODE u32
__host__ __device__ void AES_decrypt_4x_reg(const uint4 * const src_cipher_block,
    uint4 * const dest_cipher_block,
    KEY_T * const cipher_key)
{
// Read 4 x 32 bit values from data block as 128 bit read
uint4 key = *src_cipher_block;

// Store into four 32 bit registers
u32 w0 = key.x;
u32 w1 = key.y;
```

