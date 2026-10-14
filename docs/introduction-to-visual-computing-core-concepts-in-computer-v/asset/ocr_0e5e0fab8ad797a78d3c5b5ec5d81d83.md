To achieve this, we have to map \(\frac{1}{n}\) to \(-1\), \(\frac{1}{f}\) to \(+1\), and the center of the range \([\frac{1}{n},\frac{1}{f}]\) to 0. The center is given by

$$\frac{\frac{1}{f}+\frac{1}{n}}{2}=\frac{f+n}{2nf}.$$  \tag{13.27}

This movement of the center is achieved by a translation by \(-\frac{f+n}{2nf}\). Then, the extent between \(\frac{1}{n}\) to \(\frac{1}{f}\) is scaled to 2 via a scale factor of

$$\frac{2}{\frac{1}{f}-\frac{1}{n}}=\frac{2nf}{n-f}.$$  \tag{13.28}

Therefore the final expression for the third coordinate of \(P_l\) is given by

$$\left(\frac{1}{Z_v}-\frac{f+n}{2nf}\right)\frac{2nf}{n-f}=\frac{2nf}{(n-f)Z_v}+\frac{f+n}{f-n}=\frac{\frac{2nf}{n-f}-\frac{n+f}{n-f}Z_v}{Z_v}.$$  \tag{13.29}

Therefore, \(P_l\) that we would like to achieve is given by

$$\begin{pmatrix}\frac{2X_vn}{Z_v(y-r_l)}-\frac{l+r}{r-l}\\\frac{2Y_vn}{Z_v(b-t)}-\frac{t+b}{t-b}\\\frac{Z_v(b-t)}{2nf}+\frac{n+f}{n-f}Z_v\\1\end{pmatrix}=\begin{pmatrix}\frac{2X_vn}{Z_v(y-r_l)}-\frac{l+r}{r-l}Z_v\\\frac{2Y_vn}{Z_v(b-t)}-\frac{t+b}{t-b}Z_v\\\frac{2nf}{n-f}+\frac{n+f}{n-f}Z_v\\Z_v\end{pmatrix}.$$  \tag{13.30}

This can be achieved by making \(D(n)\) into a matrix that depends on both \(n\) and \(f\) and is given by

$$D(n,f)=\begin{pmatrix}n&0&0&0\\0&n&0&0\\0&0&-\frac{n+f}{n-f}&\frac{2nf}{n-f}\\0&0&1&0\end{pmatrix}.$$  \tag{13.31}