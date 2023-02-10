# Display improvements for the Corne-ish Zen keyboard

This note details the changes made to the Zen and ZMK codebase to improve the experience of e-ink displays.

## Getting the changes
You can test out below changes using your Zen config repo by modifying your `config/west.yml` file, following [ZMK instructions](https://zmk.dev/docs/features/beta-testing):
```yaml
manifest:
  remotes:
    - name: caksoylar
      url-base: https://github.com/caksoylar
  projects:
    - name: zmk
      remote: caksoylar
      revision: caksoylar/zen-v2  # custom branch name
      import: app/west.yml
  self:
    path: config
```
...or alternatively, you can cherry-pick specific commits noted below to your own fork of ZMK.

### Branches
The improvements for Corne-ish Zen v2 (for R3 of the GB) are in the [`caksoylar/zen-v2`](https://github.com/caksoylar/zmk/commits/caksoylar/zen-v2) branch of my ZMK fork.
For convenience there is also a [`caksoylar/zen-v2+mouse`](https://github.com/caksoylar/zmk/commits/caksoylar/zen-v2+mouse) branch with the mouse keys feature incorporated from `ftc/mouse-ftc` branch.

If you have a v1 PCB (for R1 & R2) you can use [`caksoylar/zen-v1+v2`](https://github.com/caksoylar/zmk/commits/caksoylar/zen-unified) branch instead, which merges below changes with the Corne-ish Zen V1 PR to ZMK: zmkfirmware/zmk#1593.
(Note that you need to use `corneish_zen_v1_left` and `corneish_zen_v1_right` as the board names when building.)

## Details of improvements
Below are the details of improvements, some are always in effect and some require setting corresponding config to be enabled, as detailed below.

1. Avoid unnecessarily refreshing the battery level widget (reduce ghosting)
    - https://github.com/caksoylar/zmk/commit/1573d72
2. Tweak battery level thresholds so the battery levels are more "accurate"
    - https://github.com/caksoylar/zmk/commit/a59384b
3. Add option to hide layer changes that are momentary (using `&mo`, `&lt` etc.) from the layer widget (reduces the number of partial refreshes)
    - https://github.com/caksoylar/zmk/commit/2fb683a and https://github.com/caksoylar/zmk/commit/92a984
    - Add `CONFIG_ZMK_DISPLAY_HIDE_MOMENTARY_LAYERS=y` to your `corneish_zen.conf` file to enable
4. Add a periodic full display refresh (to clear up ghosting) using zmkfirmware/zmk#969
    - https://github.com/caksoylar/zmk/commit/4b9a004
    - Add `CONFIG_ZMK_DISPLAY_FULL_REFRESH_PERIOD=N` to your `corneish_zen.conf` file to refresh every `N` seconds
5. Add option to invert displays to white-on-black instead of black-on-white
    - https://github.com/caksoylar/zmk/commit/52b86a7
    - Add `CONFIG_IL0323_INVERT=y` to your `corneish_zen.conf` file to enable
6. Add option to hide the "LAYER" heading in the layer widget and realign all widgets
    - https://github.com/caksoylar/zmk/commit/c4dfd6f
    - Add `CONFIG_CUSTOM_WIDGET_LAYER_STATUS_HIDE_HEADING=y` to your `corneish_zen.conf` file to enable
7. Add options to select different logo images to replace the "Corne-ish Zen" logo on the right half, from @manna-harbour:
    - https://github.com/caksoylar/zmk/commit/a3aac19
    - `CONFIG_CUSTOM_WIDGET_LOGO_IMAGE_ZMK=y` for ZMK logo instead of Zen
    - `CONFIG_CUSTOM_WIDGET_LOGO_IMAGE_LPKB=y` for LowProKB logo
    - `CONFIG_CUSTOM_WIDGET_LOGO_IMAGE_MIRYOKU=y` for Miryoku logo
8. @aumuell's driver tweak to reduce ghosting for partial refreshes
    - https://github.com/zmkfirmware/zmk/commit/48376a2

## Contact
Feel free to contact me on Discord `bravekarma#4601` or you can open an issue in https://github.com/caksoylar/zmk as well.
