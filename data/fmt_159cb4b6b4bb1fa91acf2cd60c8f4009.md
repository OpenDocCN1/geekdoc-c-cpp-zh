
```
_FloatN cbrtfFN(_Float x);
_FloatN cbrtfFX(_Float x);
_DecimalW cbrtdWN(_DecimalW x);
_DecimalW cbrtdNX(_DecimalW x);

_FloatN powfFN(_FloatN x, long int n);
_FloatN powfFX(_Float x, long int n);
_DecimalW powdN(_DecimalW x, long int n);
_DecimalW powdNX(_DecimalW x, long int n);

_FloatN fabsfFN(_Float x);
_FloatN fabsfFX(_Float x);
_DecimalW fabsdWN(_DecimalW x);
_DecimalW fabsdNX(_DecimalW x);

_FloatN hypotfFN(_Float x, _Float y);
_FloatN hypotfFX(_Float x, _Float y);
_DecimalW hypototDW(_DecimalW x, _DecimalW y);
_DecimalW hypototNX(_DecimalW x, _DecimalW y);

_FloatN powfFN(_Float x, _Float y);
_FloatN powfFX(_Float x, _Float y);
_DecimalW powdN(_DecimalW x, _DecimalW y);
_DecimalW powdNX(_DecimalW x, _DecimalW y);

_FloatN powfFN(_FloatN x, long int n);
_FloatN powfFX(_Float x, long int n);
_DecimalW powdN(_DecimalW x, long int n);
_DecimalW powdNX(_DecimalW x, long int n);

_FloatN powfFN(_Float x, _Float y);
_FloatN powfFX(_Float x, _Float y);
_DecimalW powdN(_DecimalW x, _DecimalW y);
_DecimalW powdNX(_DecimalW x, _DecimalW y);

_FloatN rootfFN(_Float x, long int n);
_FloatN rootfFX(_Float x, long int n);
_DecimalW rootdN(_DecimalW x, long int n);
_DecimalW rootdNX(_DecimalW x, long int n);

_FloatN rsqrtFN(_Float x);
_FloatN rsqrtFX(_Float x);
_DecimalW rsqtdWN(_DecimalW x);
```

# ISO/IEC 9899:2024(en)

```
_DecimalNx rsqrtdnNx(_DecimalNx x);
_FloatN sqrtfnN(_FloatN x);
_FloatNx sqrtfnNx(_FloatNx x);
_DecimalN sqrtdnN(_DecimalN x);
_DecimalNx rsqrtdnNx(_DecimalNx x);
```

## 12.10.9 误差与伽马函数

```
_FloatN erffN(_FloatN x);
_FloatNx erffNx(_FloatNx x);
_DecimalN erfdN(_DecimalN x);
_DecimalNx erfdNx(_DecimalNx x);

_FloatN erfcN(_FloatN x);
_FloatNx erfcNx(_FloatNx x);
_DecimalN ercdnN(_DecimalN x);
_DecimalNx ercdnNx(_DecimalNx x);

_FloatN lgammaf(_FloatN x);
_FloatNx lgammafx(_FloatNx x);
_DecimalN lgammadN(_DecimalN x);
_DecimalNx lgammadNx(_DecimalNx x);

_FloatN tgammaf(_FloatN x);
_FloatNx tgammafx(_FloatNx x);
_DecimalN tgammdnN(_DecimalN x);
_DecimalNx tgammdnNx(_DecimalNx x);
```

## 12.10.10 接近整数函数

