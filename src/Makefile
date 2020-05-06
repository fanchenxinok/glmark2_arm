CROSS_COMPILER = $(EASY_SDK)/sysroots/x86_64-arago-linux/usr/bin/arm-linux-gnueabihf
CC = $(CROSS_COMPILER)-gcc --sysroot=$(EASY_SDK)/sysroots/armv7ahf-neon-linux-gnueabi
CXX = $(CROSS_COMPILER)-g++ --sysroot=$(EASY_SDK)/sysroots/armv7ahf-neon-linux-gnueabi
AR = $(CROSS_COMPILER)-ar
ARFLAG = -rcs

USR_INC = /home/joe/worksource/toolchain_sdk_j6entry/sysroots/armv7ahf-neon-linux-gnueabi/usr

MODULE_SELECT=drm-glesv2
#MODULE_SELECT=wayland-glesv2

CFLAGS = -g -O0 -march=armv7-a -marm -mfpu=neon -mfloat-abi=hard
CLIBS = -L./libmatrix/ -lmatrix -L./libpng -lpng -L./zlib -lzlib -L./glad -lglad -L./libjpeg-turbo -ljpeg-turbo -lm -ldl -lrt -ljpeg
INCLUDE_DIRS = -I$(USR_INC)/include/ -I./include -I./glad/include -I./module_select -I./scene-terrain -I./scene-ideas -I./libmatrix -I./zlib -I./libpng -I./libjepg-turbo 
SUBDIRS = ./libmatrix ./zlib ./libpng ./glad ./libjpeg-turbo 

TARGET = glmark2_arm
SOURCES = $(wildcard ./*.cpp ./scene-terrain/*.cpp ./scene-ideas/*.cpp)

ifeq ($(MODULE_SELECT), drm-gl)
	SOURCES += ./module_select/native-state-drm.cpp
	CLIBS += -ldrm -lgbm -ludev
	CFLAGS += -DGLMARK2_USE_DRM -DGLMARK2_USE_GL -DGLMARK2_USE_EGL
	INCLUDE_DIRS += -I$(USR_INC)/include/EGL \
			-I$(USR_INC)/include/drm \
			-I$(USR_INC)/include/gbm
else ifeq ($(MODULE_SELECT), drm-glesv2)
	SOURCES += ./module_select/native-state-drm.cpp
	CLIBS += -ldrm -lgbm -ludev
	CFLAGS += -DGLMARK2_USE_DRM -DGLMARK2_USE_GLESv2 -DGLMARK2_USE_EGL
	INCLUDE_DIRS += -I$(USR_INC)/include/EGL \
			-I$(USR_INC)/include/GLES2 \
			-I$(USR_INC)/include/drm \
			-I$(USR_INC)/include/gbm
else ifeq ($(MODULE_SELECT), wayland-gl)
	SOURCES += ./module_select/native-state-wayland.cpp
	CLIBS += -lwayland-client -lwayland-server -L./xdc_shell -lxdc-shell -L./wayland-egl -lwayland-egl
	CFLAGS += -DGLMARK2_USE_WAYLAND -DGLMARK2_USE_GL -DGLMARK2_USE_EGL
	INCLUDE_DIRS += -I$(USR_INC)/include/EGL -I./xdc_shell
	SUBDIRS += ./xdc_shell ./wayland-egl
else ifeq ($(MODULE_SELECT), wayland-glesv2)
	SOURCES += ./module_select/native-state-wayland.cpp
	CLIBS += -lwayland-client -lwayland-server -L./xdc_shell -lxdc-shell -L./wayland-egl -lwayland-egl
	CFLAGS += -DGLMARK2_USE_WAYLAND -DGLMARK2_USE_GLESv2 -DGLMARK2_USE_EGL
	INCLUDE_DIRS += -I$(USR_INC)/include/EGL \
			-I$(USR_INC)/include/GLES2 \
			-I./xdc_shell
	SUBDIRS += ./xdc_shell ./wayland-egl
else
	SOURCES +=
endif

export CC CXX CFLAGS AR ARFLAG MODULE_SELECT
	
CPP_OBJECTS = $(patsubst %.cpp,%.o,$(SOURCES))

OBJECTS = $(CPP_OBJECTS)

$(TARGET) : $(OBJECTS)
	$(CXX) $^ -o $@ $(CLIBS)

$(OBJECTS) : %.o : %.cpp $(SUBDIRS)
	$(CXX) -c $(CFLAGS) $< -o $@ $(INCLUDE_DIRS)

$(SUBDIRS):ECHO
	+$(MAKE) -C $@

ECHO:
	@echo $(SUBDIRS)
	@echo begin compile

.PHONY : clean
clean:
	for dir in $(SUBDIRS);\
	do $(MAKE) -C $$dir clean||exit 1;\
	done
	rm -rf $(TARGET) $(OBJECTS) ./lib/*.a
