# 使Ubuntu-18.04支持休眠

[参考文章](https://fitzcarraldoblog.wordpress.com/2018/07/14/configuring-lubuntu-18-04-to-enable-hibernation-using-a-swap-file/)

安装好ubuntu后，休眠（hibernation）一般是不能用的，通常按了电源键后电脑将会自动关机。

下面是解决方法

## 1. 创建swapfile

根据你的电脑内存大小选择创建多大的swapfile。建议最低为内存大小的2/5。

```bash
sudo swapoff -a
sudo dd if=/dev/zero of=/swapfile bs=1024 count=4M
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapoff -a
sudo swapon /swapfile
```

创建完成后可通过下面任意一行命令检查状态

```bash
swapon -s
free -m
```



## 2.查找UUID

```bash
sudo blkid

# 我的是 /dev/nvme0n1p2: UUID="f406e523-b0bb-45e0-a159-96b32c70da0f" TYPE="ext4" PARTUUID="96f00fcb-af84-4865-920a-5ee25d564f01"

```

## 3.查找resume偏移量

```bash
sudo filefrag -v /swapfile

# 我的是 27165763
```

通常在第一行的physical_offset的第一个值

你也可以安装uswsusp来查看这个偏移量

```bash
sudo apt install uswsusp
sudo swap-offset /swapfile
```



## 4.更新/boot/grub/grub.cfg文件

```bash
sudo vim /etc/default/grub
```

用步骤2，3的参数修改下面的命令然后加到 `GRUB_CMDLINE_LINUX_DEFAULT` 这一行的最后。

示例：

```bash
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash resume=UUID=f406e523-b0bb-45e0-a159-96b32c70da0f resume_offset=27165763 resumedelay=5"
```

**注意**：`resumedelay=15` 参数是指定在尝试读取恢复文件之前暂停的延迟（以秒为单位）。我添加这个是为了让包含交换文件的文件系统有足够的时间成为读写文件。

完成后刷新文件

```bash
sudo update-grub
```



## 5.创建/etc/initramfs-tools/conf.d/resume文件

```bash
sudo vim /etc/initramfs-tools/conf.d/resume
```

继续用2，3得到的参数添加进去

```bash
resume=UUID=f406e523-b0bb-45e0-a159-96b32c70da0f resume_offset=27165763
```

刷新文件

```bash
sudo update-initramfs -u -k all
```



## 6.更新系统文件，允许睡眠



首先查看polkit版本

```bash
 
pkaction --version
```



#### 如果版本<0.106

新建文件

```bash
sudo vim /var/lib/polkit-1/localauthority/50-local.d/50-enable-suspend-on-lockscreen.pkla
```

添加以下

```bash
[Allow hibernation and suspending with lock screen]
Identity=unix-user:*
Action=org.freedesktop.login1.suspend;org.freedesktop.login1.suspend-multiple-sessions;org.freedesktop.login1.hibernate;org.freedesktop.login1.hibernate-multiple-sessions
ResultAny=yes
ResultInactive=yes
ResultActive=yes
```



#### 版本>= 0.106

新建文件

```bash
sudo vim /etc/polkit-1/rules.d/85-suspend.rules
```

添加以下

```bash
polkit.addRule(function(action, subject) {
    if (action.id == "org.freedesktop.login1.suspend" ||
        action.id == "org.freedesktop.login1.suspend-multiple-sessions" ||
        action.id == "org.freedesktop.login1.hibernate" ||
        action.id == "org.freedesktop.login1.hibernate-multiple-sessions")
    {
        return polkit.Result.YES;
    }
});
```

## 7. 重启

```bash
reboot
```

