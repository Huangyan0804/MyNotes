## ubuntu下创建Desktop桌面启动器教程

---

[toc]

---

###  语法

| 关键词          | 意义     |
| --------------- | -------- |
| [Desktop Entry] | 文件头   |
|Encoding	| 编码 |
| Type    | 启动器类型 |
| Name            | 应用名称 |
|Name[xx]	 |不同语言的应用名称|
|Comment	|描述|
|Exec	|执行的命令|
|Icon	|图标路径|
|Terminal |	是否使用终端|
|Categories |	应用的类型（内容相关）|

---

## 例子

以Firefox为例，创建的文件内容如下:

```
[Desktop Entry]
Encoding=UTF-8
Type=Application
Name=Firefox
Comment=good browser
Exec=sh /opt/firefox/firefox.sh
Icon = /opt/firefox/firefox.svg
Terminal=false
Categories=Application;Network;
```

---

### 使用流程

1. 创建文件，以.desktop为后缀
2. 编写内容，修改权限
3. 测试是否能双击启动程序 
4.  移动到/usr/share/applications/目录下

> 注意：文件中不能有多余的空格，否则会出错