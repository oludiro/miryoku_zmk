# Ahokore firmware builds

- Enable mouse keys with `CONFIG_ZMK_POINTING=y` for every Ahokore build. The flag is a build input, not currently saved in `config/ahokore.conf`; a build can succeed without working mouse keys if it is omitted.
- The last working build used board `ahokore` and ZMK branch `zmkfirmware/zmk/v0.3-branch`. To reproduce it from the desired pushed Git ref:

  ```sh
  gh workflow run build-inputs.yml --repo <owner>/<repo> --ref <ref> \
    -f board=ahokore -f branches=zmkfirmware/zmk/v0.3-branch \
    -f kconfig=CONFIG_ZMK_POINTING=y
  ```

- Check that the workflow succeeds and its logs show the pointing flag before providing the `zmk.uf2` artifact for flashing. A successful build does not verify operation on the keyboard.
- The user confirmed the mouse speed in `config/ahokore.keymap`: `ZMK_POINTING_DEFAULT_MOVE_VAL 2000` and `U_MOUSE_MOVE_TIME 750` (milliseconds). Preserve these settings unless asked to change them.
