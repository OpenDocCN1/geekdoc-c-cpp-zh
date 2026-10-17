
`return (new Complex(re, im));`

```cs
// 复数 z的复数反正弦

public static Complex CArcSin(Complex z)

{

  return (-i*Complex.Clog((i*z)+Complex.Sqrt(1.0-(z*z)));

}

```

```cs
// 复数 z的复数反正弦（版本 2）

public static Complex CArcSin2(Complex z)

{

  double x = z.real;

  double y = z.imag;

  double ysq = y*y;

  double rtpos = Math.Sqrt(Math.Pow(x+1.0,2.0)+ysq);

  double rtneg = Math.Sqrt(Math.Pow(x-1.0,2.0)+ysq);

  double alpha = 0.5*(rtpos-rtneg);

  double beta = 0.5*(rtpos+rtneg);

double InvSinZRe = Math.Asin(beta);

double InvSinZIm = Math.Sign(y) *

Math.Log(alpha + Math.Sqrt(alpha*alpha-1.0));

  return (new Complex(InvSinZRe, InvSinZIm));

}

```

```cs
// 复数 z的复数反余弦

public static Complex CArcCos(Complex z)

{

  return (-i*Complex.Clog(z+Complex.Sqrt(1.0-(z*z)));

}

```

```cs
// 复数 z的复数反余弦（版本 2）

public static Complex CArcCos2(Complex z)

{

  double x = z.real;

  double y = z.imag;

  double ysq = y*y;

  double rtpos = Math.Sqrt(Math.Pow(x+1.0,2.0)+ysq);

  double rtneg = Math.Sqrt(Math.Pow(x-1.0,2.0)+ysq);

  double alpha = 0.5*(rtpos-rtneg);

  double beta = 0.5*(rtpos+rtneg);

  double InvCosZRe = Math.Acos(beta);

  double InvCosZIm = -Math.Sign(y) *

Math.Log(alpha + Math.Sqrt(alpha*alpha-1.0));

  return (new Complex(InvCosZRe, InvCosZIm));

}

```

# 复数

```cs
// 复数 z的复数反正正切

public static Complex CArcTan(Complex z)

{

    return ((i/2.0)*Complex.CLog((i+z)/(i-z)));

}

// 复数 z的复数反正正切（版本 2）

public static Complex CArcTan2(Complex z)

{

    double x = z.real;

    double y = z.imag;

    double xsqd = x * x;

    double ysqd = y * y;

    double InvTanRe=0.5*Math.Atan(2.0*x,1.0-xsqd-ysqd);

    double InvTanIm=Math.Log((xsqd+Math.Pow(y-1.0,2.0)));

    return (new Complex(InvTanRe,InvTanIm));

}

// 复数 z的复数反余正切

public static Complex CArcCot(Complex z)

{

    return (Complex.CArcTan(1.0/z));

}

// 复数 z的复数反余正切（版本 2）

public static Complex CArcCot2(Complex z)

{

    return ((i/2.0)*Complex.CLog((z-i)/(z+i)));

}

// 复数 z的复数反正割

public static Complex CArcSec(Complex z)

{

    return (Complex.CArcos(1.0/z));

}

// 复数 z的复数反正割（版本 2）

public static Complex CArcSec2(Complex z)

{

    return (i*Complex.CLog((Complex.CSqrt(1.0-(z*z))+1.0)/z));

}

// 复数 z的复数反正割

public static Complex CArcCsc(Complex z)

{

    return (Complex.CArcSin(1.0/z));

}

// 复数 z的复数反正割（版本 2）

public static Complex CArcCsc2(Complex z)

{

    return (-i*Complex.CLog((Complex.CSqrt((z*z)-1.0)+i)/z));

}

```

