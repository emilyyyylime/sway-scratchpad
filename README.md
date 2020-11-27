i3-scratchpad
=============
>The Swiss Army Knife of floating i3 windows

![Sample Gif](https://gitlab.com/aquator/i3-scratchpad/-/raw/master/sample.gif)

Features
--------
- Start applications in specified size and position
- Multi monitor support
- Relative sizing based on screen size
- Anchor points: set distances relative to screen edges, or center
- Toggle mode: the same command will hide the window if it is displayed
- Wraps command line apps to URxvt terminal

Usage
-----
```
Usage: i3-scratchpad [[-s <screen>] [-a <anchor>] [-d <size>] [-p <pos>]] [-u [-w][-o <opts>]] [-t] [-m <edge>] <command>
Executes a program in a positioned scratchpad, optionally wrapped in a URxvt window.
Caches optional URxvt wrapper script and stores window id at XDG_RUNTIME_DIR based on command,
so executing the same command will re-use the existing window, if it still exists.

Arguments:
 -h            Prints this help page.
 -s <screen>   Screen identifier, as listed in xrandr. Falls back to primary screen.
 -d <size>     Dimensions of window in pixels, in WIDTHxHEIGHT format.
               Percentages of the screen dimensions can be used as well. Default is 50%x50%
 -p <pos>      Position of terminal on pixels, in X,Y format.
               Negative values can be used as well. Default is 0,0
 -a <anchor>   Sets where to calculate position from. Valid values are
               top-left, top-center, top-right
               center-left, center-center, center-right
               bottom-left, bottom-center, bottom-right
               Can be shortened as: tl, tc, tr, cl, cc, cr, bl, bc, br
               Position will be calculated from anchor point of screen to anchor
               point of window. Default is center-center.
 -m <edge>     Animates the movement to target position from specified edge.
               Valid values are top, left, bottom, right, or short t, l, b, r
 -u            Use URxvt terminal to launch the command - for command line apps.
 -o <opts>     Extra URxvt options to pass.
 -w            Hides the cursor and waits for keypress before closing the
               terminal window. Useful for commands immediately returning.
 -t            Toggles the window.

Example:
 # Calendar at the bottom right of primary screen with 32px bottom margin:
 $ i3-scratchpad -d200x200 -abr -p0,-32 -wtu cal
```

Installation
------------
You can just download the script file. You can also find it at [AUR](https://aur.archlinux.org/packages/i3-scratchpad-git/). (Thanks tami for contribution)

Requirements
------------
Created for [i3wm] in [Bash]. Uses **xrandr** and **wmctrl** for positioning and toggling. [URxvt] or fork is needed for command line wrapper. Bash **sleep** extension is required for animation, the scripts tries to load that automatically. General tools like **sed**, **grep** and **cat** are also used.

Examples
--------
#### Terminal + i3
Create a drop-down terminal with `i3-scratchpad -tmt -atc urxvt +transparent` Use of real transparency is advised for best effect.
Configuration of i3 to toggle the terminal with $mod+Tab:
```
# Toggle dropdown terminal
bindsym $mod+Tab exec --no-startup-id "i3-scratchpad -tmt -atc urxvt +transparent"
```

#### Terminal + Polybar
Fly a calendar into picture with `i3-scratchpad -d200x200 -abr -p0,-50 -wtuo +transparent -mb cal`
You can hook that up to a polybar date module:
```ini
[module/my-calendar]
type = custom/script
exec = printf '%%{A1:i3-scratchpad -d200x200 -abr -p0,-50 -wtuo +transparent -mb cal:}%s%%{A}' "$(date +%Y-%m-%d)"
```

#### Browser
Want an Apple Music Player? Sure thing.
```shell
i3-scratchpad -s DP-1  -d900x500 -p0,0 -mr -tatr -- brave --app=https://music.apple.com/en/browse
```

[Brave] is a [Chromium] based browser, check your browser's options for a standalone new window run.

License
-------
This is free and unencumbered software released into the public domain.

Anyone is free to copy, modify, publish, use, compile, sell, or
distribute this software, either in source code form or as a compiled
binary, for any purpose, commercial or non-commercial, and by any
means.

In jurisdictions that recognize copyright laws, the author or authors
of this software dedicate any and all copyright interest in the
software to the public domain. We make this dedication for the benefit
of the public at large and to the detriment of our heirs and
successors. We intend this dedication to be an overt act of
relinquishment in perpetuity of all present and future rights to this
software under copyright law.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS BE LIABLE FOR ANY CLAIM, DAMAGES OR
OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE,
ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
OTHER DEALINGS IN THE SOFTWARE.

For more information, please refer to <http://unlicense.org/>


[i3wm]: https://i3wm.org/
[Bash]: https://www.gnu.org/software/bash/
[URxvt]: http://software.schmorp.de/pkg/rxvt-unicode.html
[Brave]: https://brave.com/
[Chromium]: https://www.chromium.org/
