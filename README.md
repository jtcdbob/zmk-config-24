# How to update firmware
## Make updates to keymap and create an artifact
1. Update the `config/manuform.keymap` file
2. Commit and push the change to trigger the github Action
3. Download the artifact file from the latest build

## Flash the firmware
4. Unzip the artifact file to get two files to flash the firmware
5. Connect the keyboard
6. Set the keyboard into bootloader mode
  a. Use the key combo (eg. CONF + bootloader).
  b. Alternatively, use the microcontroller pins (connect the RST + GND quickly twice in a row).
7. Add the corresponding file to the new volume

# Special keys
[https://zmk.dev/docs/keymaps](https://zmk.dev/docs/keymaps)

Some keys to keep in mind:
* `&mo NAV` to change to `NAV` layer when the key is held down
* `&mt LGUI SPACE` to send `cmd (LGUI)` when the key is held down and send `SPACE` when the key is tapped
* `&sys_reset` resets the keyboard and forces a reconnection
  * To pair the halves for the first time, the keyboard needs to reset at the same time
  * Usually no more pairing is needed after the intial setup
* `&bt BT_SEL 0` selects the bluetooth profile `0`
* `&bt BT_CLR` clears the curent bluetooth profile. Remember to forget the connection on the device as well or it may keep sending signals that may jam the keyboard.
  * To repair the keyboard to a device, the bluetooth profile needs to be cleared on both the keyboard and the device, or the credentials will not match

NOTE: The right half doesn't act as a central, so physical RST + GND may be needed to trigger bootloader for flashing.

# Configurations
The current configs are set in `config/board/shields/manuform/manuform_left(right).conf` files. The TIMEOUT values can be tweaked to reduce the interrupts when the keyboard is idle for a while.
```
CONFIG_ZMK_SLEEP=y
CONFIG_ZMK_IDLE_TIMEOUT=20000
CONFIG_ZMK_IDLE_SLEEP_TIMEOUT=180000
```

It will reduce the battery life but should be fine in general. The [Power Profiler](https://zmk.dev/power-profiler) can estimate the battery life:
* `board: nice!nano v2`
* `split: True`
* `battery size: 820 mAh`
