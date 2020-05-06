TOP_DIR = ..

SOURCES =

ifeq ($(MODULE_SELECT), drm-gl)
	SOURCES += ./src/gl.c
else ifeq ($(MODULE_SELECT), drm-glesv2)
	SOURCES += ./src/egl.c ./src/gles2.c
else ifeq ($(MODULE_SELECT), wayland-gl)
	SOURCES += ./src/gl.c
else ifeq ($(MODULE_SELECT), wayland-glesv2)
	SOURCES += ./src/egl.c ./src/gles2.c
else
	SOURCES +=
endif

INCLUDE_DIRS = -I./include -I$(TOP_DIR)/
TARGET = libglad.a
OBJECTS = $(patsubst %.c,%.o,$(SOURCES))

$(TARGET) : $(OBJECTS)
	$(AR) $(ARFLAG) $@ $^
	
$(OBJECTS) : %.o : %.c 
	$(CC) -c $(CFLAGS) $< -o $@ $(INCLUDE_DIRS)

.PHONY : clean
clean:
	rm -rf $(TARGET) $(OBJECTS) 