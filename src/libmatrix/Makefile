TOP_DIR = ..

SOURCES = $(wildcard ./*.cc)
INCLUDE_DIRS = -I./ -I$(TOP_DIR)/include -I$(TOP_DIR)/glad/include
TARGET = libmatrix.a
OBJECTS = $(patsubst %.cc,%.o,$(SOURCES))

$(TARGET) : $(OBJECTS)
	$(AR) $(ARFLAG) $@ $^
	
$(OBJECTS) : %.o : %.cc 
	$(CXX) -c $(CFLAGS) $< -o $@ $(INCLUDE_DIRS)

.PHONY : clean
clean:
	rm -rf $(TARGET) $(OBJECTS) 