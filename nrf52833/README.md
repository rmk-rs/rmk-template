# RMK 

RMK is a feature-rich and easy-to-use keyboard firmware.

## Use the template

To run this firmware, you should have latest Rust installed. [`probe-rs`](https://probe.rs/docs/getting-started/installation/) and [`flip-link`](https://github.com/knurling-rs/flip-link) should also be installed.

After having everything installed, use the following command to run the example:

```
cargo run --release
```

## uf2 support

If your board ships with a UF2 bootloader (such as the Adafruit_nRF52_Bootloader), you can flash without a debug probe. RMK uses the `cargo-make` tool to generate .uf2 firmware, with the generation process defined in the `Makefile.toml`.

1. Get `cargo-make` tool:
   ```shell
   cargo install --force cargo-make
   ```
2. Compile RMK and generate the .uf2 firmware:
   ```shell
   cargo make uf2 --release
   ```
3. Flash

   - Put your board into bootloader mode. A USB drive will appear on your computer.
   - Drag and drop the generated .uf2 firmware file onto the USB drive. The RMK firmware will be automatically flashed onto your microcontroller.

### Memory layout

`memory.x` gives the firmware the whole 512K of flash, which assumes there is no
bootloader. If your board has one, move `FLASH` past it — for the
Adafruit_nRF52_Bootloader that is `ORIGIN = 0x00001000, LENGTH = 508K`, with
`RAM : ORIGIN = 0x20000008, LENGTH = 127K`.

### Additional notes

RMK defaults to USB-priority mode if a USB cable is connected. After flashing, remember to disconnect the USB cable, or [switch to BLE-priority mode](https://rmk.rs/docs/features/wireless.html#multiple-profile-support) by pressing User11(Switch Output) key.
