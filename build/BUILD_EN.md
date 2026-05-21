# 2026-anniversary-badge Build Guide

[日本語版ビルドガイド / Japanese version](./BUILD.md)

This document describes the assembly procedure for the Women Who Go Tokyo 10th Anniversary Badge (`wwgt2026badge`). If you have some experience with soldering, it should take about 1 to 2 hours to complete.

## Parts list

![](./images/001.jpg)

| No | Part                                                                                                                                                 | Qty | Notes                |
| -- |----------------------------------------------------------------------------------------------------------------------------------------------------| ---- |----------------------|
| 1  | PCB                                                                                                                                                | 1 |                      |
| 2  | [RP2040 Zero](https://ja.aliexpress.com/item/1005008186242400.html)                                                                                | 1 | Waveshare RP2040-Zero |
| 3  | [Joystick](https://akizukidenshi.com/catalog/g/g104048/)                                                                                           | 1 | Analog, 2-axis       |
| 4  | [ST7789 LCD](https://ja.aliexpress.com/item/1005009249695645.html)                                                                                 | 1 | 240 × 240            |
| 5  | [Pull-up resistors](https://akizukidenshi.com/catalog/g/g116332/)                                                                                  | 2 | 470Ω to 1kΩ          |
| 6  | [Key switches](https://shop.yushakobo.jp/collections/all-switches)                                                                                 | 2 | MX compatible        |
| 7  | [Keycaps](https://shop.yushakobo.jp/collections/keycaps?sort_by=created-descending&filter.v.availability=1&filter.v.price.gte=&filter.v.price.lte=)| 2 |                      |
| 8  | [Key sockets](https://shop.yushakobo.jp/products/a01ps?variant=37665172521121)                                                                     | 2 | MX socket            |
| 9  | [Rotary encoder with LED](https://akizukidenshi.com/catalog/g/g105771/)                                                                            | 1 | EC11 compatible      |
| 10 | [RGB LEDs](https://akizukidenshi.com/catalog/g/g115478/)                                                                                           | 2 | SK6812MINI-E         |
| 11 | [Buzzer](https://akizukidenshi.com/catalog/g/g104118/)                                                                                             | 1 |                      |
| 12 | [Grove connector](https://akizukidenshi.com/catalog/g/g112634/)                                                                                    | 1 |                      |
| 13 | [Pin socket 9-pin](https://akizukidenshi.com/catalog/g/g110100/)                                                                                   | 2 | For RP2040 Zero      |
| 14 | [Pin socket 5-pin](https://akizukidenshi.com/catalog/g/g102762/)                                                                                   | 1 | For RP2040 Zero      |
| ~~15~~ | ~~[Pin socket 8-pin](https://akizukidenshi.com/catalog/g/g103785/)~~                                                                                   | ~~1~~ | ~~For ST7789 LCD~~       |
| 16 | Hat                                                                                                                                                | 1 | For the joystick     |
| 17 | Switch plate                                                                                                                                       | 1 |                      |
| 18 | Bottom plate                                                                                                                                       | 1 |                      |
| 19 | Wood screws                                                                                                                                        | 2 | 2.1 × 10             |

## Required tools

- Soldering iron (temperature-controlled preferred)
- Solder (leaded or lead-free)
- Tweezers
- Nippers (to trim the leads of components such as resistors)
- Masking tape (for temporary fixing)
- Phillips screwdriver (to fasten the plate with wood screws)
- Tester / multimeter (for verification — optional)

## Overall assembly flow

The general flow is as follows.

1. Solder surface-mount components (from the lowest profile parts first)
2. Solder through-hole components
3. Mount the RP2040 Zero, ST7789, and joystick
4. Flash the firmware and verify the operation
5. Attach the plates, keycaps, encoder knob, and joystick hat to finish

Keep in mind the principle of "components soldered earlier should not get in the way of components attached later" to work safely.

---

## Step 0. Preparation

Prepare a workbench.
If you do not have a workbench, fix the PCB on some kind of stand.

{image}

The side with a space to write your name (the white rectangle in the lower middle) is the `front`, and the side with the QR code is the `back`.

## ![Working face - Back](https://img.shields.io/badge/Working_face-Back-a42e4f) Step 1. Solder the resistors

There is no polarity. Insert the resistors from the front.
If you care about the orientation, adjust as you like.

Flip the PCB over and solder from the back.
First, solder just one pin of one resistor. Then check the position carefully; if anything looks off, reflow and adjust.
If you are unsure how to adjust, call a support staff member.

Once soldering is done, trim the leads short (within 1 mm).
When cutting, hold the lead with your finger so that the offcut does not fly off.


## ![Working face - Back](https://img.shields.io/badge/Working_face-Back-a42e4f) Step 2. Solder the RGB LEDs

For each RGB LED, the **notch (mark) on the corner of the package** is on the pin 1 (DIN) side. Align the notch with the corner on the silkscreen on the PCB.

Pre-tin one pad, place the part with tweezers, then apply the iron to fix it.
Verify the position and orientation; if it is misaligned, remelt the solder and adjust.

Solder the remaining three pins.
Both LEDs must be installed in the same orientation.

These parts are heat-sensitive, so be careful not to keep the iron on them for too long.


## ![Working face - Back](https://img.shields.io/badge/Working_face-Back-a42e4f) Step 3. Solder the key sockets

Place the MX-compatible key sockets on the back side of the PCB, aligned with the silkscreen, at the two locations.

> **⚠ Watch the orientation**
> MX sockets can be inserted upside down. Make sure the orientation matches the photo.

Solder just one pin first.
The terminals are thick, so heat the pad (PCB side) well before flowing solder.
While the solder is still molten, press the socket against the PCB with your finger so that it sits flat.
Verify the position and orientation; remelt and adjust if necessary.

Solder the other pin to finish.
Install the second socket the same way.


## ![Working face - Back](https://img.shields.io/badge/Working_face-Back-a42e4f) Step 4. Solder the Grove connector

Insert the Grove connector from the front side of the PCB.
After inserting it, you will flip the board over and solder from the back, so secure it with masking tape.

Solder just one pin first.
Verify the position and orientation; remelt and adjust if necessary.

Next, solder the pin on the diagonal (so that 2 pins are now fixed).
Check again that the body is not lifted or tilted.

Solder the remaining pins to finish.


## ![Working face - Back](https://img.shields.io/badge/Working_face-Back-a42e4f) Step 5. Solder the pin sockets

Install the following pin sockets on the front side of the PCB.

- **9-pin × 2 + 5-pin × 1** : for the RP2040 Zero
- ~~**8-pin × 1** : for the ST7789 LCD~~

If a pin socket is lifted or tilted, the component plugged into it later will sit at an angle. Some effort is needed to keep them vertical.

The recommended approach is to insert the matching pin header (the legs on the RP2040 Zero or the ST7789 LCD) into the pin socket first and use it as a jig. This keeps the pin socket upright.

Solder only the pins at each end first.
Flip the PCB over and check from the side that the pin socket is flush with the PCB and stands vertically.
If it is not vertical, remelt the solder and adjust.

Once you confirm it is vertical, solder the remaining pins to finish.


## ![Working face - Back](https://img.shields.io/badge/Working_face-Back-a42e4f) Step 6. Solder the rotary encoder

Insert the rotary encoder with LED into the front of the PCB.

Make sure the body sits flush against the PCB.
Flip the board over and solder.


## ![Working face - Back](https://img.shields.io/badge/Working_face-Back-a42e4f) Step 7. Solder the buzzer

Insert the through-hole buzzer into the front of the PCB.
There is no polarity.

Tack-solder one leg.
Make sure the body is pressed firmly against the PCB; remelt and adjust if necessary.

Solder the other leg to finish.


## ![Working face - Front](https://img.shields.io/badge/Working_face-Front-2ea44f) Step 8. Mount the microcontroller (RP2040 Zero)

Using the pin header that comes with the RP2040 Zero, and using the pin sockets installed in Step 5 as a jig, solder the microcontroller in a vertical orientation.

First, insert the pin header into the pin sockets on the PCB.
**At this point, do not solder the pin header to either the PCB or the microcontroller.**
The pin sockets are used as a jig to keep the pin header vertical.

Place the microcontroller on top of it, oriented as in the photo.
**The side with the USB-C connector and the white BOOT button facing up is the front.**

Solder just one pin from the top side.
Check the position and tilt; if the microcontroller is not vertical, remelt and adjust.

Once it is vertical, solder the remaining pins from the top side.


## ![Working face - Front](https://img.shields.io/badge/Working_face-Front-2ea44f) Step 9. Install the ST7789 LCD

~~Insert the ST7789 LCD module into the **8-pin pin socket** installed in Step 5. No soldering is required.~~

~~The pin header that comes with the LCD module fits directly into the 8-pin pin socket.~~
**Make sure the display side faces forward (towards the front of the badge).**
Be careful not to put pressure on the flexible cable or the display face with your fingers.

Once inserted, check from the side that the LCD is not tilted and is parallel to the PCB.


## ![Working face - Back](https://img.shields.io/badge/Working_face-Back-a42e4f) Step 10. Install the joystick

Insert the joystick module into the front of the PCB.

Flip the board over and solder just one pin first.
From the front side, check that the body is not lifted or tilted; remelt and adjust if necessary.

Solder the remaining pins to finish.

This completes the basic hardware build.
Before attaching the plates, be sure to run the verification in Step 11.

---

## Step 11. Verification (firmware flashing)

> **📅 For participants of the workshop on May 30, 2026**
> The RP2040 Zero we hand out on the day will come with verification firmware pre-flashed.
> So at the workshop you can skip the firmware-flashing steps below and go straight to verification.
> Refer to the steps below if you want to reflash the firmware at home, or to overwrite the pre-flashed firmware.

Always verify the operation once before attaching the plates.

```
$ git clone https://github.com/WomenWhoGoTokyo/2026-anniversary-badge
$ cd 2026-anniversary-badge
$ tinygo flash --target waveshare-rp2040-zero --size short ./src/all.go
```

The checkpoints after flashing are listed below. They are based on the behavior of `./src/all.go`.

| Check item | Expected behavior |
| -------- | ------------ |
| ST7789 LCD | A logo image is shown right after startup |
| Encoder LED | Keeps blinking at 1-second intervals |
| Press the up key | The 2 RGB LEDs light up in cherry-blossom pink. They turn off when released. |
| Press the down key | The 2 RGB LEDs light up in light blue. They turn off when released. |
| Press up and down keys at the same time | The RGB LEDs show an intermediate color blending cherry-blossom pink and light blue |
| Tilt the joystick | Depending on the direction, the RGB LEDs change to one of 7 rainbow colors (soft red / orange / yellow / green / cyan / blue / purple) |
| Rotate the encoder | The logo on the LCD rotates by 15 degrees per click |
| Press the encoder | Toggles the buzzer ON / OFF. While ON, do-re-mi-fa-sol-la-ti-do keeps repeating. |

Using a serial monitor (`tinygo monitor`) alongside, you can also check the internal state.

| Action | Example serial output |
| ---- | -------------- |
| Startup | `joystick: 8000 8000 (init)` |
| Press the up key | `The top button was pressed` |
| Press the down key | `The bottom button was pressed` |
| Rotate the encoder | `rotary: 1 angle: 15` |
| Press the encoder | `buzzer ON` / `buzzer OFF` (toggles each press) |
| Tilt the joystick fully | XY values such as `joystick: 6E10 7E30` |

If something does not work, refer to the "Troubleshooting" section below.

---

## Step 12. Final hardware assembly

Once verification is done, move on to assembling the case.

1. **Fit the switch plate**
    Before plugging in the key switches, place the switch plate on top of the PCB. Confirm the orientation of the plate using the silkscreen and the hole positions on the PCB.
2. **Insert the key switches**
    Push the key switches through the plate into the MX sockets on the PCB. Make sure the pins are not bent before inserting.
3. **Attach the keycaps**
    Put the keycaps on the switches.
4. **Attach the encoder knob**
    Push the knob that comes with the rotary encoder onto the shaft.
5. **Attach the joystick hat**
    Place the hat on top of the joystick stick.
6. **Attach the bottom plate**
    Place the bottom plate against the back of the PCB and fasten it with the two included **wood screws (2.1 × 10)**. Tighten the screws slowly with a Phillips screwdriver. Tightening too much can crack the plate or warp the PCB, so be careful.

That's it — your badge is done.

---

## Appendix : Replacing the image data

If you want to change the logo image shown on the LCD, use `tools/imgconv` to convert a PNG to RGB565.

```
$ go run ./tools/imgconv -in src/images/badge240.png -out src/images/badge.rgb565
```

Replace `src/images/badge240.png` with your favorite 240 × 240 image, run the command, and then reflash with `tinygo flash`.
