# 2026-anniversary-badge

[日本語版 README はこちら / Japanese version](./README.md)

This repository contains the firmware, schematics, and assembly guide for the Women Who Go Tokyo 10th Anniversary Badge (a.k.a. `wwgt2026badge`).
It is a workshop kit that combines an RP2040 Zero and TinyGo, designed so you can start from soldering.

> ## Special Thanks
>
> This workshop was produced with significant help from the [**TinyGo Keeb**](https://tinygo-keeb.org/) community.
> We sincerely thank them for generously sharing the sample code, circuit design, and workshop know-how — including the project that served as our base, [tinygo-keeb/workshop-conf2025badge](https://github.com/tinygo-keeb/workshop-conf2025badge).

If anything is unclear, please feel free to ask via an Issue.

## What is in this repository

- `src/` : Sample firmware written in TinyGo
- `wwgt2026badge/` : KiCad project (schematics and PCB data)
- `lib/` : Custom symbol / footprint libraries
- `tools/imgconv/` : Tool to generate RGB565 images for the LCD
- `build/BUILD.md` : Hardware assembly guide (Japanese) / `build/BUILD_EN.md` : Assembly guide (English)

## Schematics

You can view the schematics directly in the browser with KiCanvas.

- [Open in KiCanvas](https://kicanvas.org/?repo=https%3A%2F%2Fgithub.com%2FWomenWhoGoTokyo%2F2026-anniversary-badge%2Ftree%2Fmain%2Fwwgt2026badge)

## Hardware assembly

Soldering instructions, the order of assembly, and the required tools are described in the build guide.

- [Build guide (English)](./build/BUILD_EN.md)
- [ビルドガイド (日本語)](./build/BUILD.md)

# Environment setup

Please refer to [TinyGo Keeb's environment setup section](https://github.com/tinygo-keeb/workshop-conf2025badge#%E7%92%B0%E5%A2%83%E8%A8%AD%E5%AE%9A).


# Target hardware

The microcontroller on this badge is an RP2040 (Cortex M0+), and the MCU board used is the [Waveshare RP2040-Zero](https://www.waveshare.com/wiki/RP2040-Zero). The TinyGo target name is `waveshare-rp2040-zero`.

The main features are as follows.

- Waveshare RP2040-Zero
- ST7789 LCD
- Rotary encoder with LED
- Analog joystick
- Key switches × 2 with RGB LEDs
- Buzzer
- Grove connector

A summary of the pin assignment is shown below. See the schematics for details.

| Function | Pin |
| ---- | ---- |
| Up button | GPIO0 |
| Down button | GPIO1 |
| Rotary encoder A / B | GPIO2 / GPIO3 |
| SK6812MINI-E (WS2812B compatible) | GPIO4 |
| Encoder switch | D5 (GPIO5) |
| Encoder LED | D7 (GPIO7) |
| Buzzer | D8 (GPIO8) PWM4 |
| ST7789 RST / DC / CS / BL | GPIO9 / GPIO12 / GPIO13 / GPIO14 |
| Joystick X / Y | GPIO29 / GPIO28 (ADC) |

# Running the sample firmware

First, clone this repository. All commands below assume you run them from the repository root.

```
$ git clone https://github.com/WomenWhoGoTokyo/2026-anniversary-badge
$ cd 2026-anniversary-badge
```

The samples are placed under `src/` as a flat structure where one file equals one feature. Since multiple files each declare `package main`, you build by **specifying a file directly**, not a directory.

```
$ tinygo build -o out.uf2 --target waveshare-rp2040-zero --size short ./src/blink.go
```

## Build + flash (via bootloader)

If you hold the `BOOT` button on the RP2040 Zero and press the `RESET` button (or unplug and re-plug the USB cable), the bootloader starts and the board appears as an external drive on your PC. From there, you can drag-and-drop a `*.uf2` file to flash it.

This method also works for uf2 files built without TinyGo, so it is convenient when you just want to verify that something runs.

## Build + flash (tinygo flash)

With `tinygo flash` you can build and flash in one step. If no error message is shown, it succeeded.

```
$ tinygo flash --target waveshare-rp2040-zero --size short ./src/blink.go
```

To check serial output, use `tinygo monitor`. If the port cannot be auto-detected, specify it explicitly with `--port`.

```
$ tinygo ports
Port                 ID        Boards
COM7                 2E8A:000A waveshare-rp2040-zero

$ tinygo monitor --port COM7
```

You can also run both at once with `tinygo flash --monitor`, but in some environments the port is detected incorrectly. If it does not work well, run them separately.

# List of samples

`src/` contains the following samples. Each can be flashed with `tinygo flash --target waveshare-rp2040-zero ./src/<filename>`.

| File | Description |
| -------- |------------------------------------|
| `blink.go` | Blink the rotary encoder LED |
| `sk6812.go` | Light up the RGB LEDs under the key switches in sequence |
| `key_input.go` | Detect presses of the up and down keys |
| `rotary.go` | Read the rotation value of the rotary encoder |
| `encorder_sw.go` | Detect a press of the rotary encoder |
| `joystick.go` | Read XY values from the analog joystick |
| `st7789_txt.go` | Display text on the ST7789 LCD |
| `buzzer.go` | Play do-re-mi-fa-sol-la-ti-do on the buzzer |
| `all.go` | A demo that combines all features (logo display + input-driven LEDs + buzzer) |

## Blink (blink.go)

Blinks the rotary encoder LED (D7) once per second.

```
$ tinygo flash --target waveshare-rp2040-zero --size short ./src/blink.go
```

If the LED lights up, it works. Try changing the value passed to `time.Sleep` to adjust the blink rate.

## RGB LED (sk6812.go)

There are two SK6812MINI-E LEDs on the board. With `WriteRaw([]uint32{...})` you can control multiple LEDs at once.

```
$ tinygo flash --target waveshare-rp2040-zero --size short ./src/sk6812.go
```

Colors are specified as uint32, with 8 bits each from the most significant side representing Green / Red / Blue / (White, for SK6812 RGBW).

```go
colors := []uint32{
    0xFFFFFFFF, // white
    0xFF0000FF, // green
    0x00FF00FF, // red
    0x0000FFFF, // blue
}
```

## Key input (key_input.go)

Reads the two up/down keys as GPIO inputs on the microcontroller. They are pulled up, so the line goes Low when a key is pressed.

```
$ tinygo flash --target waveshare-rp2040-zero --size short ./src/key_input.go
$ tinygo monitor
The top button was pressed
The bottom button was pressed
```

## Rotary encoder (rotary.go)

Uses the Quadrature driver from `tinygo.org/x/drivers/encoders`.

```
$ tinygo flash --target waveshare-rp2040-zero --size short ./src/rotary.go
$ tinygo monitor
value:  -1
value:  0
value:  1
```

## Encoder switch (encorder_sw.go)

The rotary encoder also acts as a button when pressed in. It simply detects a Low signal on GPIO5.

```
$ tinygo flash --target waveshare-rp2040-zero --size short ./src/encorder_sw.go
$ tinygo monitor
encorder sw is pressed!!
```

## Analog joystick (joystick.go)

Reads the two XY axes via ADC and shows them in hexadecimal. When idle, the displayed value should be around `0x8000`.

```
$ tinygo flash --target waveshare-rp2040-zero --size short ./src/joystick.go
$ tinygo monitor
8000 8000
6E10 7E10
```

## LCD (st7789_txt.go)

Combines `tinygo.org/x/drivers/st7789` and `tinygo.org/x/tinyfont` to display text on the LCD.

```
$ tinygo flash --target waveshare-rp2040-zero --size short ./src/st7789_txt.go
```

When flashing succeeds, "Hello / Gophers!" is shown on the LCD.

To display an image, convert a PNG to RGB565 format with `tools/imgconv`, then embed it with `go:embed`.

```
$ go run ./tools/imgconv -in src/images/badge240.png -out src/images/badge.rgb565
```

## Buzzer (buzzer.go)

Drives the buzzer by toggling a GPIO and plays do-re-mi-fa-sol-la-ti-do.

```
$ tinygo flash --target waveshare-rp2040-zero --size short ./src/buzzer.go
```

In `all.go` the implementation uses PWM. For applications that keep the buzzer sounding for a long time, the PWM approach keeps CPU usage lower.

## Full-feature demo (all.go)

An "all-in-one" demo that shows the logo on the LCD, drives the RGB LEDs in sync with input, displays rainbow colors based on joystick direction, toggles the buzzer on/off when the encoder is pressed, and rotates the LCD display when the encoder is rotated.

```
$ tinygo flash --target waveshare-rp2040-zero --size short ./src/all.go
```

# References

- [tinygo-keeb/workshop-conf2025badge](https://github.com/tinygo-keeb/workshop-conf2025badge) — The workshop on which this repository is based
- [Make your own keyboard using sago35/tinygo-keyboard (Japanese)](https://qiita.com/sago35/items/b008ed03cd403742e7aa)
- [koebiten — A 2D game engine for TinyGo](https://github.com/sago35/koebiten)
- [Embedded development with TinyGo from the basics (Japanese)](https://sago35.hatenablog.com/entry/2022/11/04/230919)
