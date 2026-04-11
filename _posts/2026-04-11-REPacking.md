---
author: Marcus Koen
title: 2. Cracking - Packing/Loading Custom Stub
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

  /* Fix code block visibility */
pre, code {
  background-color: #0b0b0b !important;
  color: #f2f2f2 !important;
}

/* Inline code */
code {
  padding: 0.15em 0.35em;
  border-radius: 4px;
}

/* Fenced code blocks */
pre {
  padding: 1em;
  overflow-x: auto;
  border-radius: 6px;
  box-shadow: inset 0 0 0 1px rgba(255,255,255,0.08);
}

/* Optional: monospace consistency */
pre, code {
  font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
}

  /* Highlighted line in assembly dumps */
mark {
    display: inline-block;
  margin-left: -1ch; /* adjust if needed */
  background-color: #334422 !important;   /* matrix-greenish glow */
  color: #ff0 !important;
  padding: 2px 6px;
  border-radius: 3px;
  font-weight: bold;
  box-shadow: 0 0 8px rgba(255, 255, 0, 0.3);
}

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

Thank you to [frank2](https://github.com/frank2/packer-tutorial) for the invaluable fucking resource
TODO: CMAKE

# Simple Packing with [UPX](https://github.com/upx/upx)

# Code for main program to be packed
```
#include <iostream>

using namespace std;

int main()
{
    bool bFlag = false;

    int pass = 80085;
    int entered;
    while(!bFlag)
    {
        cout << "Enter Code" << endl;
        cin >> entered;

        if(pass==entered)
            bFlag = true;
            else cout << "Pass incorrect" << endl;
    }

    cout << "Correct" << endl;

    return 0;
}
```
# CRITICAL: So for future unpacking jobs:

    Disable ASLR on the original packed EXE before you even start debugging (using CFF Explorer or similar).
    This way, the unpacked code will always land at the same base address every time.
# Finding OEP of the actual payload
I used the tailhead method. When in first entry point in user module, use graph view to check functions that have a lot of filler functions.
That function pointing to those dud functions actually leads to the OEP if stepped into.

The first entry point given by x64dbg:
```
0000000140016230 | 53                       | push rbx                                                  |
```
Openin graph view we see the following at the Entry Point
```
0000000140016230 | 53                       | push rbx                                                  |
0000000140016231 | 56                       | push rsi                                                  |
0000000140016232 | 57                       | push rdi                                                  |
0000000140016233 | 55                       | push rbp                                                  |
0000000140016234 | 48:8D35 EADDFFFF         | lea rsi,qword ptr ds:[140014025]                          |
000000014001623B | 48:8DBE DBCFFEFF         | lea rdi,qword ptr ds:[rsi-13025]                          |
0000000140016242 | 57                       | push rdi                                                  |
0000000140016243 | 31DB                     | xor ebx,ebx                                               |
0000000140016245 | 31C9                     | xor ecx,ecx                                               |
0000000140016247 | 48:83CD FF               | or rbp,FFFFFFFFFFFFFFFF                                   |
000000014001624B | E8 50000000              | call topack(packed).1400162A0                             |
```
Stepping into the call with graph view you will see the following function:
```
0000000140016482 | 48:39C4                  | cmp rsp,rax                                               | rax:EntryPoint
0000000140016485 | 75 F9                    | jne topack(packed).140016480                              |
0000000140016487 | 48:83EC 80               | sub rsp,FFFFFFFFFFFFFF80                                  |
000000014001648B | E9 95ACFEFF              | jmp topack(packed).140001125                              |
```

Analyzing:
```
000000014001648B | E9 95ACFEFF              | jmp topack(packed).140001125                              |
```
contains massive padding of byte pointers e.g:
```
000000014000111D | 0000                     | add byte ptr ds:[rax],al                                  | rax:EntryPoint
000000014000111F | 0000                     | add byte ptr ds:[rax],al                                  | rax:EntryPoint
0000000140001121 | 0000                     | add byte ptr ds:[rax],al                                  | rax:EntryPoint
0000000140001123 | 0000                     | add byte ptr ds:[rax],al                                  | rax:EntryPoint
0000000140001125 | 0000                     | add byte ptr ds:[rax],al                                  | rax:EntryPoint
0000000140001127 | 0000                     | add byte ptr ds:[rax],al                                  | rax:EntryPoint
0000000140001129 | 0000                     | add byte ptr ds:[rax],al                                  | rax:EntryPoint
000000014000112B | 0000                     | add byte ptr ds:[rax],al                                  | rax:EntryPoint
000000014000112D | 0000                     | add byte ptr ds:[rax],al                                  | rax:EntryPoint
000000014000112F | 0000                     | add byte ptr ds:[rax],al                                  | rax:EntryPoint
0000000140001131 | 0000                     | add byte ptr ds:[rax],al                                  | rax:EntryPoint
0000000140001133 | 0000                     | add byte ptr ds:[rax],al                                  | rax:EntryPoint
0000000140001135 | 0000                     | add byte ptr ds:[rax],al                                  | rax:EntryPoint
0000000140001137 | 0000                     | add byte ptr ds:[rax],al                                  | rax:EntryPoint
```
So we know that 140001125 is the entry point
Putting a break point on the function that jumps to the entry point we can then step into the call once the breakpoint hits 
```
000000014001648B | E9 95ACFEFF              | jmp topack(packed).140001125                              |
```
Stepping in reveals the actual execution code
```
0000000140001125 | 55                       | push rbp                                                  |
0000000140001126 | 48:89E5                  | mov rbp,rsp                                               |
0000000140001129 | 48:83EC 30               | sub rsp,30                                                |
000000014000112D | C745 FC FF000000         | mov dword ptr ss:[rbp-4],FF                               |
0000000140001134 | 48:8B05 55430000         | mov rax,qword ptr ds:[140005490]                          |
000000014000113B | C700 00000000            | mov dword ptr ds:[rax],0                                  |
0000000140001141 | E8 0E000000              | call topack(packed).140001154                             |
0000000140001146 | 8945 FC                  | mov dword ptr ss:[rbp-4],eax                              |
```
So we have confirmed that 0000000140001125 is the EOP.
Now for Scylla:
1. OEP as 0000000140001125
2. IAT Autosearch and click Advanced searc(yes)
3. Get Imports
4. Delete or trunk invalid imports
5. Dump exe
6. Fix Dumped exe
7. Can now analyze statically or dynamically without any packing



