---
author: Marcus Koen
title: 1. Cracking - Debug Flags
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

A quick note: https://anti-debug.checkpoint.com/ is absolutely, fucking invaluable resource. This series will show how to patch all the checks mentioned.

# IsDebuggerPresent()
This function is from the Win32 API
Code used:
```
#include <iostream>
#include <windows.h>
using namespace std;

int main()
{

    cout << "Hello world!" << endl;

    while(!IsDebuggerPresent())
    {

    }
    //just realized to make this harder give no message
    cout << "Debugger Detected" << endl;
    return 0;
}

```
Assembly from said function in x64dbg

<pre><code>00007FF793CD16D0 | 55                       | push rbp                                |
00007FF793CD16D1 | 48:89E5                  | mov rbp,rsp                             |
00007FF793CD16D4 | 48:83EC 20               | sub rsp,20                              |
00007FF793CD16D8 | E8 4A010000              | call idp.7FF793CD1827                   |
00007FF793CD16DD | EB 28                    | jmp idp.7FF793CD1707                    |
00007FF793CD16DF | 48:8D05 6A390000         | lea rax,qword ptr ds:[7FF793CD5050]     | rax:EntryPoint, 00007FF793CD5050:"No Debugger"
00007FF793CD16E6 | 48:89C2                  | mov rdx,rax                             | rdx:EntryPoint, rax:EntryPoint
00007FF793CD16E9 | 48:8B05 F03C0000         | mov rax,qword ptr ds:[<&std::cout>]     | rax:EntryPoint
00007FF793CD16F0 | 48:89C1                  | mov rcx,rax                             | rax:EntryPoint
00007FF793CD16F3 | E8 58000000              | call <JMP.&std::basic_ostream<char, std |
00007FF793CD16F8 | 48:8D05 5D390000         | lea rax,qword ptr ds:[7FF793CD505C]     | rax:EntryPoint, 00007FF793CD505C:"cls"
00007FF793CD16FF | 48:89C1                  | mov rcx,rax                             | rax:EntryPoint
00007FF793CD1702 | E8 E11A0000              | call <JMP.&system>                      |
00007FF793CD1707 | 48:8B05 2A8C0000         | mov rax,qword ptr ds:[<IsDebuggerPresen | rax:EntryPoint
00007FF793CD170E | FFD0                     | call rax                                | rax:EntryPoint
<mark>00007FF793CD1710 | 85C0                     | test eax,eax                            |</mark>
00007FF793CD1712 | 0F94C0                   | sete al                                 |
00007FF793CD1715 | 84C0                     | test al,al                              |
00007FF793CD1717 | 75 C6                    | jne idp.7FF793CD16DF                    |
00007FF793CD1719 | 48:8D05 40390000         | lea rax,qword ptr ds:[7FF793CD5060]     | rax:EntryPoint, 00007FF793CD5060:"Debugger Detected"
00007FF793CD1720 | 48:89C2                  | mov rdx,rax                             | rdx:EntryPoint, rax:EntryPoint
00007FF793CD1723 | 48:8B05 B63C0000         | mov rax,qword ptr ds:[<&std::cout>]     | rax:EntryPoint
00007FF793CD172A | 48:89C1                  | mov rcx,rax                             | rax:EntryPoint
00007FF793CD172D | E8 1E000000              | call <JMP.&std::basic_ostream<char, std |
00007FF793CD1732 | 48:89C1                  | mov rcx,rax                             | rax:EntryPoint
00007FF793CD1735 | 48:8B05 B43C0000         | mov rax,qword ptr ds:[<&JMP.&std::basic | rax:EntryPoint
00007FF793CD173C | 48:89C2                  | mov rdx,rax                             | rdx:EntryPoint, rax:EntryPoint
00007FF793CD173F | E8 1C000000              | call <JMP.&std::ostream::operator<<(std |
00007FF793CD1744 | B8 00000000              | mov eax,0                               |
00007FF793CD1749 | 48:83C4 20               | add rsp,20                              |
00007FF793CD174D | 5D                       | pop rbp                                 |
00007FF793CD174E | C3                       | ret                                     |
</code></pre>

