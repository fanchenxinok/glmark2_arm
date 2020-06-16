# glmark2_arm
glmark2 is GPU test tool run on Windows or Linux x86 platform, so i create this repository for ARM platform GPU test base on glmark2.

# how to cross-compile glmark2_arm
(1) cd src/  
(2) modify Makefile, then modify cross-comile tool gcc's env setting “CROSS_COMPILER”，modify USR_INC as your system root/usr/include  
(3) modify module select setting “MODULE_SELECT”, default module is "drm-glesv2",  now the "wayland-glesv2" module can not run normally   yet, if you can run "wayland-glesv2" module normally, please tell me, and commit to this repository.  
(4) make  
# run on my ARM board result as following：
![result1](https://github.com/fanchenxinok/glmark2_arm/blob/master/doc/result1.jpg)
![result2](https://github.com/fanchenxinok/glmark2_arm/blob/master/doc/result2.jpg)
