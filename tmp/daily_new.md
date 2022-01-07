+ TODO: 我的一次系统拯救  <09-12-21, Redari-Es> + 
##

于2021-12-09 01:31 修复成功，迫不及待的开始记录下来
12月八日晚,正要写代码验证我的想法的时候，启动电脑，系统突然引导不了，停在了grub界面，且显示了/boot/vmlinuz-linux not found!的错误导致我的boot引导不出来。
试了半天，我从之前就做好的启动盘，启动个live，查看了boot, 发现有这个文件，打开后也没有啥特别的。随既就复制到了我的硬盘里的同个文件。reboot！

但结果任是不行，开始新的报错，/boot/initramfs-linux.img not found!
去查了下这是什么东西，简单认识了是一个内存镜像brabra的，之后修改
查了需要对当前的系统来制作的，用mkinit来制作一份，但制作的却是live系统的，想了半天，而且由于我的Artix，查了下，arch系的是mkinitcpio，这是自己补全出来的，挺幸运的。
后面想到了chroot方法，来隔离这个live系统，让我自己的系统成为根目录，这就行了，所以我就

> artix-chroot /run/media/xxx/xxxx/ (artix更改了chroot，每个系统可能不同)

试了之后是系统内核低了，live的是linux-5.13的，而最新的已经是5.15了，原来是因为我大半年每更新，前天更了一半就忙别的东西导致的呀，汗！

随即就是先进入bash里再pacman -S linux 更新下内核就可以了，它会自动帮你制作出initramfs-linux.img

不过根据这次的经验我又学到了东西。


