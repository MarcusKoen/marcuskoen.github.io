---
author: Marcus Koen
title: Hello World on the Playstation 2
---

1. PCSX2
2. Dumb BIOS
3. Hello world C++
4. ELF File
5. Run and check console

# PCSX2
The PS2 emulator. Can be found at [official PCSX2 website](https://pcsx2.net/downloads/) or from their [Github](https://github.com/PCSX2/pcsx2).

# PS2 BIOS
This is required for PCSX2 to run. You get it by dumping your PS2 BIOS to a USB...or maybe there are some floating around online.

# Install dependencies
```
sudo apt update
sudo apt install -y git build-essential cmake \
    texinfo bison flex libgmp-dev libmpfr-dev libmpc-dev
```
# Install ps2dev Toolchain
```
git clone https://github.com/ps2dev/ps2dev.git
cd ps2dev
./install.sh
```
# Add to your shell config

```
~/.bashrc
export PS2DEV=$HOME/ps2dev
export PATH=$PATH:$PS2DEV/bin
source ~/.bashrc
mips64r5900el-ps2-elf-gcc --version
```
# First program
```
#include <tamtypes.h>
#include <kernel.h>
#include <stdio.h>

int main(int argc, char *argv[])
{
    printf("Hello World from PlayStation 2!\n");

    // Keep running so emulator doesn’t instantly exit
    SleepThread();
    return 0;
}
```
# Makefile
```
EE_BIN = hello.elf
EE_OBJS = main.o

EE_INCS =
EE_LIBS = -lc

all: $(EE_BIN)

clean:
	rm -f *.o *.elf

include $(PS2DEV)/ee/Makefile.pref
include $(PS2DEV)/ee/Makefile.eeglobal
```
# Build
```
make
hello.elf
```
