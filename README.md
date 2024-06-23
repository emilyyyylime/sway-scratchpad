sway-scratchpad
=============
>Your Swiss Army Knife for toggleable floating windows on Sway or i3

![Sample Gif](raw/master/sample.gif)

Features
--------
- Start applications in specified size and position
- Multi monitor support
- Relative sizing based on screen size
- Anchor points: set distances relative to screen edges, or center
- Toggle mode: the same command will hide the window if it is displayed

Usage
-----
```
Usage: sway-scratchpad [-a <anchor>] [-d <size>] [-p <pos>] [-s <screen>] [-m <edge>] [-w <wm>] [-h] [-t] [-v] [-V] <command>
Executes a program in a positioned scratchpad window.
Marks windows for the command arguments, so executing the same command will re-use the existing window, if it still exists.

Arguments:
 -a <anchor>   Sets where to calculate position from. Valid values are combinations of {top,centre,bottom} and
               {left,centre,right}, separated by "-". (Example: centre-right). Can be shortened as: tl, tr, etc.
               Position will then be calculated from the anchor point on the screen to that same anchor
               point on the window. Default is centre-centre.
 -d <size>     Dimensions of window in pixels, in WIDTHxHEIGHT format.
               Percentages of the screen dimensions can be used as well. Default is 50%x50%
 -h            Prints this help page.
 -m <edge>     Animates the movement to target position from specified edge.
               Valid values are top, left, bottom, right / t, l, b, r.
 -p <pos>      Position of window on pixels, in X,Y format. Negative values can be used as well. Default is 0,0.
 -s <screen>   Screen identifier, as listed in xrandr. Falls back to focused screen (sway) or primary screen (i3).
 -t            Toggles the window.
 -v            Verbose, for debugging.
 -V            Print version information.
 -w [sway|i3]  Which window manager to use.
 <command>     Command to execute in order to open window, if it doesn't exist.

Example:
 # Popdown seethrough terminal (kitty)
 bindsym $mod+Ctrl+Return exec --no-startup-id sway-scratchpad -t -mt -atc -d 60%x60% -- kitty --override background_opacity=0.7
```

Installation
------------
You can just download the script file and add it to your `$PATH`. You can also find it at [TODO: AUR](#placeholder).

Requirements
------------
Created for [swaywm] in [Bash], but fully supports [i3wm] as well.
Bash **sleep** extension is required for animation, the script tries to load that automatically.
General tools like **jq**, **sed**, **md5sum**, **which** and **pgrep** are also used.

Examples
--------
#### Dropdown terminal
Create a drop-down terminal with `sway-scratchpad -tmt -atc kitty -o background_opacity=0.7`. Use of real transparency is recommended for best effect.
Configuration of i3/sway to toggle the terminal with $mod+Ctrl+Return:
```
# Toggle dropdown terminal
bindsym $mod+Ctrl+Return exec --no-startup-id "sway-scratchpad -tmt -atc kitty -o background_opacity=0.7"
```

#### Browser
Want an Apple Music Player? Sure thing.
```shell
sway-scratchpad -d900x500 -p0,0 -mr -tatr -- brave --app=https://music.apple.com/en/browse
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


[swaywm]: https://swaywm.org/
[i3wm]: https://i3wm.org/
[Bash]: https://www.gnu.org/software/bash/
[Brave]: https://brave.com/
[Chromium]: https://www.chromium.org/
