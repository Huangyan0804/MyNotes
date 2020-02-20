# Ubuntu下使用Tesseract-ocr

---



## 安装

[官方WiKi说明](https://tesseract-ocr.github.io/)

[Github下载地址（含训练集）](https://github.com/tesseract-ocr)



## 使用jTessBoxEditor训练

[训练教程1](https://blog.csdn.net/weixin_39497322/article/details/83626583)

[训练教程2](https://www.cnblogs.com/xpwi/p/9604567.html)

准备好样本图片，merge成test.tif

生成BOX文件, 打开在  test.tif  文件目录下打开终端，执行  

```bash
tesseract test.tif test makebox
```

在命令行执行:**echo font 0 0 0 0 0 >font_properties**   注意 font 是值创建 字体的名字，下面合并训练文件时 会用到。
结果生成了font_properties文件 

生成.tr训练文件,在命令行执行: 

```bash
tesseract test.tif test -l eng -psm 7 nobatch box.train
```

生成字符集文件 

在命令行执行 : 

```bash
unicharset_extractor test.box 
```

生成shape文件

 在命令行执行 : 

```bash
shapeclustering -F font_properties -U unicharset -O test.unicharset test.tr
```

生成聚集字符特征文件 

在命令行执行: 

```bash
mftraining -F font_properties -U unicharset -O test.unicharset test.tr 
```

生成字符正常化特征文件 
在命令行执行: 

```bash
cntraining test.tr 
```

生成的文件用 mv 命令进行更名

```bash
mv normproto test.normproto  
mv inttemp test.inttemp
mv pffmtable test.pffmtable  
mv unicharset test.unicharset  
mv shapetable test.shapetable
```

合并训练文件 
在命令行执行: 

```bash
combine_tessdata test.
```

**将fontyp.traineddata文件拷贝至Tesseract-OCR文件夹里的tessdata语言包文件夹里**

```bash
mv test.traineddata test1.traineddata 
sudo cp test1.traineddata /usr/share/tesseract-ocr/4.00/tessdata/
sudo cp test1.traineddata ../jTessBoxEditor/tesseract-ocr/tessdata/

```



## 将图片灰度，二值化

```python
img_grey = img.convert("L")
# 将颜色转成灰度
```

```python
img_two = img_grey.point(lambda x: 255 if x > 100 else 0)
# x 是颜色的中间值
```







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

## 



# 1123456