```
_FloatN ceilf(_FloatN x);
_FloatNx ceilfNx(_FloatNx x);
_DecimalN ceildN(_DecimalN x);
_DecimalNx ceildNx(_DecimalNx x);

_FloatN floorf(_FloatN x);
_FloatNx floorfNx(_FloatNx x);
_DecimalN floordN(_DecimalN x);
_DecimalNx floordNx(_DecimalNx x);

_FloatN nearbyintN(_FloatN x);
_FloatNx nearbyintNx(_FloatNx x);
_DecimalN nearbyintN(_DecimalN x);
_DecimalNx nearbyintNx(_DecimalNx x);

_FloatN rintf(_FloatN x);
_FloatNx rintNx(_FloatNx x);
_DecimalN rintdN(_DecimalN x);
_DecimalNx rintNx(_DecimalNx x);

long int llrintf(_FloatN x);
long int llrintNx(_FloatNx x);
long int llrintdN(_DecimalN x);
long int llrintNx(_DecimalNx x);

long int llroundf(_FloatN x);
long int llroundNx(_FloatNx x);
long int llrounddN(_DecimalN x);
long int llroundNx(_DecimalNx x);

_Float roundN(_FloatN x);
_FloatNx roundNx(_FloatNx x);
_DecimalN rounddN(_DecimalN x);
_DecimalNx roundNx(_DecimalNx x);

long int roundff(_Float x);
long int roundfNx(_FloatNx x);
long int rounddd(_DecimalN x);
long int roundddx(_DecimalNx x);

long int llroundff(_Float x);
long int llroundfNx(_FloatNx x);
long int llrounddd(_DecimalN x);
long int llroundddx(_DecimalNx x);

_Float truncN(_FloatN x);
_FloatNx truncNx(_FloatNx x);
_DecimalN truncDN(_DecimalN x);
_DecimalNx truncNx(_DecimalNx x);

_Float truncfN(_FloatN x);
_FloatNx truncfNx(_FloatNx x);
_DecimalN truncdN(_DecimalN x);
_DecimalNx truncDNx(_DecimalNx x);

_Float fromfpN(_Float x, int width);
_FloatNx fromfpNx(_FloatNx x, int width);
_DecimalN fromfpdN(_DecimalN x, int width);
_DecimalNx fromfpDNx(_DecimalNx x, int width);
_Float ufromfpN(_Float x, int width);
_FloatNx ufromfpNx(_FloatNx x, int width);
_DecimalN ufromfpdN(_DecimalN x, int width);
_DecimalNx ufromfpDNx(_DecimalNx x, int width);

_Float frompxN(_Float x, int width);
_FloatNx frompxNx(_FloatNx x, int width);
_DecimalN frompxdN(_DecimalN x, int width);
_DecimalNx frompxDNx(_DecimalNx x, int width);
_Float ufrompxN(_Float x, int width);
_FloatNx ufrompxNx(_FloatNx x, int width);
_DecimalN ufrompxdN(_DecimalN x, int width);
_DecimalNx ufrompxDNx(_DecimalNx x, int width);
```

## 7.12.11.2 余数函数

```
_Float modffN(Float x, Float y);
_FloatN modffNx(Float x, Float y);
_DecimalN moddd(Decimal x, Decimal y);
_DecimalN modddx(Decimal x, Decimal y);

_Float remainffN(Float x, Float y);
_FloatN remainfNx(Float x, Float y);
_DecimalN remaindd(Decimal x, Decimal y);
_DecimalN remainddx(Decimal x, Decimal y);

_Float remquoffN(Float x, Float y, int *quo);
_FloatN remquoffNx(Float x, Float y, int *quo);
```

## 7.12.12 操作函数

```
_Float copysignN(Float x, Float y);

_FloatNx copysnx(_FloatNx x, _FloatNx y);
_DecimalNx copysvnd(_DecimalNx x, _DecimalNx y);
_DecimalNx copysndvx(_DecimalNx x, _DecimalNx y);

_FloatNx nanf(const char *tagp);
_FloatNx nanfnx(const char *tagp);
_DecimalNx nandv(const char *tagp);
_DecimalNx nandx(const char *tagp);

_FloatNx nextafter(_FloatNx x, _FloatNx y);
_FloatNx nextafterfnx(_FloatNx x, _FloatNx y);
_DecimalNx nextafterdv(_DecimalNx x, _DecimalNx y);
_DecimalNx nextafterdx(_DecimalNx x, _DecimalNx y);

_FloatNx nextup(_FloatNx x, _FloatNx y);
_FloatNx nextupfnx(_FloatNx x, _FloatNx y);
_DecimalNx nextupdv(_DecimalNx x, _DecimalNx y);
_DecimalNx nextupdx(_DecimalNx x, _DecimalNx y);

_FloatNx nextown(_FloatNx x, _FloatNx y);
_FloatNx nextownfnx(_FloatNx x, _FloatNx y);
_DecimalNx nextdowndv(_DecimalNx x, _DecimalNx y);
_DecimalNx nextdowndx(_DecimalNx x, _DecimalNx y);
```