```cs
// 复数 z的双曲正弦

public static Complex CSinh(Complex z)

{

    return ((Complex.CExp(z)-Complex.CExp(-z))/2.0);

}

// 复数 z的双曲正弦（版本 2）

public static Complex CSinh2(Complex z)

{

    double x = z.real;

    double y = z.imag;

    double SinhZRe = Math.Sinh(x)*Math.Cos(y);

    double SinhZIm = Math.Cos(x)*Math.Sin(y);

    return (new Complex(SinhZRe, SinhZIm));

}

// 复数 z的复数双曲正弦（版本 3）

public static Complex CSinh3(Complex z)

{

    return (-i*Complex.CSinh(i*z));

}

// z数 z的双曲余弦

public static Complex Cosh(Complex z)

{

    return ((..Exp((z)+ExpCExpExp(-))/2;

}

// 复数 z的双曲余弦（版本 2）

public static Complex Cosh2(Complex z)

{

    double x = z.real;

    double y = z.imag;

    double CoshZRe = Math.Cos(x)*Math.Cos(y);

    double.osh(x =..x(

    y (

    return(newosh(,oshoshosh,osh

Im));

}

// 复数 z的双曲余弦（版本 3）

public static Complex Cosh3(Complex z)

{

    return (Complex.CCosh(i*z));

}

// 复数 z的复数双曲正切

public static Complex CTanh(Complex z)

{

    return (Complex.CSinh(z)/Complex.Cosh(z));

}

// 复数 z的双数双曲正切（版本 2）

public static Complex CTanh2(Complex z)

{

    double twox = 2.0*z.real;

    double twoy = 2.0*z.imag;

    double denom = Math.Cosh(twox)+Math.Cos(twoy);

    double TanhRe = Math.Sinh(twox)/denom;

    double TanhIm = -Math.Sin(twoy)/denom;

    return (new Complex(TanhRe,TanhIm));

}

// 复数 z的复数双曲正切（版本 3）

public static Complex CTanh3(Complex z)

{

    double twox = 2.0*z.real;

    double twoy = 2.0*z.imag;

    double denom = Math.Coshosh(twox)-Math.Cos(twoy);

    double CothRe = Math.Sinh(twox)/denom;

    double CothIm = -Math.Sin(twoy)/denom;

    return (new Complex(CothRe,CothIm));

}

// 复数 z的双曲反余正正切

public static Complex CCoth(Complex z)

{

  return (Complex.Cosh(z)/Complex.CSinh(z));

}

// 复数 z的双曲反余正正切（版本 2）

public static Complex CCoth2(Complex z)

{

  return (Complex.Cosh(z)/Complex.CSinh(z));

}

// 复数 z的双曲反余正正切（版本 4）

public static Complex CCoth4(Complex z)

{

  return (i*Complex.CCot(i*z));

}

// 复数 z的双曲反正割

public static Complex CSech(Complex z)

{

  return (1.0/Complex.Cosh(z));

}

// 复数 z的双曲反正割（版本 2）

public static Complex CSech2(Complex z)

{

  return (1.0/Complex.Cosh2(z));

}

// 复数 z的双曲反正割（版本 3）

public static Complex CSech3(Complex z)

{

    double CosX = Math.Cos(z.real);

    double CosY = Math.Cos(z.imag);

    double SinhX = Math.Sinh(z.real);

    double SinY = Math.Sin(z.imag);

    double denom = CosY*CosY+SinY*SinhX;

    double CsechRe = (CosX*CosY)/denom;

    double CsechIm = -(SinhX*SinY)/denom;

    return new Complex(CsechRe, CsechIm);

}

// 复数 z的双曲反正割（版本 4）

public static Complex CSech4(Complex z)

{

    return (Complex.Csec(i*z));

}

// 复数 z的双曲反正割

public static Complex CCscch(Complex z)

{

    return (1.0/Complex.CSinh(z));

}

// 复数 z的双曲反正割（版本 2）

public static Complex CCscch2(Complex z)

{

    return (1.0/Complex.CSinh2(z));

}

// 复数 z的双曲反正割（版本 3）

public static Complex CCscch3(Complex z)

{

    double CosX = Math.Cos(z.real);

    double CosY = Math.Cos(z.imag);

    double SinhX = Math.Sinh(z.real);

    double SinY = Math.Sin(z.imag);

    double denom = CosY*CosY+SinY*SinhX;

    double CsechRe = (CosX*CosY)/denom;

    double CsechIm = -(SinhX*SinY)/denom;

    return new Complex(CsechRe, CsechIm);

}

// 复数 z的双曲反正割（版本 4）

public static Complex CCscch4(Complex z)

{

    return (i*Complex.CSch(z));

}

```

