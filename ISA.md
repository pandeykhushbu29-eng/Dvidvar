# Chapter 1 — Introduction

## 1.1 Purpose

Dvidvar (Doublers is a nickname) is an open 64-trit Instruction Set Architecture (ISA) designed to be simple, predictable, and practical. It is intended for operating systems, systems software, compilers, educational use, and future hardware implementations.

The ISA defines the behavior of processors that execute Doublers instructions. It does not define the physical design of a processor. Hardware designers are free to implement the ISA using any suitable architecture, provided the implementation behaves according to this specification.

---

## 1.2 Goals

The primary goals of Doublers are:

* Simplicity over unnecessary complexity.
* Fixed, well-defined instruction behavior.
* Easy implementation in hardware.
* Efficient native execution.
* Stable long-term compatibility.
* Open specification for software and hardware developers.

---

## 1.3 Scope

This specification defines:

* The register architecture.
* The memory model.
* Instruction encoding.
* Instruction behavior.
* Exception handling.
* Privilege levels.
* System calls.
* Compliance requirements.

This specification does not define:

* Operating system design.
* Compiler implementation.
* Processor microarchitecture.
* Semiconductor manufacturing.

---

## 1.4 Design Philosophy

Doublers follows five design principles:

1. Simplicity
2. Predictability
3. Readability
4. Hardware friendliness
5. Long-term compatibility

The ISA should remain understandable to both beginners and experienced system programmers while remaining practical for modern computing.

---

## 1.5 Versioning

The first public release of the architecture is named:

Doublers ISA Version 1.0

Future revisions may introduce optional extensions while preserving compatibility with the Base ISA whenever practical.

---

## 1.6 Open Architecture

Doublers is intended to be an open architecture.

Any individual or organization may develop compatible software, tools, simulators, operating systems, compilers, debuggers, or hardware implementations that conform to this specification, subject to the applicable community and licensing rules.

---

## 1.7 Terminology

Throughout this specification:

ISA — Instruction Set Architecture

CPU — Central Processing Unit

Register — A processor storage location.

Opcode — The ternary identifier of an instruction.

Operand — Data supplied to an instruction.

Extension — An optional group of additional instructions beyond the Base ISA.

Trit — A ternary digit representing one of three values: 0, 1, or 2.

---

# Chapter 2 — Architecture Overview

## 2.1 Overview

Doublers is a modern 64-trit Instruction Set Architecture (ISA) designed for operating systems, embedded systems, educational purposes, and general systems programming.

The architecture prioritizes simplicity, consistency, and efficient hardware implementation while remaining extensible through optional ISA extensions.

---

## 2.2 Architecture Summary

| Property | Value |
| --- | --- |
| Architecture Name | Doublers-64 |
| Trit Size | 64 Trits |
| Smallest Addressable Unit | 1 Trit |
| Endianness | Little Endian |
| General Purpose Registers | 16 |
| Special Registers | 4 |
| Address Space | 64-trit |
| Memory Model | Flat |
| Extension Support | Yes |

---

## 2.3 Execution Model

A Doublers-compatible processor executes instructions in the following order:

1. Fetch the instruction from memory.
2. Decode the instruction.
3. Read any required registers or memory operands.
4. Execute the operation.
5. Write the result.
6. Advance the Instruction Pointer (IP) unless modified by the instruction.

This execution model applies to all implementations of the Base ISA.

---

## 2.4 General Purpose Registers

The architecture provides sixteen (16) general-purpose 64-trit registers.

These registers are identified as:

* D0
* D1
* D2
* D3
* D4
* D5
* D6
* D7
* D8
* D9
* D10
* D11
* D12
* D13
* D14
* D15

Unless otherwise specified, any instruction may use any general-purpose register.

---

## 2.5 Special Registers

Every Doublers-compatible processor shall implement the following special registers:

**IP** — Instruction Pointer

Tracks the address of the next instruction to be executed.

**SP** — Stack Pointer

Tracks the top of the active stack.

**BP** — Base Pointer

Provides a stable reference for stack frames.

