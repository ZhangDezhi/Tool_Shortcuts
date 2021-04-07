
3是一个平铺式窗口管理器(tiling window manager),使用BSD开源协议开源，主要应用于Linux和BSD操作系统。

在i3中，一切命令均以`修饰键($mod)`开头，默认$mod为Alt键，为了避免热键冲突，推荐使用Window键。

目前流行的两款WM产品：awesome和i3，awesome风格十分具有科技感，配置自由，但需要一定的时间来学习。而i3WM对于大部份程序员来说上手快，使用方便

在 GNOME 显示管理器（GDM）屏幕，选择 i3 而不是 GNOME

```bash
# $HOME/.config/i3 

# Mod 键通常都会作为 i3 命令快捷键的发起键. win / alt
$mod + Enter	启动虚拟终端
$mod + A	焦点转义到父窗口上
$mod + S	堆叠布局
$mod + W	标签布局
$mod + E	默认布局
$mod + SpaceBar	焦点在平铺式／浮动式转换
$mod + D	启动 dmenu
$mod + H	水平分割窗口
$mod + V	垂直分割窗口
$mod + J	焦点往左窗口移
$mod + K	焦点往下窗口移
$mod + L	焦点往上窗口移
$mod + ;	焦点往右窗口移
$mod + Shift + Q	杀死当前窗口的进程
$mod + Shift + E	退出 i3
$mod + Shift + C	当场重新加载 i3config, 无需重启
$mod + Shift + R	重启 i3 （还重新加载了 i3config, 又没有退出过程）
$mod + Shift + J	窗口左移
$mod + Shift + K	窗口下移
$mod + Shift + L	窗口上移
$mod + Shift + :	窗口右移
$mod + Shift + SpaceBar	窗口在平铺式／浮动式转换

```
