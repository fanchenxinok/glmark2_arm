TOP_DIR = ..

SOURCES = $(wildcard ./src/*.c)
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