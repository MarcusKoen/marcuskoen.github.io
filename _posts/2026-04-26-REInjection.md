---
author: Marcus Koen
title: 4. Cracking - Injection
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

```
Oh my poes, DO NOT hook any applications or inject any code that is not your own, 
it is illegal and only practice on your own software in your own VMs!!!
```
# Environments
Microsoft Detours\
Loader.exe\
HookDLL.dll

# Setting up Detours
What the fuck is this?\
# Build Microsoft Detours
```
git clone https://github.com/microsoft/Detours.git
```
1. Open "x64 Native Tools Command Prompt for VS"
2. Navigate to Detours folder
3. run nmake

# Create Solution
1. Project 1: TestApp (Console App)
2. Project 2: HookDLL (DLL)
3. Project 3: MyLoader (Console App)

# Configure Detours in VS
Do this for HookDLL and MyLoader\
C/C++ → General → Additional Include Directories:\
```
C:\Dev\DetoursProject\detours\include
```
Linker → General → Additional Library Directories:\
```
C:\Dev\DetoursProject\detours\lib.X64
```
Linker → Input → Additional Dependencies:\
```
detours.lib
```
# Fix HookDLL
Linker → Command Line → Additional Options\
```
/EXPORT:DetourFinishHelperProcess,@1
```
Now build

# HookDLL.cpp
Project → Properties → C/C++ → Precompiled Headers\
```
Not Using Precompiled Headers
```

```
#define _CRT_SECURE_NO_WARNINGS
#include <windows.h>
#include <detours.h>
#include <iostream>
#include <string>
//#include "pch.h"
#include <cstdio>
#pragma comment(lib, "detours.lib")

// =======================
// MessageBox Hook
// =======================
typedef int (WINAPI* MessageBoxA_t)(HWND, LPCSTR, LPCSTR, UINT);
MessageBoxA_t OriginalMessageBoxA = MessageBoxA;

int WINAPI HookedMessageBoxA(HWND hWnd, LPCSTR text, LPCSTR caption, UINT type) {
    std::cout << "[HookDLL] MessageBox intercepted!\n";

    return OriginalMessageBoxA(
        hWnd,
        "Hooked MessageBox Text!",
        "Hooked Title",
        type
    );
}

// =======================
// WriteFile Hook (cout)
// =======================
typedef BOOL(WINAPI* WriteFile_t)(
    HANDLE, LPCVOID, DWORD, LPDWORD, LPOVERLAPPED);

WriteFile_t OriginalWriteFile = WriteFile;

BOOL WINAPI HookedWriteFile(
    HANDLE hFile,
    LPCVOID buffer,
    DWORD bytesToWrite,
    LPDWORD bytesWritten,
    LPOVERLAPPED overlapped)
{
    HANDLE hStdOut = GetStdHandle(STD_OUTPUT_HANDLE);

    if (hFile == hStdOut && buffer && bytesToWrite > 0) {
        std::string msg((const char*)buffer, bytesToWrite);
        msg = "[HOOKED] " + msg;

        return OriginalWriteFile(
            hFile,
            msg.c_str(),
            (DWORD)msg.size(),
            bytesWritten,
            overlapped
        );
    }

    return OriginalWriteFile(
        hFile,
        buffer,
        bytesToWrite,
        bytesWritten,
        overlapped
    );
}

// =======================
// Install Hooks
// =======================
void InstallHooks() {
    DetourTransactionBegin();
    DetourUpdateThread(GetCurrentThread());

    DetourAttach(&(PVOID&)OriginalMessageBoxA, HookedMessageBoxA);
    DetourAttach(&(PVOID&)OriginalWriteFile, HookedWriteFile);

    DetourTransactionCommit();
}

// =======================
// Entry Point
// =======================
BOOL APIENTRY DllMain(HMODULE hModule, DWORD reason, LPVOID) {
    if (reason == DLL_PROCESS_ATTACH) {
        DisableThreadLibraryCalls(hModule);

        AllocConsole();
        freopen("CONOUT$", "w", stdout);

        std::cout << "[HookDLL] Injected!\n";

        InstallHooks();

        MessageBoxA(NULL, "DLL Injected Successfully!", "HookDLL", MB_OK);
    }

    return TRUE;
}
```
# MyLoader.cpp
```
#include <windows.h>
#include <detours.h>
#include <iostream>

#pragma comment(lib, "detours.lib")

int main() {
    const char* target =
        "C:\\Dev\\DetoursLab\\DetoursLab\\x64\\Debug\\TestApp.exe";

    const char* dll =
        "C:\\Dev\\DetoursLab\\DetoursLab\\x64\\Debug\\HookDLL.dll";

    STARTUPINFOA si = { sizeof(si) };
    PROCESS_INFORMATION pi = {};

    std::cout << "Launching target with DLL injection...\n";

    if (!DetourCreateProcessWithDllsA(
        NULL,
        (LPSTR)target,
        NULL,
        NULL,
        FALSE,
        CREATE_DEFAULT_ERROR_MODE,
        NULL,
        NULL,
        &si,
        &pi,
        1,
        &dll,
        NULL))
    {
        std::cout << "Failed. Error: " << GetLastError() << std::endl;
        return 1;
    }

    std::cout << "Success! PID: " << pi.dwProcessId << std::endl;

    WaitForSingleObject(pi.hProcess, INFINITE);

    CloseHandle(pi.hProcess);
    CloseHandle(pi.hThread);

    return 0;
}
```
# TestApp.cpp
```
#include <windows.h>
#include <iostream>
#include <string>

int main() {
    std::cout << "=== TestApp Started ===\n";

    std::cout << "Normal cout message 1\n";
    std::cout << "Normal cout message 2\n";

    MessageBoxA(NULL, "Original MessageBox text", "Original Title", MB_OK);

    for (int i = 1; i <= 3; i++) {
        std::string msg = "Loop iteration " + std::to_string(i);
        std::cout << msg << std::endl;

        MessageBoxA(NULL, msg.c_str(), "Loop MessageBox", MB_OK);
    }

    std::cout << "=== TestApp Finished ===\n";
    std::cin.get();

    return 0;
}
```
# Now run Loader.exe
```
Launching target with DLL injection...
Success! PID: xxxxx
[HookDLL] Injected!
[HOOKED] [HookDLL] MessageBox intercepted!
[HOOKED] === TestApp Started ===
[HOOKED] Normal cout message 1
[HOOKED] Normal cout message 2
[HOOKED] [HookDLL] MessageBox intercepted!
[HOOKED] Loop iteration 1[HOOKED]

```