**FLAGS** — Status Register

Stores status information such as arithmetic results and processor state.

---

## 2.6 Memory Model

Doublers uses a flat memory model.

All memory locations exist within a single linear address space.

Memory is trit-addressable.

The operating system is responsible for memory protection, allocation, and virtual memory management where applicable.

---

## 2.7 Instruction Length

The Base Doublers ISA uses a fixed-length instruction format.

Every Base ISA instruction occupies exactly one instruction word.

A fixed-length encoding simplifies hardware decoding, compiler implementation, and instruction fetching.

The exact ternary layout is defined in Chapter 6.

---

## 2.8 Privilege Levels

The Base ISA defines two privilege levels:

**Kernel Mode**

Provides unrestricted access to privileged instructions and hardware resources.

**User Mode**

Restricts execution of privileged instructions and protects operating system resources.

Operating systems are responsible for managing transitions between privilege levels.

---

## 2.9 Extensions

The architecture supports optional instruction set extensions.

Processors implementing additional instructions shall clearly identify all supported extensions.

Programs shall not assume extension availability unless explicitly required.

---

## 2.10 Compatibility

A processor is considered Doublers-compatible if it correctly implements all mandatory requirements defined by the Base ISA.

Optional extensions shall not alter the behavior of Base ISA instructions.

---

## 2.11 Future Expansion

Doublers is designed as an open Instruction Set Architecture (ISA).

The original creator may not be able to maintain or publish future official versions of this specification.

To encourage continued development, the community is permitted to create compatible extensions, derivative specifications, tools, and hardware implementations, provided that:

* They clearly identify their work as community-created.
* They do not claim to be official Doublers specifications.
* They preserve compatibility with the Doublers Base ISA whenever practical.

The original Doublers ISA v1.0 shall remain the reference foundation for the architecture.

# Chapter 3 — Register Architecture

## 3.1 Overview

The Doublers Base ISA defines sixteen (16) general-purpose registers and four (4) special-purpose registers.

All general-purpose registers are sixty-four (64) trits wide and are equally capable of storing integer values, addresses, or implementation-defined data.

No general-purpose register has a permanently reserved architectural purpose.

---

## 3.2 Register Set

The Base ISA defines the following general-purpose registers:

| Register | Width | Description |
| --- | ---: | --- |
| D0 | 64 Trits | General Purpose Register |
| D1 | 64 Trits | General Purpose Register |
| D2 | 64 Trits | General Purpose Register |
| D3 | 64 Trits | General Purpose Register |
| D4 | 64 Trits | General Purpose Register |
| D5 | 64 Trits | General Purpose Register |
| D6 | 64 Trits | General Purpose Register |
| D7 | 64 Trits | General Purpose Register |
| D8 | 64 Trits | General Purpose Register |
| D9 | 64 Trits | General Purpose Register |
| D10 | 64 Trits | General Purpose Register |
| D11 | 64 Trits | General Purpose Register |
| D12 | 64 Trits | General Purpose Register |
| D13 | 64 Trits | General Purpose Register |
| D14 | 64 Trits | General Purpose Register |
| D15 | 64 Trits | General Purpose Register |

---

## 3.3 Register Width

Each register stores exactly sixty-four (64) trits.

Processors implementing the Base ISA shall not reduce the size of any general-purpose register.

---

## 3.4 Register Usage

General-purpose registers may be used by any instruction unless otherwise specified.

Software is free to assign any purpose to a register.

Operating systems, compilers, and Application Binary Interfaces (ABIs) may define register usage conventions, but such conventions are not part of the Base ISA.

---

## 3.5 Special Registers

Every Doublers-compatible processor shall implement the following special registers.

### Instruction Pointer (IP)

The IP register stores the address of the next instruction to execute.

Control-flow instructions modify the IP directly.

---

### Stack Pointer (SP)

The SP register identifies the top of the current stack.

Stack instructions automatically update the SP register.

---

### Base Pointer (BP)

The BP register provides a stable reference point for stack frames.

Its usage is optional and determined by software.

