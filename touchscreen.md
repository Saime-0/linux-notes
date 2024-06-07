## rotate screen orietation with input
install deps
```bash
-S xorg-xrandr xorg-xinput
```

create script and run
```bash
echo '#!/bin/bash
xrandr --output eDP-1 --rotate normal
xinput set-prop <TouchscreenName> --type=float "Coordinate Transformation Matrix" 1 0 0 0 1 0 0 0 1' | sudo tee /etc/local/bin/rotate-normal

echo '#!/bin/bash
xrandr --output eDP-1 --rotate left
xinput set-prop <TouchscreenName> --type=float "Coordinate Transformation Matrix" 0 -1 1 1 0 0 0 0 1' | sudo tee /etc/local/bin/rotate-left

echo '#!/bin/bash
xrandr --output eDP-1 --rotate right
xinput set-prop <TouchscreenName> --type=float "Coordinate Transformation Matrix" 0 1 0 -1 0 1 0 0 1' | sudo tee /etc/local/bin/rotate-right

echo '#!/bin/bash
xrandr --output eDP-1 --rotate inverted
xinput set-prop <TouchscreenName> --type=float "Coordinate Transformation Matrix" -1 0 1 0 -1 1 0 0 1' | sudo tee /etc/local/bin/rotate-inverted

```
