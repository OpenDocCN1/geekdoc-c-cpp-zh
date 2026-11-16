```
NColor = 256;
colormap(gray(NColor));
STFT_min = min(min(STFT));
STFT_max = max(max(STFT));
STFT = (STFT - STFT_max) * NColor / (STFT_min - STFT_max);
time=(0:2048-N)/r;
freq = (0:Nb2-1) * r / N;
axes('position',[0.1 bot 0.8 bi])
image(time,freq,STFT')
axis([0 0.24 0 2000])
YTickmark = [0 500 1000 1500 2000];
set(gca,'YDir','normal','ytick',YTickmark)
hold on;
N = N * 2
bot = bot + 0.225;
clear STFT; clear time; clear freq;
end
set(gcf,'paperposition',[0 0.5 7.5 10])
```

# 4.14.2 Wigner-Ville Distribution

```
%
% PROGRAM wvd.m
%
```