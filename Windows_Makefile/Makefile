# Directories
MSPGCC_ROOT_DIR = /path/to/your/msp430-gcc
MSPGCC_BIN_DIR = $(MSPGCC_ROOT_DIR)/bin
MSPGCC_INCLUDE_DIR = $(MSPGCC_ROOT_DIR)/include
INCLUDE_DIRS = $(MSPGCC_INCLUDE_DIR)
LIB_DIRS = $(MSPGCC_INCLUDE_DIR)
BUILD_DIR = build
OBJ_DIR = $(BUILD_DIR)/obj
BIN_DIR = $(BUILD_DIR)/bin
TI_CCS_DIR = /path/to/your/ccs2020/ccs
DEBUG_BIN_DIR = $(TI_CCS_DIR)/ccs_base/DebugServer/bin
DEBUG_DRIVERS_DIR = $(TI_CCS_DIR)/ccs_base/DebugServer/drivers

# Toolchain
CC = $(MSPGCC_BIN_DIR)/msp430-elf-gcc.exe
RM = rm -rf
DEBUG = LD_LIBRARY_PATH=$(DEBUG_DRIVERS_DIR) $(DEBUG_BIN_DIR)/DSlite.exe
CPPCHECK = cppcheck
FORMAT = clang-format
SIZE = $(MSPGCC_BIN_DIR)/msp430-elf-size
READELF = $(MSPGCC_BIN_DIR)/msp430-elf-readelf

# Files
TARGET = $(BIN_DIR)/blink

# Sources
SOURCES = # Add your sources

# Objects
OBJECT_NAMES = $(SOURCES:.c=.o)
OBJECTS = $(patsubst %,$(OBJ_DIR)/%,$(OBJECT_NAMES))

# Static Analysis
CPPCHECK_FLAGS = \
	--quiet --enable=all --error-exitcode=1 \
	--inline-suppr \
	--suppress=toomanyconfigs \
	-I $(INCLUDE_DIRS) \
	$(SOURCES) && echo "Done"

# Flags
MCU = msp430fr2355
WFLAGS = -Wall -Wextra -Werror -Wshadow
CFLAGS = -mmcu=$(MCU) $(WFLAGS) $(addprefix -I,$(INCLUDE_DIRS)) -Og -g
LDFLAGS = -mmcu=$(MCU) $(addprefix -L,$(LIB_DIRS))

# Build
## Linking
$(TARGET): $(OBJECTS)
	@mkdir -p $(dir $@)
	$(CC) $(LDFLAGS) $^ -o $@

## Compiling
$(OBJ_DIR)/%.o: %.c
	@mkdir -p $(dir $@)
	$(CC) $(CFLAGS) -c -o $@ $^

# Phonies
.PHONY: all clean flash cppcheck format size 

all: $(TARGET)

clean:
	$(RM) $(BUILD_DIR)

flash: $(TARGET)
	$(DEBUG) load --config=/path/to/your/MSP-EXP430FR2355LP.ccxml $(TARGET)

cppcheck:
	@echo "Starting. Please wait..."
	@$(CPPCHECK) $(CPPCHECK_FLAGS)

format:
	@$(FORMAT) -i $(SOURCES)

size: $(TARGET)
	$(SIZE) $(TARGET)

symbols: $(TARGET)
	$(READELF) -s $(TARGET) | sort -n
