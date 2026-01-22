# Suit Sprint  
### C + x86 Assembly (IA-32, AT&T Syntax)

A small terminal-based game written in **C** with core logic implemented in **32-bit x86 Assembly**.  
Each round randomly selects a suit, moves it upward on a grid, and the first suit to reach the top wins.

---

## Overview

- **Language:** C + IA-32 Assembly  
- **Architecture:** 32-bit (x86)  
- **Interface:** Terminal  
- **Purpose:** Educational project demonstrating C ↔ Assembly integration

---

## Game Rules

- The board is a **5 × 4 grid**
- Columns represent suits:
  - `H` – Hearts
  - `S` – Spades
  - `D` – Diamonds
  - `C` – Clubs
- All suits start on the **bottom row**
- Each draw:
  1. Generates a pseudo-random number (Assembly RNG)
  2. Selects a suit
  3. Moves that suit **up one row**
- The first suit to reach **row 0** wins
- Player can restart or exit after each round

---

## Example Output

. . . .
. . . .
. . . .
. . . .
H S D C
Drawn: S7
. S . .
. . . .
. . . .
. . . .
H . D C
Winner: S


---

## Assembly Responsibilities

The following functions are implemented in **x86 Assembly**:

- `asm_seed(int seed)`  
  Stores the random seed in global memory

- `asm_rand()`  
  Linear Congruential Generator (LCG)  
seed = seed * 1103515245 + 12345

- `asm_move_logo(int suit, int *positions)`  
Moves the selected suit up by one row

- `asm_check_win(int *positions)`  
Returns the winning suit index, or `-1` if no winner

---

## Project Files

├── main.c # Game logic & display (C)
├── asm.s # RNG, movement, win check (Assembly)
├── README.md
└── Makefile


---

## Build & Run

### Requirements

- GCC with **32-bit multilib support**
- Linux / WSL recommended

Install multilib (Ubuntu/Debian):
```bash
sudo apt update
sudo apt install gcc-multilib


gcc -m32 main.c asm.s -o run
or using Makefile:
make


./run


all:
	gcc -m32 main.c asm.s -o run

clean:
	rm -f run


Notes
This project must be compiled as 32-bit (-m32)
Designed for learning:
C ↔ Assembly calling conventions
Stack frames
Pointer passing
Low-level RNG implementation
Uses AT&T syntax, not Intel syntax
