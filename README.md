# daphuongtien
baitaplon
I. read and create Melody.wav

[X,fs] = audioread('thongtin.wav');
t = 0 : 1/fs : length(X)/fs-1/fs;
E = X(:,1);
B = E';
f1 = 440; % frequency (Hz)
f2 = 20 * f1;
f3 = 75 * f1;
A1 = 3; A2 = A1*2; A3 = A1*3; A4 = A1*4;
y1 = A1 * sin( 2 * pi * f1 * t  );
y2 = A2 * sin( 2 * pi * f2 * t  );
y3 = A3 * sin( 2 * pi * f3 * t );
B1 = B.*y1;
B2 = B.*y2;
B3 = B.*y3;
H=[B B1 B2 B3];
soundsc( H, fs );

filename = 'Melody.wav';
audiowrite(filename,H,fs);

2. FFT Transform
K = fft(H);
plot(abs(K))
3. Spectrogram
win = 128 ;% window length in samples
% number of samples between overlapping windows:
hop = win/2;
nfft = win; % width of each frequency bin
spectrogram(H,win,hop,nfft,fs,'yaxis');
% change the tick labels of the graph from scientific notation to floating point:
yt = get(gca,'YTick');
set(gca,'YTickLabel', sprintf('%.0f|',yt));
