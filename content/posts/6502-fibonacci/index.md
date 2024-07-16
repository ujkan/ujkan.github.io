---
title: '6502 Assembly - Fibonacci'
excerpt: New possibilities from old concepts
date: 2024-07-15
permalink: /posts/2024/07/6502-fibonacci
tags:
  - 6502
  - assembly
---
# Introduction
I've been learning some 6502 assembly
([streams](https://www.youtube.com/@ujkansulejmani/streams))
and most recently I implemented a subroutine to calculate the n-th Fibonacci
number.
# What is 6502?

> The MOS Technology 6502 (typically pronounced "sixty-five-oh-two")
> is an 8-bit microprocessor
> L

I implemented a subroutine that calculates the n-th Fibonacci number in
6502 assembly.

Here's the code
```assembly
define N_loc $01fd
define fpp_loc $01fc
define fp_loc $01fb

fib:
  TXA
  PHA             ; stores N in the stack, loc $01fd since $01fe
                  ; and $01ff are ret. address
  LDA #0          ; 1st fibonacci is 0
  PHA
  LDA #1          ; 2nd fibonacci is 1
  PHA
  LDX #2          ; loop counter; i = 2
loop:
  CPX N_loc       ; i == n?
  BEQ fibdone     ; then quit, done

  ; fp = fpp + fp
  LDA fp_loc
  ADC fpp_loc
  STA fp_loc

  ; fpp = fp - fpp
  SEC             ; set carry for subtraction
  LDA fp_loc
  SBC fpp_loc
  STA fpp_loc

  INX             ; i++
  JMP loop

fibdone:
  LDA fp_loc     ; result stored in accumulator
  RTS

```
