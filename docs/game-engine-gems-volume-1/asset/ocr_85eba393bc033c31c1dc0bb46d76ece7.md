# 18.6 Implementation

The discussed algorithm is implemented as a fragment shader run in a deferred shading pass, as shown in Listing 18.1. For the sake of simplicity, we omitted parts related to interleaved sampling. The program receives the fragment position in texture space (wPos) and in 2D clipping space (hPos) as interpolants. By fetching from the texture map containing normal vectors and depth values (depthMapSampler) with the texture-space position, we obtain the camera-space normal vector and the depth value. The 2D clipping-space coordinates are also transformed back to camera space using the camera-space depth, which results in the shaded point s.

# Listing 18.1: This fragment shader implements the algorithm discussed in this gem.

```
float4 psAO(float2 wPos : TEXCOORD0, float2 hPos :
{
    wPos += pixelsize * 0.5; // Texture coordinates

    float3 N = tex2D(depthMapSampler, wPos).xyz; //
    float depth = tex2D(depthMapSampler, wPos).a; //

    // Compute camera-space position
    float4 pcamera = mul(float4(hPos, 0, 1), projMat
    pcamera.xyz /= pcamera.w;

    float3 s = pcamera.xyz * depth / pcamera.z; //

    float O = 0; // Enumerator of ambient occ
    float Denom = 0; // Denominator of ambient oc
    float3 I = 0; // Irradiance

    for (int sampleidx = 0; sampleidx < sampleCount;
{

```