---

### FLAGS Register

The FLAGS register records the outcome of selected processor operations.

The Base ISA defines the following status flags.

| Flag | Meaning |
| --- | --- |
| Z | Zero Flag |
| C | Carry Flag |
| O | Overflow Flag |
| N | Negative Flag |

Future ISA revisions or extensions may define additional status flags.

---

## 3.6 Register Access

General-purpose registers are readable and writable by all standard instructions.

Special registers may only be modified by instructions defined for that purpose.

Attempting to modify protected registers using undefined instructions results in an Illegal Instruction Exception.

---

## 3.7 Register Reset State

Following processor reset:

* The Instruction Pointer shall point to the platform-defined reset vector.
* The Stack Pointer shall be initialized by the platform firmware or bootloader.
* The FLAGS register shall be initialized to the processor default state.
* The initial values of D0–D15 are implementation-defined.

Software shall not rely on the initial values of general-purpose registers.

---

## 3.8 Reserved Registers

The Base ISA reserves no general-purpose registers.

Future extensions shall not permanently repurpose D0–D15 in a manner that breaks compatibility with existing software.

---

## 3.9 Compliance

A processor shall be considered compliant with this chapter only if it:

* Implements all sixteen general-purpose registers.
* Implements all required special registers.
* Supports sixty-four-trit register operations.
* Preserves the architectural behavior defined in this chapter.

# Chapter 4 — Memory Architecture

## 4.1 Overview

The Doublers Base ISA defines a flat, trit-addressable memory architecture.

Every compatible processor shall access memory using the rules defined in this chapter.

The architecture is designed to remain simple while supporting modern operating systems.

---

## 4.2 Address Space

Doublers-64 defines a sixty-four (64) trit virtual address space.

Each memory location is identified by a unique 64-trit address.

The theoretical address range is:

0x0000000000000000

to

0xFFFFFFFFFFFFFFFF

The actual amount of available memory is implementation-defined.

---

## 4.3 Memory Unit

The smallest addressable memory unit is one (1) trit.

Larger values are formed by combining consecutive trits.

Supported data sizes include:

| Data Type | Size |
| --- | --- |
| Trit | 1 Trit |
| Trit Word | 16 Trits |
| Long Trit Word | 32 Trits |
| Double Trit Word | 64 Trits |

Future ISA extensions may introduce larger data types.

---

## 4.4 Endianness

The Base ISA uses Little-Endian trit ordering.

The least significant trit of a multi-trit value is stored at the lowest memory address.

Processors shall not alter this behavior.

---

## 4.5 Memory Alignment

Natural alignment is recommended.

Examples:

* 16-trit values should be aligned to 2-trit boundaries.
* 32-trit values should be aligned to 4-trit boundaries.
* 64-trit values should be aligned to 8-trit boundaries.

Processors may support unaligned memory access.

If unsupported, an Alignment Exception shall be generated.

---

## 4.6 Memory Access

Memory may be accessed only through instructions defined by the ISA.

Examples include:

* LOAD
* STORE
* PUSH
* POP

Undefined methods of memory access are prohibited.

---

## 4.7 Read and Write Operations

A read operation retrieves data from memory without modifying the stored value.

A write operation replaces the existing value stored at the specified address.

All memory accesses shall obey the privilege rules defined by the operating system.

---

## 4.8 Memory Protection

The Base ISA provides support for protected memory.

The implementation of virtual memory, paging, and permission management is platform-defined.

Operating systems are responsible for enforcing memory protection.

---

## 4.9 Reserved Memory

Processors may reserve implementation-specific memory regions.

Software shall not depend upon reserved memory unless documented by the platform.

---

## 4.10 Stack Memory

The stack grows toward lower memory addresses.

The Stack Pointer (SP) always identifies the current top of the stack.

PUSH decreases the Stack Pointer before storing data.

POP retrieves data before increasing the Stack Pointer.

---

## 4.11 Null Address

The interpretation of address 0x0000000000000000 is platform-defined.

Operating systems may reserve this address to detect invalid memory accesses.

