# Include common build rules
include ../Rules.mk

# Define the name of the application
APP := video_decode

# Specify source files for the application
SRCS := \
	video_decode_csvparser.cpp \
	video_decode_main.cpp \
	$(wildcard $(CLASS_DIR)/*.cpp)

# Generate object file names from source file names
OBJS := $(SRCS:.cpp=.o)

# OpenCV libraries
OPENCV_LIBS := `pkg-config --libs opencv4`
OPENCV_CFLAGS := `pkg-config --cflags opencv4`

# Compiler flags
CPPFLAGS += $(OPENCV_CFLAGS)

# Target for building all objects
all: $(APP)

# Rule to build object files for source files in the class directory
$(CLASS_DIR)/%.o: $(CLASS_DIR)/%.cpp
	$(AT)$(MAKE) -C $(CLASS_DIR)

# Rule to compile source files into object files
%.o: %.cpp
	@echo "Compiling: $<"
	$(CPP) $(CPPFLAGS) -c $<

# Rule to link object files into the final executable
$(APP): $(OBJS)
	@echo "Linking: $@"
	$(CPP) -o $@ $(OBJS) $(CPPFLAGS) $(LDFLAGS) $(OPENCV_LIBS)

# Target to clean up built files
clean:
	$(AT)rm -rf $(APP) $(OBJS)
