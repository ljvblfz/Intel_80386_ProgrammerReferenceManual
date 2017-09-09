# ADD -- Add

| Opcode   | Instruction     | Clocks | Description                                   |
| -------- | :-------------: | :----: | :-------------------------------------------: |
| 04 ib    | ADD AL,imm8     | 2      | Add immediate byte to AL                      |
| 05 iw    | ADD AX,imm16    | 2      | Add immediate word to AX                      |
| 05 id    | ADD EAX,imm32   | 2      | Add immediate dword to EAX                    |
| 80 /0 ib | ADD r/m8,imm8   | 2/7    | Add immediate byte to r/m byte                |
| 81 /0 iw | ADD r/m16,imm16 | 2/7    | Add immediate word to r/m word                |
| 81 /0 id | ADD r/m32,imm32 | 2/7    | Add immediate dword to r/m dword              |
| 83 /0 ib | ADD r/m16,imm8  | 2/7    | Add sign-extended immediate byte to r/m word  |
| 83 /0 ib | ADD r/m32,imm8  | 2/7    | Add sign-extended immediate byte to r/m dword |
| 00 /r    | ADD r/m8,r8     | 2/7    | Add byte register to r/m byte                 |
| 01 /r    | ADD r/m16,r16   | 2/7    | Add word register to r/m word                 |
| 01 /r    | ADD r/m32,r32   | 2/7    | Add dword register to r/m dword               |
| 02 /r    | ADD r8,r/m8     | 2/6    | Add r/m byte to byte register                 |
| 03 /r    | ADD r16,r/m16   | 2/6    | Add r/m word to word register                 |
| 03 /r    | ADD r32,r/m32   | 2/6    | Add r/m dword to dword register               |

## Operation

```
DEST := DEST + SRC;
```

## Description

[ADD](ADD.md) performs an integer addition of the two operands (DEST and SRC). The result of the addition is assigned to the first operand (DEST), and the flags are set accordingly.

When an immediate byte is added to a word or doubleword operand, the immediate value is sign-extended to the size of the word or doubleword operand.

## Flags Affected

OF, SF, ZF, AF, CF, and PF as described in [Appendix C](../appendix/appc.md)

## Protected Mode Exceptions

`#GP(0)` if the result is in a nonwritable segment; `#GP(0)` for an illegal memory operand effective address in the CS, DS, ES, FS, or GS segments; `#SS(0)` for an illegal address in the SS segment; `#PF(fault-code)` for a page fault

## Real Address Mode Exceptions

Interrupt 13 if any part of the operand would lie outside of the effective address space from 0 to 0FFFFH

## Virtual 8086 Mode Exceptions

Same exceptions as in Real Address Mode; `#PF(fault-code)` for a page fault