针对目前linux的鼠标和触摸板的驱动。

当我在一次更新后，我的dwm中的鼠标和触摸板滚动不是反向的，让我突然感到难受，在经过一系列的查询后恢复成功。

已从之前的更换成了目前X11的libinput，所有设置将在这里编写

> /usr/share/X11/xorg.conf.d/

> /etc/X11/xorg.conf.d/40-libinput.conf 目前大家所使用的。</br>
> /etc/X11/xorg.conf.d/70-synaptics.conf 之前使用的，已停止维护，若要启动查看其对应文档



我目前的配置

```c
# Match on all types of devices but joysticks
#
# If you want to configure your devices, do not copy this file.
# Instead, use a config snippet that contains something like this:
#
# Section "InputClass"
#   Identifier "something or other"
#   MatchDriver "libinput"
#
#   MatchIsTouchpad "on"
#   ... other Match directives ...
#   Option "someoption" "value"
# EndSection
#
# This applies the option any libinput device also matched by the other
# directives. See the xorg.conf(5) man page for more info on
# matching devices.

Section "InputClass"
        Identifier "libinput pointer catchall"
        MatchIsPointer "on"
        MatchDevicePath "/dev/input/event*"
        Driver "libinput"
        Option "ScrollMethod" "twofinger"
        #Option "NaturalScrolling" "False"
EndSection

Section "InputClass"
        Identifier "libinput keyboard catchall"
        MatchIsKeyboard "on"
        MatchDevicePath "/dev/input/event*"
        Driver "libinput"
EndSection

Section "InputClass"
        Identifier "libinput touchpad catchall"
        MatchIsTouchpad "on"
        MatchDevicePath "/dev/input/event*"
        Driver "libinput"

        Option "VertTwoFingerScroll" "true"
        Option "VertTwoFingerScroll" "true"
        Option "VertScrollDelta" "-111"
        Option "HorizScrollDelta" "-111"
        Option "TapButton1" "1"            #单指敲击产生左键事件
        Option "TapButton2" "2"            #双指敲击产生中键事件
        Option "TapButton3" "3"            #三指敲击产生右键事件
        Option "VertEdgeScroll" "on"       #滚动操作：横向、纵向、环形
        Option "NaturalScrolling" "true"
        Option "VertTwoFingerScroll" "on"
        Option "HorizEdgeScroll" "on"
        Option "HorizTwoFingerScroll" "on"
        Option "CircularScrolling" "on"
        Option "CircScrollTrigger" "2"

        Option "EmulateTwoFingerMinZ" "40" #精确度
        Option "EmulateTwoFingerMinW" "8"
        Option "CoastingSpeed" "20"        #触发快速滚动的滚动速度

        Option "PalmDetect" "1"            #避免手掌触发触摸板
        Option "PalmMinWidth" "3"          #认定为手掌的最小宽度
        Option "PalmMinZ" "200"            #认定为手掌的最小压力值



EndSection

Section "InputClass"
        Identifier "libinput touchscreen catchall"
        MatchIsTouchscreen "on"
        MatchDevicePath "/dev/input/event*"
        Driver "libinput"
EndSection

Section "InputClass"
        Identifier "libinput tablet catchall"
        MatchIsTablet "on"
        MatchDevicePath "/dev/input/event*"
        Driver "libinput"
EndSection
```