## 12.10.13 最小与正差

```
_FloatNx dfmin(_FloatNx x, _FloatNx y);
_FloatNx dfminx(_FloatNx x, _FloatNx y);
_DecimalN dfindv(_DecimalN x, _DecimalN y);
_DecimalN dfindx(_DecimalN x, _DecimalN y);

_FloatNx fmin(_FloatNx x, _FloatNx y);
_FloatNx fminx(_FloatNx x, _FloatNx y);
_DecimalNx fmindv(_DecimalNx x, _DecimalNx y);
_DecimalNx fmindx(_DecimalNx x, _DecimalNx y);

_FloatNx fmax(_FloatNx x, _FloatNx y);
_FloatNx fmaxfnx(_FloatNx x, _FloatNx y);
_DecimalNx fmaxdv(_DecimalNx x, _DecimalNx y);
_DecimalNx fmaxdx(_DecimalNx x, _DecimalNx y);

_FloatNx fagn(_FloatNx x, _FloatNx y);
_FloatNx fagnfnx(_FloatNx x, _FloatNx y);
_DecimalNx fmagdv(_DecimalNx x, _DecimalNx y);
_DecimalNx fmagdx(_DecimalNx x, _DecimalNx y);

_FloatNx fminimum(_FloatNx x, _FloatNx y);
_FloatNx fminimumfnx(_FloatNx x, _FloatNx y);
_DecimalNx fminimumdv(_DecimalNx x, _DecimalNx y);
_DecimalNx fminimumdx(_DecimalNx x, _DecimalNx y);

_FloatNx fmaximum(_FloatNx x, _FloatNx y);
_FloatNx fmaximumfnx(_FloatNx x, _FloatNx y);
_DecimalNx fmaximumdv(_DecimalNx x, _DecimalNx y);
_DecimalNx fmaximumdx(_DecimalNx x, _DecimalNx y);
```

## 12.10.14 融合加法

## 12.10.15 舍入最近类型函数

```
_Float fminimum_numf(_Float x, _Float y);
_FloatNx fminimum_numfx(_Float x, _Float y);
_DecimalN fminimum_numd(_DecimalN x, _DecimalN y);
_DecimalNx fminimum_numxd(_DecimalN x, _DecimalN y);

_Float fmaximum_numf(_Float x, _Float y);
_FloatNx fmaximum_numfx(_Float x, _Float y);
_DecimalN fmaximum_numd(_DecimalN x, _DecimalN y);
_DecimalNx fmaximum_numxd(_DecimalN x, _DecimalN y);

_Float fminimum_numf(_Float x, _Float y);
_FloatNx fminimum_numfx(_Float x, _Float y);
_DecimalN fminimum_numd(_DecimalN x, _DecimalN y);
_DecimalNx fminimum_numxd(_DecimalN x, _DecimalN y);
```

_Float fadd(_Float x, _Float y); // M < N

_FloatNx faddx(_Float x, _Float y); // M < N

_Float faddff(_Float x, _Float y); // M < N

_FloatNx faddxff(_Float x, _Float y); // M < N

_Decimal_ fadd(_Decimal x, _Decimal y); // M < N

_DecimalNx faddxd(_Decimal x, _Decimal y); // M < N

_Float fsub(_Float x, _Float y); // M < N

_FloatNx fsubx(_Float x, _Float y); // M < N

_Float fsubff(_Float x, _Float y); // M < N

_FloatNx fsubxff(_Float x, _Float y); // M < N

_Decimal_ fsub(_Decimal x, _Decimal y); // M < N

_DecimalNx fsubxd(_Decimal x, _Decimal y); // M < N

_Float fmul(_Float x, _Float y); // M < N

_FloatNx fmulx(_Float x, _Float y); // M < N

_Float fmulff(_Float x, _Float y); // M < N

_FloatNx fmulxff(_Float x, _Float y); // M < N