---

## 4.12 Future Expansion

Future ISA extensions may introduce:

* Trit encryption
* Capability-based memory
* Tagged memory
* Persistent memory support

Such extensions shall preserve compatibility with the Base ISA whenever practical.

---

## 4.13 Compliance

A processor is compliant with this chapter if it:

* Implements trit-addressable memory.
* Uses Little-Endian trit ordering.
* Supports 64-trit addressing.
* Correctly performs all defined memory operations.
* Preserves architectural compatibility with the Base ISA.

# Chapter 5 — Instruction Set Architecture

## 5.1 Overview

The Instruction Set Architecture (ISA) defines the complete communication interface between software and the Doublers-64 processor.

Instructions are fixed-size ternary commands executed by the processor. Each instruction specifies an operation, source operands, destination operands, and optional immediate data.

The Doublers-64 ISA is designed with the following goals:

- Simple decoding
- High performance execution
- Easy compiler support
- Future expansion capability
- Strong separation between user and privileged operations

Every valid Doublers-64 processor must implement the base instruction set defined in this chapter.

---

## 5.2 Instruction Size

Doublers-64 uses a fixed-length instruction format.

### Base Instruction Length

| Field | Size |
| --- | ---: |
| Instruction Size | 32 Trits |
| Opcode Field | 8 Trits |
| Register Fields | Variable |
| Immediate Field | Variable |

All instructions are aligned on 4-trit boundaries.

The Instruction Pointer (IP) always points to the next 32-trit instruction.

---

## 5.3 Instruction Encoding

A standard Doublers-64 instruction follows this format:

31 24 23 20 19 16 15 0
+--------------------+---------+---------+-------------------------+
| OPCODE | RD | RS1 | IMM / RS2 |
+--------------------+---------+---------+-------------------------+

### Fields

#### OPCODE (8 trits)

Defines the operation performed by the processor.

Range:

00000000 - 11111111

Total possible instructions:

256 Opcodes

#### RD (4 trits)

Destination register.

Range:

D0 - D15

Used when an instruction writes a result.

#### RS1 (4 trits)

First source register.

Contains the first input operand.

#### IMM / RS2 (16 trits)

This field has two possible meanings:

1. Immediate trit value
2. Second source register and additional control trits

The instruction type determines the interpretation.

---

## 5.4 Instruction Categories

The Doublers-64 instruction set is divided into multiple groups.

| Category | Purpose |
| --- | --- |
| Arithmetic | Mathematical operations |
| Logical | Trit manipulation |
| Memory | Load and store operations |
| Branch | Program flow control |
| System | Processor management |
| Floating Point | Decimal calculations |
| Atomic | Multi-core synchronization |
| Extension | Future expansion |

---

## 5.5 Opcode Organization

Opcode ranges are reserved by category.

| Opcode Range | Category |
| --- | --- |
| 0x00 - 0x1F | Arithmetic |
| 0x20 - 0x3F | Logical |
| 0x40 - 0x5F | Memory |
| 0x60 - 0x7F | Branch & Control |
| 0x80 - 0x9F | System |
| 0xA0 - 0xBF | Floating Point |
| 0xC0 - 0xDF | Atomic Operations |
| 0xE0 - 0xFF | Reserved Extensions |

Reserved instructions must trigger an illegal instruction exception.

---

## 5.6 Arithmetic Instructions

Arithmetic instructions operate on ternary values stored inside general-purpose registers.

### ADD

Operation:

RD = RS1 + RS2

Example:

ADD D1, D2, D3

Meaning:

D1 = D2 + D3

Flags affected:

- Z — Zero
- C — Carry
- O — Overflow
- N — Negative

### SUB

Operation:

RD = RS1 - RS2

Example:

SUB D4, D5, D6

### MUL

Operation:

RD = RS1 × RS2

### DIV

Operation:

RD = RS1 ÷ RS2

Division by zero generates a processor exception.

---

## 5.7 Immediate Arithmetic

Immediate instructions allow constants inside instructions.

### ADDI

Operation:

