@[TOC](MATLAB图片的色彩转换)
## 一、需求分析
从电脑上读取一张彩色图像，通过独立编程（不使用已有函数）
	①实现将彩色图像转换为灰度图像、黑白图像的功能；
	②实现将图像整体呈现效果为偏绿色风格；
	③并将原始图像、灰度图像、黑白图像、绿色滤镜图像展示在同一个图像			   窗口内。
	每个子图要有相应的图名，最终呈现效果参考如图。
## 二、算法分析
1.彩色图像转换为灰度图像公式：==Y=0.299*R+0.587*G+0.114*B==
2.彩色图像转换为黑白图像公式：

 - ==$X=\frac{R+G+B}{3}$==
 - ==$c(u)=\begin{cases} 1，X\geq125\\ 0， X<125\end{cases}$== 
 
3.加绿色滤镜思路：将彩色图像的G通道值整体变大一定数值即可。
4.将图像读取后视作图像矩阵，对图像的操作即为对图像矩阵中每个元素进行操作，采用遍历每个元素操作的方法。
## 三、实验代码

```python
clear
clc
% 读入图像
img = imread('敖丙.jpg');

%分离r,g,b通道
R = img(:,:,1);
G = img(:,:,2);
B = img(:,:,3);

%创建一个新的窗口
figure;
subplot(2,2,1),imshow(img),title('原图');

subplot(2,2,2),Gray_img = 0.299*R+0.587*G+0.114*B,imshow(Gray_img),title('灰度图');
imwrite(Gray_img,'C:\Users\25392\Desktop\灰色敖丙.jpg');

subplot(2,2,3);
Gray_img = imread('灰色敖丙.jpg');
[m,n,t]=size(Gray_img);
alpha=125; %阈值
for i=1:m
    for j=1:n
       for k=1:t
            if Gray_img(i,j,k)>=alpha
                imbw(i,j,k)=1;
            else
                imbw(i,j,k)=0;
            end  
       end
    end
end
imshow(imbw)
title('二值图')

subplot(2,2,4);
Green_img(:,:,1)=R;
Green_img(:,:,2)=1.5*G;%图像的绿色分量加大
Green_img(:,:,3)=B; 
imshow(Green_img)
title('绿色滤镜');

```
## 四、实验结果
![因为喜欢敖丙就选了这张图](https://img-blog.csdnimg.cn/20210103132255246.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NDczMzMw,size_16,color_FFFFFF,t_70#pic_center)
## 五、心得体会
 对于这次期末作业，我个人感觉对自己的能力有所提升。
处理图片这个项目，其实难度不大。将彩图制成灰度图片直接用Y=0.299*R+0.587*G+0.114*B即可，给图片加绿色滤镜也挺简单的，直接把彩色图像的G通道值变大些就好了。
唯一让我觉得有难度的是彩色图转成黑白二值图。最开始我想把RGB相加再除以3但遇到了一个问题，RGB相加时超过255的话会全变成255，导致输出的图片一片黑。
还有就是彩色图转成黑白二值图时，应该先把彩色图片转成灰度图片以及在写MATLAB程序时，在最开始的地方要养成写clear和clc的习惯。
最后，非常感谢尹宽老师的倾情授课，让我收获了许多知识！
## 六、致谢
非常感谢[微博用户](http://blog.sina.com.cn/s/blog_6935ad190101cuax.html)提供不用==im2bw函数==将图片转换成二值图的方法！



