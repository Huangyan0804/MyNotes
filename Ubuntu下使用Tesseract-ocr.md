# Ubuntu下使用Tesseract-ocr

---



## 安装

[官方WiKi说明](https://tesseract-ocr.github.io/)

[Github下载地址（含训练集）](https://github.com/tesseract-ocr)



## 使用jTessBoxEditor训练

[训练教程1](https://blog.csdn.net/weixin_39497322/article/details/83626583)

[训练教程2](https://www.cnblogs.com/xpwi/p/9604567.html)



## 使用



```


-psm pagesegmode 也是一个可选参数默认值为3  不同的值用来说明待识别图片 提高识别率，不同值的含义如下：

0 =只进行定向和脚本检测（OSD）

1 =通过OSD进行页面自动分割

2 =自动分割，但没有OSD，或OCR

3 =全自动分割，但没有OSD（默认）

4 =假设待识别图片是一列的文本

5 =假设待识别图片是一个统一的垂直对齐的文本块

6 =假设待识别图片是一个统一的文本块

7 =把图像作为一个单一的文本行

8 =把图像当作一个字

9 =把图像作为一个字在一个圆圈中

10 =把图像当作一个单独的字符

11    Sparse text. Find as much text as possible in no particular order.

12    Sparse text with OSD.

13    Raw line. Treat the image as a single text line,
		bypassing hacks that are Tesseract-specific.
```



