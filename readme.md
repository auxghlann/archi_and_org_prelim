# 8086 Assembler

## What is Assembly Language?
* A low-level programming language.
* Represents machine code instructions in a human-readable format.

## Computer Model

<img src="Screenshot 2024-09-17 182753.png"> 

* **System Bus:** Connects various components of the computer.
* **CPU:** The heart of the computer.
* **RAM:** Stores programs for execution.

## Inside the CPU
### General Purpose Registers
* **`AX`:** Accumulator register (AH/AL).
* **`BX`:** Base address register (BH/BL).
* **`CX`:** Count register (CH/CL).
* **`DX`:** Data register (DH/DL).
* **`SI`:** Source index register.
* **`DI`:** Destination index register.
* **`BP`:** Base pointer.
* **`SP`:** Stack pointer.

## Registers

* **Programmer determines usage:** The programmer decides how to use each general-purpose register.
* **Main purpose:** To store numbers (variables).
* **Size:** 16 bits.
* **Example:** 0011000000111001b (binary) or 12345 (decimal).

### Registers with 8-bit Sub-registers
* **`AX`:** AH and AL
* **`BX`:** BH and BL
* **`CX`:** CH and CL
* **`DX`:** DH and DL

### Example
* If AX = 0011000000111001b, then AH = 00110000b and AL = 00111001b.

### Speed
* Registers are much faster than memory due to their location inside the CPU.
* Accessing memory requires the system bus, which is slower.
* Try to keep variables in registers for faster execution.

### Limitations
* Register sets are small.
* Many registers have specific purposes, limiting their use as variables.
* Registers are ideal for temporary data storage during calculations.

## Segment Registers

### Segment Registers
* **`CS`:** Points to the code segment.
* **`DS`:** Points to the data or variable segment.
* **`ES`:** Extra segment register.
* **`SS`:** Points to the stack segment.

### Segment Registers and Effective Addresses

* Segment registers Point to accessible memory blocks.
* *Not for data storage:* Segment registers are not suitable for storing arbitrary data.
* **`Effective addresses`:** 
  * Formed by combining segment and general-purpose registers.

* **Default pairings:**
    * BX, SI, DI: DS
    * BP, SP: SS
* **Valid registers:** 
  * Only certain general-purpose registers can form effective addresses (e.g., BX, SI, DI).
* **Sub-registers:** 
  * Sub-registers (like BH, BL) cannot form effective addresses.

### Special Purpose Registers
#### **`IP`:** 
 * Instruction pointer.
 * register always works together with CS segment register
 * it points to currently executing instruction.
#### **`Flags Register`:** 
 * Indicates the current state of the microprocessor.
 * modified automatically by CPU after mathematical operations, this allows to determine the type of the resul
 * determine conditions to transfer control to other parts of the program.
 * generally you cannot access these registers directly

## Memory Access
* **segment** - value in segment register (CS, DS, ES, SS)
* **offset** - value in purpose register (BX, SI, DI, BP)
## Data Types
* **`byte ptr`:** For byte.
* **`word ptr`:** For word (two bytes).
* Shorter prefixes: `b.` and `w.`.

## MOV Instruction
* Copies the second operand to the first.
* Supports various operand types: immediate values, registers, memory locations.
* Both operands must be the same size (byte or word).

* Cannot set CS or IP registers.

## Variables
* Named memory locations.
* Supported types: BYTE and WORD.
* Declaration syntax: `name DB value` or `name DW value`.
* Can be declared with or without names.
* MOV instruction used to copy values.

## Arrays
* Chains of variables.
* Text strings are byte arrays.
* Declaration syntax: `name DB value1, value2, ...`.
* Can be defined using strings.

## Compiler and Memory
* Compiler replaces variable names with offsets.
* DS register is used for the data segment.
* Memory layout: offset, hexadecimal value, decimal value, ASCII character.
* Compiler is not case-sensitive.
* ORG directive specifies the loading offset.
* Arrays are stored sequentially in memory.
--
* **Compiler conversion:** 
  * The compiler converts program source code into a set of bytes called machine code.
* **ORG directive:** 
  * Specifies how the compiler should handle the source code.
    * Sets the loading offset for the executable file (e.g., 100h).
    * Helps calculate correct variable addresses.
* **Loading offset:**
    * **COM files**: **`100h`** (256 bytes) to avoid overwriting operating system data.
    * **EXE files**: **`0000h`** and typically use a separate segment for variables.