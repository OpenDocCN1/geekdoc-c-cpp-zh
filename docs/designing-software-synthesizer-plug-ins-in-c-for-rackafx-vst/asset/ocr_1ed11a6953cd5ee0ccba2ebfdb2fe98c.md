```
double CSEMFilter::doFilter(double xn)
{
    // return xn if filter not supported
    if(m_uFilterType != LPF2 && m_uFilterType != HPF2 &&
        m_uFilterType != BPF2 && m_uFilterType != BSF2)
        return xn;

    // form the HP output first
    double hpf = m_dAlpha0*(xn - m_dRho*m_dZ11 - m_dZ12);

    // BPF Out
    double bpf = m_dAlpha*hpf + m_dZ11;

    // for nonlinear proc --
    if(m_uNLP -- ON)
        bpf = tanh(m_dSaturation*bpf);

    // LPF Out
    double lpf = m_dAlpha*bpf + m_dZ12;

    // note R is the traditional analog damping factor
    double R = 1.0/(2.0*m_dQ);

    // BSF Out
    double bsf = xn - 2.0*R*bpf;

    // SEM BPF Out
    // using m_dAuxControl for this one-off control
    double semBSF = m_dAuxControl*hpf + (1.0 - m_dAuxControl)*lpf;

    // update memory
    m_dZ11 = m_dAlpha*hpf + bpf;
    m_dZ12 = m_dAlpha*bpf + lpf;
}
```

update()

+   - always call the base class method first