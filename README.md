# fn-backlight

This is a custom way to change the backlight on systems for which xbacklight
can't find outputs because they don't live at `/sys/class/backlight`. Such
systems have backlight controls at a subdir such as
`/sys/class/backlight/intel_backlight`. This script provides a wrapper interface
to those backlight controls.

This was written with the purpose of binding the backlight controls to media
keys in systems which, by their choice of window manager, don't have automatic
function key mapping, as is the case with Awesome and i3. For these cases, this
script can be mapped with `xbindkeys` to provide the same functionality -- see below.

## Installation

Be sure to edit the script for your system's values, namely the location of the
dir that contains the `brightness` and `max_brightness` files, as well as the
step for raising/lowering and the minimum brightness value that you want.

This script needs to be run with sudo, since it directly edits the
`/sys/class/backlight/intel_backlight/brightness` file. You'll want to add a
line to your /etc/sudoers file so that you don't need to input the password
every time:

    username ALL = (root) NOPASSWD:/home/username/bin/fn-backlight

This example presumes you've placed the script inside `~/bin/`.

## Usage

```bash
    # raise
    fn-backlight up
    # lower
    fn-backlight down
    # set to maximum level
    fn-backlight max
    # get the current value in percent
    fn-backlight info
    # toggle between minimum value and 50%
    fn-backlight toggle
```

## Mapping function keys with xbindkeys

This is an example config file for `xbindkeys` to map function keys appropriately:

```
"sudo ~/bin/fn-backlight up"
  XF86MonBrightnessUp
"sudo ~/bin/fn-backlight down"
  XF86MonBrightnessDown
"sudo ~/bin/fn-backlight toggle"
  m:0x8 + c:70
```

It was written for a Lenovo U31-70; run `xbindkeys --key` to find your own
system's key codes and alter your config accordingly.

