# glmark2_arm
移植glmark2跑分工具到arm板上。

(1) cd src/

(2) modify Makefile, change the CROSS_COMPILER to your cross compiler and your USR_INC( usr/include) dir in your sysroot. 

(3) modify MODULE_SELECT, default is drm-glesv2 module, just this module can work now, if you can run wayland-glesv2 module on

    your arm board, please tell me.

(4) make

运行效果如下：
![result1](https://github.com/fanchenxinok/glmark2_arm/blob/master/doc/result1.jpg)
![result2](https://github.com/fanchenxinok/glmark2_arm/blob/master/doc/result2.jpg)
