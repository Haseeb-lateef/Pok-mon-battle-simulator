# Pokémon Battle Simulator (STM32 / Nucleo-F031K6)

## 🎮 Overview  
This project is a **Pokémon battle simulator** built on the STM32 Nucleo-F031K6 microcontroller using the **CMSIS framework**.  
It renders graphics to a TFT display, plays sound effects/music, and implements a turn-based combat system where the player can select moves from a menu and battle against a CPU opponent.  

The goal was to combine **embedded systems programming** with **game design mechanics**, resulting in a small-scale but fully interactive Pokémon battle experience.  

---

## 🛠 Features  
- **Graphics Rendering** – custom low-level driver (`display.c`) to draw text, sprites, and animations on a TFT screen.  
- **Sound** – tone generation with `TIM14` timers (`sound.c`, `musical_notes.h`).  
- **Serial Communication** – UART for debugging/logging (`serial.c`).  
- **Combat System** – turn-based battle mechanics between player and CPU Pokémon.  
- **Menu Navigation** – on-screen cursor and input handling for move selection.  

---

## 📂 Project Structure  
```
├── src/
│   ├── main.c            # Core game logic, combat system, menus
│   ├── display.c         # Display driver (TFT graphics)
│   ├── sound.c           # Sound generation
│   ├── serial.c          # UART communication
│   └── prbs.c            # Pseudo-random number generator
│
├── include/
│   ├── display.h
│   ├── sound.h
│   ├── serial.h
│   ├── font5x7.h         # Bitmap font
│   └── musical_notes.h   # Frequencies for notes
│
├── platformio.ini        # PlatformIO build configuration
└── README.md             # Project documentation
```

---

## 🎯 My Role  
I was responsible for **designing and coding the core gameplay mechanics**, specifically:  
- **Combat mechanics** – damage calculation, CPU move selection, attack effects, health bar updates.  
- **Menu mechanics** – move selection system, cursor navigation (`↑/↓`), and input handling.  

You can see this work mainly in:  
- [`main.c`](src/main.c) – functions like `game_loop()`, `pika_moves()`, `charm_moves()`, `cpu_choose_move_char()`, `cpu_choose_move_pika()`, and related combat logic.  
- Menu positioning macros (`INC`, `X`, `START`) and functions (`move_up_func`, `move_down_func`).  

---

## 🚀 How to Build & Run  
### Requirements  
- [PlatformIO](https://platformio.org/)  
- STM32 Nucleo-F031K6 board  
- TFT display connected to GPIOA/SPI1 pins  
- Speaker/buzzer connected to TIM14 output  

### Build & Flash  
```bash
pio run --target upload
```

---

## 📸 Demo  
*(Add screenshots, wiring diagrams, or gameplay photos in the `assets/` folder once available)*  

---

## 👨‍💻 Author  
**Haseeb Lateef**  
- Designed and implemented combat & menu mechanics  
- Integrated gameplay logic with display and sound drivers  
