# 使用Scrcpy连接手机



## 安装

```bash
sudo apt install scrcpy
```

为了可以使用WiFi连接，建议安装adb

```bash
sudo apt install adb
```



## 运行

---

用数据线连接手机，然后执行

```bash
scrcpy
```

可以添加一些参数，详情见

```bash
scrcpy --help
```



## 功能

---

### 捕获配置

#### 减少分辨率

需要减少屏幕分辨率来提升性能时，添加以下参数(以1024大小为例)：

```bash
scrcpy --max-size 1024
scrcpy -m 1024  # 简写
```

通常只填写一个值来保留宽高比

#### 更改图像比特率

默认的比特率是8 Mbps，以下是改成2 Mbps：

```bash
scrcpy --bit-rate 2M
scrcpy -b 2M  # 简写
```

#### 限制帧速 

一般安卓手机的帧速是 >= 10，可以这么更改：

```bash
scrcpy --max-fps 15
```

#### 裁剪

```bash
scrcpy --crop 1224:1440:0:0   # 从 (0,0) 裁剪到 (1224, 1440)
```

### 录屏

```bash
scrcpy --record file.mp4  # 录制到file.mp4
scrcpy -r file.mkv  # 简写
```

如果只想录屏而不显示：

```bash
scrcpy --no-display --record file.mp4
scrcpy -Nr file.mkv
# 用 Ctrl+C 结束
# Windows 上不能用 Ctrl+C 结束，只能断开连接结束录屏 
```



### 连接

#### 无线连接

使用`adb`连接手机：

1. 确保手机和电脑在同一个WiFi下
2. 用数据线将手机连接电脑
3. 获取你的手机IP地址`adb shell ip addr show wlan0`
4. 使用adb在手机上开启端口：`adb tcpip 5555`
5. 拔下手机与电脑的连接线
6. 连接你的手机：`adb connnect your_ip:5555` (用你的手机ip替换your_ip)
7. 运行`scrcpy`

**建议降低分辨率提升性能**



### 按键控制

#### 旋转屏幕

`Ctrl` + `r`

#### 复制粘贴

`Ctrl` + `c` 复制手机剪贴板到电脑剪贴板

`Ctrl` + `Shift` + `v` 将电脑剪贴板粘贴到手机剪贴板

`Ctrl` + `v` 将电脑剪贴板作为文字粘贴到手机



### 复制文件

直接拖拽，会自动复制到/sdcard/下

可在开始使通过命令切换目录

```
scrcpy --push-target /sdcard/your_folder
```





### 快捷键

| Action                             | Shortcut                      | Shortcut (macOS)             |
| ---------------------------------- | ----------------------------- | ---------------------------- |
| 全屏模式                           | `Ctrl`+`f`                    | `Cmd`+`f`                    |
| 将窗口调整为1：1                   | `Ctrl`+`g`                    | `Cmd`+`g`                    |
| 调整窗口大小以删除黑色边框         | `Ctrl`+`x` \| *Double-click¹* | `Cmd`+`x` \| *Double-click¹* |
| 点击主界面                         | `Ctrl`+`h` \| *Middle-click*  | `Ctrl`+`h` \| *Middle-click* |
| 点击返回                           | `Ctrl`+`b` \| *Right-click²*  | `Cmd`+`b` \| *Right-click²*  |
| 点击选择应用                       | `Ctrl`+`s`                    | `Cmd`+`s`                    |
| 点击菜单                           | `Ctrl`+`m`                    | `Ctrl`+`m`                   |
| 点击音量+                          | `Ctrl`+`↑` *(up)*             | `Cmd`+`↑` *(up)*             |
| 点击音量-                          | `Ctrl`+`↓` *(down)*           | `Cmd`+`↓` *(down)*           |
| 点击电源键                         | `Ctrl`+`p`                    | `Cmd`+`p`                    |
| 亮屏                               | *Right-click²*                | *Right-click²*               |
| 关闭屏幕显示                       | `Ctrl`+`o`                    | `Cmd`+`o`                    |
| 旋转屏幕                           | `Ctrl`+`r`                    | `Cmd`+`r`                    |
| 展开通知栏                         | `Ctrl`+`n`                    | `Cmd`+`n`                    |
| 折叠通知栏                         | `Ctrl`+`Shift`+`n`            | `Cmd`+`Shift`+`n`            |
| Copy device clipboard to computer  | `Ctrl`+`c`                    | `Cmd`+`c`                    |
| Paste computer clipboard to device | `Ctrl`+`v`                    | `Cmd`+`v`                    |
| Copy computer clipboard to device  | `Ctrl`+`Shift`+`v`            | `Cmd`+`Shift`+`v`            |
| 启用/禁用FPS计数器                 | `Ctrl`+`i`                    | `Cmd`+`i`                    |

*¹双击黑色边框来移除它们*
*²如果屏幕关着，右键双击来打开，否则等于按下返回键*