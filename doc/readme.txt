(1) cd src/
(2) modify Makefile, change the CROSS_COMPILER to your cross compiler and your USR_INC( usr/include) dir in your sysroot. 
(3) modify MODULE_SELECT, default is drm-glesv2 module, just this module can work now, if you can run wayland-glesv2 module on
    your arm board, please tell me.
(4) make