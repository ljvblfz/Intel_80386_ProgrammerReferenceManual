# AAD -- ASCII Adjust AX before Division

| Opcode | Instruction | Clocks | Description                     |
| ------ | :---------: | :----: | :-----------------------------: |
| D5 0A  | AAD         | 19     | ASCII adjust AX before division |

## Operation

```
AL := AH * 10 + AL;
AH := 0;
```

## Description

[AAD](AAD.md) is used to prepare two unpacked BCD digits (the least-significant digit in AL, the most-significant digit in AH) for a division operation that will yield an unpacked result. This is accomplished by setting AL to AL + (10 * AH), and then setting AH to 0. AX is then equal to the binary equivalent of the original unpacked two-digit number.

## Flags Affected

SF, ZF, and PF as described in [Appendix C](../appendix/appc.md); OF, AF, and CF are undefined

## Protected Mode Exceptions

None

## Real Address Mode Exceptions

None

## Virtual 8086 Mode Exceptions

None