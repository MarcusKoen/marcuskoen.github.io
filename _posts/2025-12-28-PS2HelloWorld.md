---
author: Marcus Koen
title: Hello World on the Playstation 2
---

<style>
html, body {
  margin: 0;
  padding: 0;
  background: #0f0f0f;
  color: #e0e0e0;
  font-family: monospace, system-ui, sans-serif;
}

/* Rain container */
.rain-container {
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 1;
  overflow: hidden;
}

/* Individual raindrop */
.raindrop {
  position: absolute;
  width: 1px;
  height: 60px;
  background: linear-gradient(
    to bottom,
    rgba(200, 220, 255, 0),
    rgba(200, 220, 255, 0.35)
  );
  animation: rain linear infinite;
}

/* Falling animation */
@keyframes rain {
  from {
    transform: translateY(-120vh) translateX(0);
  }
  to {
    transform: translateY(120vh) translateX(-80px);
  }
}

/* Variation */
.raindrop:nth-child(1)  { left: 5%;  animation-duration: 0.9s; }
.raindrop:nth-child(2)  { left: 10%; animation-duration: 1.1s; }
.raindrop:nth-child(3)  { left: 15%; animation-duration: 0.8s; }
.raindrop:nth-child(4)  { left: 20%; animation-duration: 1.2s; }
.raindrop:nth-child(5)  { left: 25%; animation-duration: 0.95s; }
.raindrop:nth-child(6)  { left: 30%; animation-duration: 1.05s; }
.raindrop:nth-child(7)  { left: 35%; animation-duration: 0.85s; }
.raindrop:nth-child(8)  { left: 40%; animation-duration: 1.15s; }
.raindrop:nth-child(9)  { left: 45%; animation-duration: 0.9s; }
.raindrop:nth-child(10) { left: 50%; animation-duration: 1.2s; }
.raindrop:nth-child(11) { left: 55%; animation-duration: 0.8s; }
.raindrop:nth-child(12) { left: 60%; animation-duration: 1.1s; }
.raindrop:nth-child(13) { left: 65%; animation-duration: 0.95s; }
.raindrop:nth-child(14) { left: 70%; animation-duration: 1.05s; }
.raindrop:nth-child(15) { left: 75%; animation-duration: 0.85s; }
.raindrop:nth-child(16) { left: 80%; animation-duration: 1.15s; }
.raindrop:nth-child(17) { left: 85%; animation-duration: 0.9s; }
.raindrop:nth-child(18) { left: 90%; animation-duration: 1.2s; }
.raindrop:nth-child(19) { left: 95%; animation-duration: 0.8s; }
</style>

<div class="rain-container">
  <div class="raindrop"></div><div class="raindrop"></div><div class="raindrop"></div>
  <div class="raindrop"></div><div class="raindrop"></div><div class="raindrop"></div>
  <div class="raindrop"></div><div class="raindrop"></div><div class="raindrop"></div>
  <div class="raindrop"></div><div class="raindrop"></div><div class="raindrop"></div>
  <div class="raindrop"></div><div class="raindrop"></div><div class="raindrop"></div>
  <div class="raindrop"></div><div class="raindrop"></div><div class="raindrop"></div>
  <div class="raindrop"></div>
</div>

1. PCSX2
2. Dumb BIOS
3. Hello world C++
4. ELF File
5. Run and check console

# PCSX2
The PS2 emulator. Can be found at [official PCSX2 website](https://pcsx2.net/downloads/) or from their [Github](https://github.com/PCSX2/pcsx2).

# PS2 BIOS
This is required for PCSX2 to run. You get it by dumping your PS2 BIOS to a USB...or maybe there are some floating around online.


# FUCK ME THIS IS WHAT ACTUALLY WORKED

# Persistent Docker
```
docker pull ps2dev/ps2dev:latest
sudo docker run -it --rm -v "$(pwd)":/project -w /project ps2dev/ps2dev:latest

export PS2DEV=/usr/local/ps2dev
export PS2SDK=$PS2DEV/ps2sdk
export PATH=$PATH:$PS2DEV/bin

echo $PS2DEV
echo $PS2SDK
%ee  iop  dvp  ports
mips64r5900el-ps2-elf-gcc --version
apk add --no-cache gmp mpfr mpc1
apk add --no-cache make git bash

```
# Makefile
```
EE_BIN = mygame.elf
EE_OBJS = main.o
EE_LIBS = -ldebug

EE_CFLAGS = -O2 -G0 -Wall

all: $(EE_BIN)

clean:
        rm -f *.elf *.o *.a

include $(PS2SDK)/samples/Makefile.pref
include $(PS2SDK)/samples/Makefile.eeglobal
```
# main.c
```
#include <tamtypes.h>
#include <kernel.h>
#include <sifrpc.h>
#include <debug.h>      // for scr_printf / init_scr

int main(int argc, char **argv)
{
    // Initialize RPC so we can talk to IOP if needed
    SifInitRpc(0);

    // Initialize debug screen output (basic text on screen)
    init_scr();

    // Clear screen and print message
    scr_printf("Hello from PS2 Homebrew!\n");
    scr_printf("Your first ELF is running :)\n\n");
    scr_printf("Press RESET or power off...\n");

    // Infinite loop - game "main loop"
    while(1) {
        // Could add controller reading / graphics later here
    }

    return 0;
}
```
![Hello World](/assets/images/Hello-World-PS2.png)
