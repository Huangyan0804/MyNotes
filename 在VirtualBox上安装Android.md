# 在VirtualBox上安装Android



这种搭配可能是性能低的笔记本上最好的选择了。



首先安装VirtualBox -> [Downloads](https://www.virtualbox.org/wiki/Downloads)

然后准备Android的iso文件 -> [Downloads](https://www.android-x86.org/download)



安装完成后打开 `VirtualBox`，点击新建。

然后设置相应的信息，注意文件夹就是虚拟机文件存放位置。

类型选`Linux`，版本选`Other Linux`，至于是`32位`还是`64位`，就看你下载的`iso`是多少位的了。

然后分配内存，自己酌情考虑。

然后选择`现在创建虚拟硬盘`，选择VDI；点击下一步，选择动态分配

根据实际情况来配置虚拟硬盘的大小，硬盘空间大的请随意，然后点击创建。

找到我们刚才创建好的`Android_test`，点击设置。

然后点击显示-调整显存大小-启用硬件加速里面的3D加速。

选择存储-点击盘片-分配一个光驱，就是把你下载的`Android-X86`的`iso`添加进去。然后点击ok。



双击我们创建好的虚拟机。

选择`Advanced options...`

选择`Auto_Installation`

选择yes！

选择Reboot以重启。

然后我们将其强制退出！

然后在设置里面，把iso的盘片移除，免得开机时加载盘片去了。然后再重新双击启动！

然后选择`Android-x86 8.1-r2`，千万别手贱按了回车，通过下面的帮助信息得知，我们要按下`E键`，进入编辑页面.

然后在`kernel`哪里，同样的按下`E键`，进入编辑页面

移动光标，找到图中的`quiet`这个词。

把`quiet`改为`nomodeset xforcevesa`，然后按下回车键，再按下键盘上的`B键`。

然后你就会看到Android的字母了，慢慢等待即可！后面的就不说了，等到了“开机”，应该就自己会玩了，跟用手机也区别不大！