RD = RS1 + IMM

Example:

ADDI D1, D2, 25

Equivalent:

D1 = D2 + 25

---

## 5.8 Increment and Decrement

### INC

Operation:

RD = RD + 1

### DEC

Operation:

RD = RD - 1

---

## 5.9 No Operation

### NOP

Operation:

No action.

NOP consumes one instruction cycle.

Used for:

- Timing adjustment
- Pipeline alignment
- Debugging

---

## 5.10 Logical Instructions

Logical instructions perform trit-level operations on registers.

These operations are essential for:

- Device control
- Cryptography
- Operating system functions
- Low-level programming

Logical instructions operate on 64-trit values.

### AND

Operation:

RD = RS1 AND RS2

### OR

Operation:

RD = RS1 OR RS2

### XOR

Operation:

RD = RS1 XOR RS2

### NOT

Operation:

RD = NOT RS1

### SHL

Operation:

RD = RS1 << IMM

### SHR

Operation:

RD = RS1 >> IMM

### ROL

Operation:

RD = RotateLeft(RS1, IMM)

### ROR

Operation:

RD = RotateRight(RS1, IMM)

---

## 5.11 Comparison Instructions

Comparison instructions update FLAGS without changing registers.

### CMP

Operation:

FLAGS.Z = (RS1 == RS2)

### TEST

Operation:

FLAGS.Z = (RS1 & RS2) == 0

---

## 5.12 Memory Instructions

### LOAD

Operation:

RD = Memory[RS1 + IMM]

### STORE

Operation:

Memory[RS1 + IMM] = RD

### PUSH

Operation:

SP = SP - 8
Memory[SP] = RD

### POP

Operation:

RD = Memory[SP]
SP = SP + 8

---

## 5.13 Control Flow Instructions

### JMP

Operation:

IP = Address

### CALL

Operation:

SP = SP - 8
Memory[SP] = IP + 4
IP = Address

### RET

Operation:

IP = Memory[SP]
SP = SP + 8

### BEQ

Condition:

IF FLAGS.Z = 1
IP = Address

### BNE

Condition:

IF FLAGS.Z = 0
IP = Address

### BGT

Condition:

IF greater
IP = Address

### BLT

Condition:

IF less
IP = Address

---

## 5.14 System Instructions

System instructions provide direct control over processor features.

These instructions are restricted to privileged execution modes and are primarily used by:

- Operating system kernels
- Hypervisors
- Hardware management software

User applications cannot execute privileged instructions.

Attempting to execute a privileged instruction without permission generates a protection exception.

### MODE

Operation:

Change CPU privilege level

### RSYS

Operation:

RD = System_Register

### WSYS

Operation:

System_Register = RD

### HALT

Operation:

Stop processor execution

### SYSCALL

Operation:

Transfer execution into kernel functionality

---

# Chapter 6 — Execution Environment

## 6.1 Overview

The Execution Environment defines the operational behavior of the Doublers-64 processor.

It describes:

- Instruction execution
- CPU operating modes
- Pipeline behavior
- Exception handling
- Interrupt processing
- Boot sequence
- Processor state management

---

## 6.2 Processor Execution Model

Doublers-64 uses a sequential instruction execution model.

The processor follows this cycle:

FETCH → DECODE → EXECUTE → MEMORY → WRITEBACK

---

## 6.3 Pipeline Hazards

Processors must handle pipeline conflicts.

### Data Hazard

Occurs when one instruction depends on the result of another.

### Control Hazard

Occurs during jumps and branches.

### Memory Hazard

Occurs when multiple operations access memory simultaneously.

---

## 6.4 Processor Operating Modes

Doublers-64 supports three privilege levels.

| Level | Name | Description |
| --- | --- | --- |
| 0 | Kernel Mode | Complete hardware access |
| 1 | Supervisor Mode | OS services |
| 2 | User Mode | Applications |

---

## 6.5 Processor State

The complete CPU state contains:

- General-purpose registers D0–D15
- Control state: IP, SP, BP, FLAGS
- System state: privilege level, interrupt state, memory configuration, exception information

