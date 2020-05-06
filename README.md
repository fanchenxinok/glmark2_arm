# glmark2_arm
移植glmark2跑分工具到arm板上。

(1) cd src/ 进入src目录
(2) 修改Makefile, 修改交叉编译工具gcc的环境变量“CROSS_COMPILER”，修改USR_INC为你的sysroot下的usr/include。
(3) 修改模式选择变量“MODULE_SELECT”，默认的跑分模式是drm-glesv2模式，现在wayland-glesv2模式跑起来有问题，如果你能将wayland-glesv2模式跑起来请告诉我，一起学习。
(4) make

运行效果如下：
![result1](https://github.com/fanchenxinok/glmark2_arm/blob/master/doc/result1.jpg)
![result2](https://github.com/fanchenxinok/glmark2_arm/blob/master/doc/result2.jpg)
