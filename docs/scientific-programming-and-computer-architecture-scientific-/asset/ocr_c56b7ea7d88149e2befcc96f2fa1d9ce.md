```
/*
for(int mc=0; mc < nmic; mc++){
  long shift = mc*n/nmic;
  long len = (mc+1)*n/nmic - mc*n/nmic; \
#pragma onload_transfer target(mic:mc) \
 nocopy(v[shift:len]:align(64) alloc_if(1) free_if(0))
}
```

In the body of the for-loop, the part of the array v[] allocated to the MIC device numbered begins with the entry v[shift] and ends with the entry v[shift+len-1]. The offload region here allocates corresponding memory on the MIC device. It has an empty body, and nothing is copied.
The crucial bit of syntax here is v[shift:len]. An array of len items is allocated on the MIC device. As before, the pointer v on the host corresponds to some other v on the MIC device inside the body of the offload region. Even in this setting, v[i] refers to the ith entry of v[] on the Phi as well as the host, but the legal values of the index i must be in the range shift <= i < shift + len. The copy of v[] on the Phi is again an image of v[] on the host, but only a segment of the original array is represented in the image.
The rest of the definition shows more instances of offload.

```
/*
* offload scaling and summing to mic devices
/
for(int mc=0; mc < nmic; mc++){
  long shift = mc*n/nmic;
  long len = (mc+1)*n/nmic - mc*n/nmic;
#pragma offload target(mic:mc) \
 in(v[shift:len]:alloc_if(0) free_if(0)) \
 out(sum[mc:1]) \
 signal(1)
{
  hostmic_scale(v+shift, len);
  hostmic_scale(v+shift, len)
```