---

## 6.6 Exceptions and Interrupts

If an instruction cannot complete normally, the processor generates an exception.

Examples include:

- Invalid instruction
- Memory violation
- Division by zero
- Privilege violation
- Hardware failure

Interrupts are asynchronous events that temporarily redirect execution to a handler, after which the original context is restored.

---

## 6.7 Boot and Initialization

Immediately after reset:

* The processor shall enter Kernel Mode.
* Interrupts shall be disabled.
* The Instruction Pointer (IP) shall contain the Reset Vector.
* The FLAGS register shall contain its implementation-defined reset value.
* General-purpose registers shall contain implementation-defined values unless otherwise specified by the platform.

---

# Chapter 7 — Base Instruction Set Summary

The Base ISA defines the mandatory instructions that every Doublers-compatible processor shall implement.

These include:

* Data movement: MOVE, LOAD, STORE
* Arithmetic: ADD, SUB, MUL, DIV, MOD, INC, DEC, NEG
* Logical: AND, OR, XOR, NOT, SHL, SHR, ROL, ROR
* Comparison: CMP, TEST
* Control flow: JMP, JE, JNE, JG, JL, JGE, JLE, CALL, RET
* Stack: PUSH, POP
* System: NOP, HALT, SYSCALL, SYSRET, BREAK, WAIT

---

# Chapter 8 — Interrupts and Exceptions

## 8.1 Overview

Interrupts and Exceptions provide a controlled mechanism for altering the normal execution flow of a Doublers-compatible processor.

An interrupt is generated by an external or asynchronous event.

An exception is generated internally during instruction execution.

Every compliant processor shall support both mechanisms.

---

## 8.2 Exception Classes

The Base ISA defines the following exception classes:

* Illegal Instruction
* Divide By Zero
* Invalid Memory Access
* Alignment Fault
* Stack Overflow
* Stack Underflow
* Privilege Exception
* Breakpoint Exception

Future extensions may define additional exception classes.

---

## 8.3 Exception Processing

When an exception occurs, the processor shall:

1. Complete any architecturally required state updates.
2. Save the current execution context.
3. Transfer execution to the appropriate exception handler.
4. Resume execution or terminate execution according to operating system policy.

---

## 8.4 Interrupt Processing

When an interrupt is accepted, the processor shall:

1. Preserve the required execution context.
2. Transfer execution to the interrupt handler.
3. Execute the handler.
4. Restore the saved context.
5. Resume execution.

---

## 8.5 Interrupt Vector Table

Each compatible processor shall provide an Interrupt Vector Table.

The operating system shall initialize this table during system startup.

Each entry shall identify the handler associated with a specific interrupt or exception.

---

# Chapter 9 — Compatibility and Community Additions

## 9.1 Overview

The Doublers ISA is a source-available architecture intended to encourage experimentation, research, and processor development.

Future additions may be created by the community provided they preserve compatibility with the Doublers Base ISA.

---

## 9.2 Base ISA Preservation

The Doublers Base ISA shall remain unchanged.

Existing instructions, registers, exceptions, and architectural behavior defined by the Base ISA shall not be modified.

Software written for the Base ISA should continue to operate correctly on compatible processors.

---

## 9.3 Community Additions

Developers may create additional instructions, registers, or processor capabilities.

Community additions should:

* Clearly document all new functionality.
* Preserve Base ISA behavior.
* Avoid redefining existing instructions.
* State any compatibility requirements.

---

## 9.4 Compatibility Requirements

Community additions shall not:

* Modify existing Base ISA instructions.
* Change register behavior.
* Alter exception handling.
* Break software written for the Base ISA.

Processors that violate these requirements shall not claim compatibility with the Doublers Base ISA.

---

# Chapter 10 — Processor Identification

## 10.1 Overview

Every Doublers-compatible processor shall provide a standardized mechanism for software to identify the processor implementation and supported architectural features.

---

## 10.2 Required Information

A compatible processor shall make the following information available:

