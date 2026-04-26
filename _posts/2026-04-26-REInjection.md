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
Oh my poes, DO NOT hook any applications or inject any code that is not your own, it is illegal and only practice on your own software in your own
Vms
```
# Environments
Microsoft Detours
Loader.exe
HookDLL.dll

# HookDLL.cpp
```
#include <windows.h>
#include <detours.h>
#include <iostream>

// Typedef for the original function
typedef int (WINAPI* MessageBoxA_t)(HWND hWnd, LPCSTR lpText, LPCSTR lpCaption, UINT uType);
MessageBoxA_t OriginalMessageBoxA = MessageBoxA;   // Point to the real function

// Our hooked version
int WINAPI HookedMessageBoxA(HWND hWnd, LPCSTR lpText, LPCSTR lpCaption, UINT uType) {
    // Log what was going to be shown
    AllocConsole();                    // Optional: create debug console
    freopen("CONOUT$", "w", stdout);
    std::cout << "[Hook] Intercepted MessageBox!\n";
    std::cout << "   Original Text: " << (lpText ? lpText : "NULL") << "\n";
    std::cout << "   Original Caption: " << (lpCaption ? lpCaption : "NULL") << "\n";

    // Modify the message (this is where you can "bypass" or change behavior)
    lpText = "This message was hooked and modified by my loader!";
    lpCaption = "Hooked by MyLoader.exe";

    // Call the original function with our changes
    return OriginalMessageBoxA(hWnd, lpText, lpCaption, uType);
}

// Install the hook
BOOL InstallHooks() {
    DetourTransactionBegin();
    DetourUpdateThread(GetCurrentThread());
    DetourAttach(&(PVOID&)OriginalMessageBoxA, HookedMessageBoxA);
    return DetourTransactionCommit() == NO_ERROR;
}

BOOL APIENTRY DllMain(HMODULE hModule, DWORD reason, LPVOID lpReserved) {
    switch (reason) {
    case DLL_PROCESS_ATTACH:
        DisableThreadLibraryCalls(hModule);
        if (InstallHooks()) {
            MessageBoxA(NULL, "HookDLL injected and hooks installed successfully!", "Success", MB_OK);
        } else {
            MessageBoxA(NULL, "Failed to install hooks!", "Error", MB_OK);
        }
        break;

    case DLL_PROCESS_DETACH:
        // Optional: uninstall hooks
        break;
    }
    return TRUE;
}
```

# Loader.cpp
```
// loader.cpp (simple version)
#include <windows.h>
#include <detours.h>
#include <iostream>

int main() {
    const char* targetExe = "C:\\path\\to\\your\\crackme.exe";   // Change this
    const char* dllToInject = "C:\\path\\to\\HookDLL.dll";       // Your DLL

    STARTUPINFOA si = { sizeof(si) };
    PROCESS_INFORMATION pi = {};

    // This launches the target + injects your DLL automatically
    if (!DetourCreateProcessWithDlls(
            NULL,                          // lpApplicationName
            const_cast<char*>(targetExe),  // lpCommandLine
            NULL, NULL, FALSE,
            CREATE_DEFAULT_ERROR_MODE,     // or CREATE_SUSPENDED if you need more control
            NULL, NULL,
            &si, &pi,
            1, &dllToInject,               // Number of DLLs + array of paths
            NULL)) {

        std::cout << "Failed to create process with DLL. Error: " << GetLastError() << std::endl;
        return 1;
    }

    std::cout << "Process launched with DLL injected! PID: " << pi.dwProcessId << std::endl;

    // Optional: Wait for the process
    WaitForSingleObject(pi.hProcess, INFINITE);

    CloseHandle(pi.hProcess);
    CloseHandle(pi.hThread);
    return 0;
}
```
# Suspended + Manual Injection

```
// Manual suspended injection example (basic LoadLibrary style)
STARTUPINFO si = { sizeof(si) };
PROCESS_INFORMATION pi;

if (!CreateProcess(NULL, const_cast<char*>(targetExe), NULL, NULL, FALSE,
                   CREATE_SUSPENDED, NULL, NULL, &si, &pi)) {
    // error
}

// Allocate memory in target for DLL path
SIZE_T pathLen = strlen(dllToInject) + 1;
LPVOID remoteMem = VirtualAllocEx(pi.hProcess, NULL, pathLen, MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);

WriteProcessMemory(pi.hProcess, remoteMem, dllToInject, pathLen, NULL);

// Get LoadLibrary address (same in all processes)
LPVOID loadLibAddr = (LPVOID)GetProcAddress(GetModuleHandle("kernel32.dll"), "LoadLibraryA");

// Create remote thread to call LoadLibrary
HANDLE hThread = CreateRemoteThread(pi.hProcess, NULL, 0,
                                    (LPTHREAD_START_ROUTINE)loadLibAddr,
                                    remoteMem, 0, NULL);

// Resume the main thread
ResumeThread(pi.hThread);
```

