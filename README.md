# myOS



## Project Structure

```
os/
├── boot/
│   └── boot.asm        # Stage 1 bootloader (512 bytes, loaded at 0x7C00)
├── kernel/
│   ├── kernel.c        # Kernel entry point
│   └── kernel.h        # Core types and declarations
├── drivers/
│   ├── vga.c           # VGA text mode driver (80x25)
│   └── vga.h
├── linker.ld           # Kernel linker script
├── Makefile            # Build system
└── README.md
```

## How It Works

1. **BIOS** loads `boot.asm` into memory at `0x7C00` and jumps to it
2. **Bootloader** reads the kernel from disk into `0x8000` and jumps to it
3. **Kernel** initializes the VGA driver and prints to screen
4. **VGA driver** writes directly to the framebuffer at `0xB8000`

## Building

### Prerequisites

```bash
# Ubuntu/Debian
sudo apt install nasm qemu-system-x86 gcc-multilib binutils

# macOS (via Homebrew)
brew install nasm qemu x86_64-elf-gcc
```

> You'll need a cross-compiler (`i686-elf-gcc`). See the [OSDev wiki](https://wiki.osdev.org/GCC_Cross-Compiler) for setup instructions.

### Build & Run

```bash
make          # build the disk image
make run      # run in QEMU (terminal mode)
make run-gui  # run in QEMU with GUI window
make clean    # remove build artifacts
```

## Roadmap

- [x] Bootloader
- [x] VGA text mode driver
- [ ] GDT (Global Descriptor Table)
- [ ] IDT + interrupt handling
- [ ] Keyboard driver
- [ ] Memory management (paging)
- [ ] Simple shell

## References

- [OSDev Wiki](https://wiki.osdev.org)
- [Intel x86 Manual](https://www.intel.com/content/www/us/en/developer/articles/technical/intel-sdm.html)
- [Writing an OS in Rust](https://os.phil-opp.com) (great concepts even for C)
