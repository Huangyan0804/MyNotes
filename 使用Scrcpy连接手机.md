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

**需要手机开启USB调试模式**

用数据线连接手机，然后执行

```bash
scrcpy
```

可以添加一些参数，详情见

```bash
scrcpy --help
```



## 启动命令

---

|         |   Scrcpy 的命令参数 |
| --------------------------- | :----------------------------------------------------------- |
| **关闭手机屏幕**            | `scrcpy -S`                                                  |
| **限制画面分辨率**          | `scrcpy -m 1024` (比如限制为 1024)                           |
| **修改视频码率**            | `scrcpy -b 4M` (默认 8Mbps，改成 4Mbps)                      |
| **裁剪画面**                | `scrcpy -c 1224:1440:0:0` 表示分辨率 1224x1440 并且偏移坐标为 (0,0) |
| **多设备切换**              | `scrcpy -s 设备ID` (使用 `adb devices` 命令查看设备ID)       |
| **窗口置顶**                | `scrcpy -T`                                                  |
| **显示触摸点击**            | `scrcpy -t` 在演示或录制教程时，可在画面上对应显示出点击动作 |
| **全屏显示**                | `scrcpy -f`                                                  |
| **文件传输默认路径**        | `scrcpy --push-target /你的/目录` 将文件拖放到 scrcpy 可以传输文件，此命令指定默认保存目录 |
| **只读模式(仅显示不控制)**  | `scrcpy -n`                                                  |
| **屏幕录像**                | `scrcpy -r 视频文件名.mp4` 或 `.mkv`                         |
| **屏幕录像 (禁用电脑显示)** | `scrcpy -Nr 文件名.mkv`                                      |
| **设置窗口标题**            | `scrcpy --window-title 'your title'`             |
| **同步传输声音** | 可借助 [USBaudio](https://github.com/rom1v/usbaudio) 这个开源项目实现，但仅支持 [Linux](https://www.iplaysoft.com/os/linux-platform) 系统 |



### 截图

```bash
#  截图（保存到SDCard）
adb shell /system/bin/screencap -p /sdcard/screenshot.png

# 从SD卡导出到电脑，注意：电脑路径必须存在
adb pull /sdcard/screenshot.png  ./  #（保存到电脑当前路径）

#如果你想删除手机上的图片，那么你可以使用这个命令来删除
adb shell rm /sdcard/screenshot.png
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
7. 重新启动`scrcpy`

> 如需切换回 USB 模式，执行：`adb usb`
>
> 如果 WiFi 较慢，可以调整码率：`scrcpy -b 3M -m 800`，意思是限制 3 Mbps，画面分辨率限制 800，数值可以随意调整。



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

| Scrcpy 快捷键列表              |                            |
| :----------------------------- | -------------------------- |
| 切换全屏模式                   | `Ctrl`+`F`                 |
| 将窗口调整为1：1（完美像素）   | `Ctrl`+`G`                 |
| 调整窗口大小以删除黑色边框     | `Ctrl`+`X` \| 双击黑色背景 |
| 设备 `HOME` 键                 | `Ctrl`+`H` \| 鼠标中键     |
| 设备 `BACK` 键                 | `Ctrl`+`B` \| 鼠标右键     |
| 设备 `任务管理` 键 (切换APP)   | `Ctrl`+`S`                 |
| 设备 `菜单` 键                 | `Ctrl`+`M`                 |
| 设备`音量+`键                  | `Ctrl`+`↑`                 |
| 设备`音量-`键                  | `Ctrl`+`↓`                 |
| 设备`电源键`                   | `Ctrl`+`P`                 |
| 点亮手机屏幕                   | 鼠标右键                   |
| 关闭屏幕显示                       | `Ctrl`+`O`                   |
| 旋转屏幕                           | `Ctrl`+`R`                   |
| 展开通知栏                         | `Ctrl`+`N`                   |
| 折叠通知栏                         | `Ctrl`+`Shift`+`N`           |
| 复制内容到设备                 | `Ctrl`+`V`                |
| 启用/禁用 FPS 计数器（stdout） | `Ctrl`+`I`                |
| 安装APK                        | 将 apk 文件拖入投屏        |
| 传输文件到设备                 | 将文件拖入投屏（非apk）    |