```cs
// 复数 z的双反曲正弦
public static Complex ARCSinh(Complex z)
{
    return (Complex.Clog(z+Complex.Sqrt(z*z)+1.0));
}

// 复数 z的双反曲正弦（版本 2）
public static Complex ARCSinh2(Complex z)
{
  double x = z.real;
  double y = z.imag;

  double xsq = x*x;
  double rtpos = Math.Sqrt(Math.Pow(y-1.0,2.0)+xsq);
  double rtneg = Math.Sqrt(Math.Pow(y+1.0,2.0)+xsq);
  double alphap = 0.5*(rtpos+rtneg);
  double betap = 0.5*(rtpos-rtneg);
  double InvSinhZRe = Math.Sign(x) *
Math.Log(alphap+Math.Sqrt(alphap*alphap-1.0));
  double InvSinhZIm = -Math.asin(betap);

  return (new Complex(InvSinhZRe, InvSinhZIm));
}

// 复数 z的双反曲余弦
public static Complex ARCCosh(Complex z)
{
    return (Complex.Clog(z+Complex.Sqrt(z*z-1.0)));
}

// 复数 z的双反曲余弦（版本 2）
public static Complex ARCCosh2(Complex z)
{
  double x = z.real;
  double y = z.imag;

  double ysq = y*y;
  double rtpos = Math.Sqrt(Math.Pow(x+1.0,2.0)+ysq);
  double rtneg = Math.Sqrt(Math.Pow(x-1.0,2.0)+ysq);
  double alpha = 0.5*(rtpos+rtneg);
  double beta = 0.5*(rtpos-rtneg);
  double InvCoshZRe = Math.Log(alpha+Math.Sqrt(alpha*alpha-1));
  double InvCoshZIm = Math.Sign(y)*Math.Acos(beta);

  return (new Complex(InvCoshZRe, InvCoshZIm));
}

// 复数 z的双反曲正切
public static Complex CARTanh(Complex z)
{
  return (0.5*Complex.Clog((1.0+z)/(1.0-z)));
}
```

# C# 中的数值方法、算法与工具

```csharp
// 复数 z 的反双曲正切 (ver 2)
public static Complex CarcTanh2(Complex z)
{
    double x = z.real;
    double y = z.imag;
    double xsqd = x*x;
    double ysqd = y*y;

    double InvTanhRe = 0.25 * Math.Log(ysqd + 
    Math.Pow(x+1.0,2.0)) / (ysqd+Math.Pow(x-1.0,2.0));

    double InvTanhIm = 0.5*Math.Atan2(2.0*y,1.0-xsqd-ysqd);

    return (new Complex(InvTanhRe,InvTanhIm));
}
```

```csharp
// 复数 z 的反双曲余angent
public static Complex CarcCoth(Complex z)
{
    return (Complex.CarcTanh(1.0/z));
}
```

```csharp
// 复数 z 的反双曲余切 (ver 2)
public static Complex CarcCoth2(Complex z)
{
    return (0.5 * Complex.CLog((z+1.0)/(z-1.0)));
}
```

```csharp
// 复数 z 的反双曲正割
public static Complex CarcSech(Complex z)
{
    return (Complex.CarcCosh(1.0/z));
}
```
