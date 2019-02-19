# image-filtering-using-octave
this has two filtering techniques related to guassian, and salt and pepper noise
clc;
clear all;
close all;
I=imread(&#39;C:\Users\admin\Desktop\Lena.tif&#39;);
[r,c]=size(I)
I_noise=imnoise(I, &quot;salt and pepper&quot;,0.05);
I_g=imnoise(I,&quot;gaussian&quot;,0,0.002);

avgI=I;
medI=I;

#averaging filter
for i=2:(r-1)
for j=2:(c-1)
Wavg=[I_noise(i-1,j-1) I_noise(i-1,j) I_noise(i-1,j+1) I_noise(i,j-1) I_noise(i,j) I_noise(i,j+1) I_noise(i+1,j-1)
I_noise(i+1,j) I_noise(i+1,j+1)];
y=sum(Wavg);
avg=y/9;
avgI(i,j)=avg;
endfor
endfor

#median filter
for i=1:r
for j=2:(c-1)

Wmed=[I_noise(i,j-1) I_noise(i,j) I_noise(i,j+1) ];
y=median(Wmed);
medI(i,j)=y;
endfor
endfor

avgI_g=I;
medI_g=I;

#averaging filter
for i=2:(r-1)
for j=2:(c-1)
Wavg_g=[I_g(i-1,j-1) I_g(i-1,j) I_g(i-1,j+1) I_g(i,j-1) I_g(i,j) I_g(i,j+1) I_g(i+1,j-1) I_g(i+1,j) I_g(i+1,j+1)];
y_g=sum(Wavg_g);
avg_g=y_g/9;
avgI_g(i,j)=avg_g;
endfor
endfor

#median filter
for i=1:r
for j=2:(c-1)
Wmed_g=[I_g(i,j-1) I_g(i,j) I_g(i,j+1) ];
ymed_g=median(Wmed_g);
medI_g(i,j)=ymed_g;
endfor
endfor

figure

subplot(1,3,1);
imshow(I);
title(&#39;original image&#39;);
subplot(1,3,2);
imshow(I_noise);
title(&#39;image added with salt-pepper noise&#39;);
subplot(1,3,3);
imshow(I_g);
title(&#39;image added with gaussian noise&#39;);

figure
subplot(1,3,1);
imshow(I_noise);
subplot(1,3,2);
imshow(avgI);
title(&#39;with averaging filter&#39;);
subplot(1,3,3);
imshow(medI);
title(&#39;with median filter&#39;);

figure
subplot(1,3,1);
imshow(I_g);
subplot(1,3,2);
imshow(avgI_g);
title(&#39;with averaging filter&#39;);
subplot(1,3,3);
imshow(medI_g);
title(&#39;with the median filter&#39;)
