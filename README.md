# Project Name

## Overview

This repository contains two main components implemented in C:

1. **Production Line Sorting & Dispatch Simulation** (see `src/main.c`):  
   A console program that reads product data from four input files (`data/line*.txt`), sorts each set of products by weight using Quick Sort, merges them into a single dispatch list, and allows the user to search for a product by its weight. This demonstrates sorting, merging and binary search algorithms on structured data.

2. **STM32 Display & Sound Drivers** (see `src/display.c`, `src/serial.c`, `src/sound.c`):  
   Low–level drivers for the STM32F031K6 microcontroller. These modules initialise and control a 1.8″ SPI TFT display, provide simple drawing primitives, and generate musical notes via PWM. Header files live in the `include/` directory. The code is configured to build with PlatformIO (`platformio.ini`) targeting the `nucleo_f031k6` board with the CMSIS framework.

> 📁 **Assets:** An `assets/` folder is included for storing images, icons, or other binary resources used by your project. This README is text–only; to avoid hitting upload limits in this environment, no sample images are included. When cloning or using this repository locally, place your binary assets in the `assets/` directory and reference them from your code or documentation as needed.

## File Layout

```
organized_project/
│
├── platformio.ini        # PlatformIO build configuration for the STM32 target
├── README.md             # This documentation
├── .gitignore            # Git ignore rules (see below)
│
├── src/                  # C source files
│   ├── main.c            # Production line sorting demo
│   ├── display.c         # Display driver for SPI TFT
│   ├── serial.c          # UART initialisation and I/O routines
│   ├── sound.c           # Simple PWM–based sound output
│   └── prbs.c            # (Unused) pseudorandom bit sequence generator
│
├── include/              # C header files
│   ├── display.h         # API for the display driver
│   ├── serial.h          # API for serial routines
│   ├── sound.h           # API for sound routines
│   ├── musical_notes.h   # Note frequencies for the sound module
│   └── font5x7.h         # 5×7 bitmap font used by the display driver
│
├── data/                 # Input data for the sorting demo
│   ├── line1.txt         # Product records for line 1
│   ├── line2.txt         # Product records for line 2
│   ├── line3.txt         # Product records for line 3
│   └── line4.txt         # Product records for line 4
│
├── assets/               # Placeholder for images, icons, and other binary assets
└── docs/                 # Future documentation, schematics, diagrams, etc.
```

The `include/` folder is the correct place for header files that are shared between source files. According to PlatformIO’s project structure guidelines, you should place C declarations and macros in `include` so they can be included from files in `src` via `#include "headername.h"`【80737660153482†L121-L129】. Source files live in `src`, and any private libraries belong in a `lib/` subfolder.

## Building (STM32F031K6)

This project uses [PlatformIO](https://platformio.org/). To build the microcontroller code:

1. Install PlatformIO CLI or use the PlatformIO extension in your IDE.
2. Clone this repository and navigate into it.
3. Run:

```bash
pio run
```

PlatformIO reads the `platformio.ini` file, selects the `nucleo_f031k6` environment, and compiles the code in `src/` and `include/`. The resulting firmware binary will be placed in `.pio/build/nucleo_f031k6/`.

To flash the firmware to your Nucleo board:

```bash
pio run --target upload
```

Ensure that you have the ST-Link drivers installed and the board is connected via USB.

## Running the Sorting Demo

To exercise the product sorting program on your development machine:

1. Compile `src/main.c` with a C compiler. For example, using GCC:

```bash
gcc src/main.c -o sorting_demo
```

2. Ensure that the input files in `data/` are present in the current working directory.
3. Run the program:

```bash
./sorting_demo
```

The program will print the sorted products from each line to the terminal. The call to display the combined dispatch list and perform a binary search is currently commented out in `main.c`; you can uncomment `output_dispatchlist_search` in `main()` to test that functionality.

## Notes on Assets

Large images or binary assets can quickly exceed the file size limits on some hosting platforms. To keep this repository lightweight, the `assets/` directory is empty by default. If your project uses images (e.g., for display splash screens or README diagrams), place them in `assets/` and reference them using relative paths. For large binary files you don’t want to track in Git, consider using [Git LFS](https://git-lfs.github.com/).

## Contributing

Feel free to open issues or submit pull requests if you improve the code, add features, or fix bugs. Please follow standard C coding conventions and document any new functions in the corresponding header files.

---