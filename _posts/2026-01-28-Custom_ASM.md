---
title: Custom Assembler ISA Instruction Set (In Progress) with emulator
author: Marcus Koen 
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

# Project available (here)[https://github.com/MarcusKoen/LISA]
I accidentally deleted the VM.cpp file.


# Start small:

1. Custom ISA
2. 8–16 instructions
3. register-based
4. output binary blobs
5. 
# Specs
1. Register based
2. 32-bit instruction size
3. 8 General purpose registers
4. Little-endian
5. Flat byte-addressed memory
6. No Flags
```

   31        24 23     20 19     16 15              0
+------------+---------+---------+----------------+
|   OPCODE   |   RD    |   RS    |    IMMEDIATE   |
+------------+---------+---------+----------------+
   8 bits       4 bits   4 bits       16 bits
```

# Registers
```
1. R0
2. R1
3. R2
4. R3
5. R4
6. R5
7. R6
8. R7
```
# Movement
```
MOV 
MOVR 
```
# Arithmetic
```
ADD
SUB
MUL
DIV
```
# Memory
```
LOAD
STORE
```
# Control
```
CMP
JMP
JZ
JNZ
```
# System
```
HALT
```
# Syntax
```
MOV  R1, 5
MOV  R0, 0

loop:
ADD  R0, R1
SUB  R1, 1
CMP  R1, 0
JNZ  loop

HALT
```
# Virtual Machine Implementation with sample program
```
#include <iostream>
#include <stdint-gcc.h>
using namespace std;


#include <cstdint>
#include <iostream>

enum Opcode {
    OP_MOV = 1,
    OP_ADD,
    OP_SUB,
    OP_CMP,
    OP_JNZ,
    OP_HALT
};

struct VM
{
    uint32_t regs[8]{};
    uint8_t memory[65536]{};
    uint32_t pc = 0;
    int32_t cmp = 0;
    bool running = true;

    // --- Helpers ---
    uint32_t fetch32()
    {
        uint32_t val = 0;
        val |= memory[pc];
        val |= memory[pc + 1] << 8;
        val |= memory[pc + 2] << 16;
        val |= memory[pc + 3] << 24;
        return val;
    }

    void step()
    {
        uint32_t instr = fetch32();

        uint8_t opcode = instr >> 24;
        uint8_t rd     = (instr >> 20) & 0xF;
        uint8_t rs     = (instr >> 16) & 0xF;
        uint16_t imm   = instr & 0xFFFF;

        pc += 4;

        switch (opcode)
        {
            case OP_MOV:
                regs[rd] = imm;
                break;

            case OP_ADD:
                regs[rd] += regs[rs];
                break;

            case OP_SUB:
                regs[rd] -= regs[rs];
                break;

            case OP_CMP:
                cmp = regs[rd] - regs[rs];
                break;

            case OP_JNZ:
                if (cmp != 0)
                    pc = imm;
                break;

            case OP_HALT:
                running = false;
                break;

            default:
                std::cerr << "Unknown opcode: " << int(opcode) << "\n";
                running = false;
        }
    }

    void run()
    {
        while (running)
            step();
    }
};


int main()
{

    VM vm;

    uint32_t program[] = {
        (OP_MOV << 24) | (0 << 20) | 0,
        (OP_MOV << 24) | (1 << 20) | 5,
        (OP_ADD << 24) | (0 << 20) | (1 << 16),
        (OP_HALT << 24)
    };

    memcpy(vm.memory, program, sizeof(program));
    vm.run();

    std::cout << "R0 = " << vm.regs[0] << "\n"; // should print 5


}
```
# Assembler
```
#include <iostream>
#include <sstream>
#include <vector>
#include <unordered_map>
#include <fstream>
#include <cstdint>

enum Opcode {
    OP_MOV = 1,
    OP_ADD,
    OP_SUB,
    OP_CMP,
    OP_JNZ,
    OP_HALT
};

uint8_t regIndex(const std::string& r)
{
    if (r[0] != 'R') throw std::runtime_error("Invalid register");
    return std::stoi(r.substr(1));
}

uint32_t encode(uint8_t op, uint8_t rd = 0, uint8_t rs = 0, uint16_t imm = 0)
{
    return (op << 24) | (rd << 20) | (rs << 16) | imm;
}

int main()
{
    std::ifstream file("program.asm");
    if (!file) return 1;

    std::vector<std::string> lines;
    std::unordered_map<std::string, uint32_t> labels;

    std::string line;
    uint32_t pc = 0;

    // ---- PASS 1: read lines + labels
    while (std::getline(file, line))
    {
        if (line.empty()) continue;

        if (line.back() == ':')
        {
            labels[line.substr(0, line.size() - 1)] = pc;
        }
        else
        {
            lines.push_back(line);
            pc += 4;
        }
    }

    // ---- PASS 2: assemble
    std::vector<uint32_t> program;

    for (auto& l : lines)
    {
        std::stringstream ss(l);
        std::string op;
        ss >> op;

        if (op == "MOV")
        {
            std::string r;
            int imm;
            ss >> r;
            ss.ignore(1); // comma
            ss >> imm;
            program.push_back(encode(OP_MOV, regIndex(r), 0, imm));
        }
        else if (op == "ADD")
        {
            std::string r1, r2;
            ss >> r1;
            ss.ignore(1);
            ss >> r2;
            program.push_back(encode(OP_ADD, regIndex(r1), regIndex(r2)));
        }
        else if (op == "SUB")
        {
            std::string r1, r2;
            ss >> r1;
            ss.ignore(1);
            ss >> r2;
            program.push_back(encode(OP_SUB, regIndex(r1), regIndex(r2)));
        }
        else if (op == "CMP")
        {
            std::string r1, r2;
            ss >> r1;
            ss.ignore(1);
            ss >> r2;
            program.push_back(encode(OP_CMP, regIndex(r1), regIndex(r2)));
        }
        else if (op == "JNZ")
        {
            std::string label;
            ss >> label;
            program.push_back(encode(OP_JNZ, 0, 0, labels[label]));
        }
        else if (op == "HALT")
        {
            program.push_back(encode(OP_HALT));
        }
        else
        {
            throw std::runtime_error("Unknown instruction: " + op);
        }
    }

// ---- Output to binary file instead of printing hex
std::ofstream out("program.bin", std::ios::binary);
if (!out) {
    std::cerr << "Cannot create program.bin\n";
    return 1;
}

for (auto instr : program) {
    // Write little-endian (most common / matches your fetch32 logic)
    out.put(static_cast<char>(instr >> 0));
    out.put(static_cast<char>(instr >> 8));
    out.put(static_cast<char>(instr >> 16));
    out.put(static_cast<char>(instr >> 24));
}

out.close();
std::cout << "Assembled " << program.size() << " instructions to program.bin\n";
}
```
