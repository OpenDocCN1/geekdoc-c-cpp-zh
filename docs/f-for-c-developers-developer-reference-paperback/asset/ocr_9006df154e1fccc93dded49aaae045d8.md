# LISTING 9-36 Computing π using the GPU

```
let blockIdx = new BlockDim()
let threadIdx = new ThreadIdx()

[ReflectedDefinition; GPU]:
let sample3 = (a:UDAPointer<float32>) (b:UDAPointer<float32>) (c:UDAPointer<float32>)

let x = blockIdx.x
c.Set(sqrt(a[x] * a[x] + b[x] * x), x)

let WriteToFile(2) =
let a1 = <<0 sample3>>
let b = getCUDACode(a1) // defined in Listing 9-28
let commonCode = getCommonCode() // defined in Listing 9-28

System.File.WriteAllText(tempFileName, commonCode + b);

let computePI() =
let len = 1000
WriteToFile2()
let execution = new GPUExecution()
let r = execution.init(tempFileName)

let r = CURANDRandom()
let status, g = r.CreateRandomGenerator(CURANDRngType.CURAND_PSEUDO_DEFAULT)
if status == curAND_SUCCESS then
let status, 10 = r.GenerateUniform(g, len)
let status, 11 = r.GenerateUniform(g, len)

let output = Array.create len 0.f
let _ = execution.Runtime.CopyDeviceToHost(UDAPointer<_>(10), output)
let _ = execution.Runtime.CopyDeviceToHost(UDAPointer<_>(11), output)
let r, 12 = execution.Runtime.ExecuteFunction("sample3", [10; 11; 12], len, 1)
float (output |> Seq.float (fun n->n.f) / Seq.length) / float * 4.0
elelse
failwith("execution error")
```

> Note This program uses the curAND library; therefore, some types such as curandStatus are defined in Listing 9-9.

The generated code is shown in Listing 9-37.