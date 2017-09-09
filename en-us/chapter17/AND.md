# AND -- Logical AND

| Opcode   | Instruction     | Clocks | Description                                     |
| -------- | :-------------: | :----: | :---------------------------------------------: |
| 24 ib    | AND AL,imm8     | 2      | AND immediate byte to AL                        |
| 25 iw    | AND AX,imm16    | 2      | AND immediate word to AX                        |
| 25 id    | AND EAX,imm32   | 2      | AND immediate dword to EAX                      |
| 80 /4 ib | AND r/m8,imm8   | 2/7    | AND immediate byte to r/m byte                  |
| 81 /4 iw | AND r/m16,imm16 | 2/7    | AND immediate word to r/m word                  |
| 81 /4 id | AND r/m32,imm32 | 2/7    | AND immediate dword to r/m dword                |
| 83 /4 ib | AND r/m16,imm8  | 2/7    | AND sign-extended immediate byte with r/m word  |
| 83 /4 ib | AND r/m32,imm8  | 2/7    | AND sign-extended immediate byte with r/m dword |
| 20 /r    | AND r/m8,r8     | 2/7    | AND byte register to r/m byte                   |
| 21 /r    | AND r/m16,r16   | 2/7    | AND word register to r/m word                   |
| 21 /r    | AND r/m32,r32   | 2/7    | AND dword register to r/m dword                 |
| 22 /r    | AND r8,r/m8     | 2/6    | AND r/m byte to byte register                   |
| 23 /r    | AND r16,r/m16   | 2/6    | AND r/m word to word register                   |
| 23 /r    | AND r32,r/m32   | 2/6    | AND r/m dword to dword register                 |

## Operation

```
DEST := DEST AND SRC;
CF := 0;
OF := 0;
```

## Description

Each bit of the result of the [AND](AND.md) instruction is a 1 if both corresponding bits of the operands are 1; otherwise, it becomes a 0.

## Flags Affected

CF := 0, OF := 0; PF, SF, and ZF as described in [Appendix C](../appendix/appc.md)

## Protected Mode Exceptions

`#GP(0)` if the result is in a nonwritable segment; `#GP(0)` for an illegal memory operand effective address in the CS, DS, ES, FS, or GS segments; `#SS(0)` for an illegal address in the SS segment; `#PF(fault-code)` for a page fault

## Real Address Mode Exceptions

Interrupt 13 if any part of the operand would lie outside of the effective address space from 0 to 0FFFFH

## Virtual 8086 Mode Exceptions

Same exceptions as in Real Address Mode; `#PF(fault-code)` for a page fault