* Processor Vendor Name
* Processor Model Name
* Doublers ISA Version
* Supported DCA Version
* Processor Revision
* Supported Community Additions

---

# Chapter 11 — Architectural Limits

## 11.1 Overview

This chapter defines the architectural limits guaranteed by the Doublers Base ISA.

All compatible processors shall satisfy the minimum requirements defined in this chapter.

---

## 11.2 Register Width

The Doublers Base ISA defines a 64-trit architecture.

General-purpose registers shall be 64 trits wide.

---

## 11.3 Address Space

The Base ISA supports a 64-trit virtual address space.

---

## 11.4 Register Count

Every compatible processor shall implement:

* Sixteen General-Purpose Registers.
* Mandatory Special-Purpose Registers.
* Mandatory Status Registers.

---

## 11.5 Privilege Levels

The Base ISA requires support for:

* Kernel Mode
* User Mode

---

# Chapter 12 — Glossary

## 12.1 Definitions

Trit — A ternary digit with one of three possible states: 0, 1, or 2.

ISA — Instruction Set Architecture.

DCA — Doublers Command Architecture.

FLAGS Register — A processor register containing architectural status information describing the result of previous operations.

Kernel Mode — The highest processor privilege level defined by the Base ISA.

User Mode — The restricted processor privilege level intended for application software.

Compatibility — The ability of processors, software, and development tools to correctly implement and execute the behavior defined by the Doublers Base ISA.

---

# Appendix A — Register Reference

## A.1 General-Purpose Registers

The Base ISA defines sixteen 64-trit General-Purpose Registers (GPRs).

| Register | Purpose |
| --- | --- |
| D0 | General-purpose |
| D1 | General-purpose |
| D2 | General-purpose |
| D3 | General-purpose |
| D4 | General-purpose |
| D5 | General-purpose |
| D6 | General-purpose |
| D7 | General-purpose |
| D8 | General-purpose |
| D9 | General-purpose |
| D10 | General-purpose |
| D11 | General-purpose |
| D12 | General-purpose |
| D13 | General-purpose |
| D14 | General-purpose |
| D15 | General-purpose |

---

## A.2 Special-Purpose Registers

| Register | Purpose |
| --- | --- |
| IP | Instruction Pointer |
| SP | Stack Pointer |
| FLAGS | Processor Status Register |

---

# Appendix B — Instruction Reference

## B.1 Arithmetic Instructions

* ADD
* SUB
* MUL
* DIV
* MOD
* INC
* DEC
* NEG

## B.2 Logical Instructions

* AND
* OR
* XOR
* NOT
* SHL
* SHR
* ROL
* ROR

## B.3 Comparison Instructions

* CMP
* TEST

## B.4 Memory Instructions

* LOAD
* STORE
* PUSH
* POP

## B.5 Control Flow Instructions

* JMP
* CALL
* RET
* JE
* JNE
* JG
* JL
* JGE
* JLE

## B.6 System Instructions

* SYSCALL
* BREAK
* NOP
* HALT

---

# Appendix C — Exception Codes

## C.1 Mandatory Exceptions

| Exception | Description |
| --- | --- |
| Illegal Instruction | Invalid or undefined instruction |
| Divide By Zero | Division by zero |
| Memory Protection | Unauthorized memory access |
| Execute Protection | Execution from non-executable memory |
| Privilege Exception | Privileged instruction executed from User Mode |
| Breakpoint | BREAK instruction encountered |
| Debug Exception | Single-step or debugging event |
| Watchpoint | Optional watchpoint event |
| System Call | SYSCALL instruction |
| Interrupt | Hardware or software interrupt |

---

# Appendix D — Reserved Instruction List

Instruction representations not assigned by the Base ISA are reserved.

Reserved instructions shall not be executed by Base ISA software.

Execution of a reserved instruction shall generate an Illegal Instruction Exception unless assigned by a compatible community addition.

---

# Appendix E — Final Note

This document has been updated to use trit-based terminology throughout the ISA specification, replacing bit-focused language with trit-focused terminology while preserving the architectural intent of the original design.

