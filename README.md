# STM32 Dual Bootloader

A lightweight dual-application bootloader written for the STM32G071RBT6 microcontroller using STM32CubeIDE. This project enables seamless switching between two user applications stored at different flash memory locations.

---

## 🚀 Features

- **Custom Bootloader** at `0x08000000`
- **User Application 1** at `0x08008000`
- **User Application 2** at `0x08010000`
- Vector Table relocation support

---

## 🧠 How It Works

1. **Bootloader** runs at startup and reads a **boot flag** or condition.
2. Based on the flag (or a button GPIO), it jumps to either:
   - App (`0x08008000`)
   - App2 (`0x08010000`)
3. Vector table is remapped dynamically.
4. Control is passed to the selected user application.

---

## 🔧 How to Build and Flash

1. **Create Two User Applications**
   - Use STM32CubeIDE to create `UserApp1` and `UserApp2` as separate projects.
   - Do **not modify** the provided `.ld` (linker script) and `system_stm32g0xx.c` files. Use them as-is for correct vector table offset and memory mapping.
   - You may update these files provided you are using a different development board, in which case based on your Flash size you will have to update the files.

2. **Build All Projects**
   - Build `Bootloader`, `User_App_1`, and `User_App_2` separately in STM32CubeIDE.

3. **Flash the Binaries to the STM32 Board**
   - Use STM32CubeProgrammer or any compatible flashing utility.
   - Flash **Bootloader** binary to: `0x08000000`
   - Flash **UserApp1** binary to: `0x08008000`
   - Flash **UserApp2** binary to: `0x08010000`

---

✅ Once flashed, the bootloader will dynamically jump to either `User_App_1` or `User_App_2` based on your logic, enabling multi-app deployment on a single STM32 board.