## rotate screen orietation with input
install deps
```bash
-S xorg-xrandr xorg-xinput
```

create script and run
```bash
cat > /etc/local/bin/rotate-normal <<EOL
#!/bin/bash
xrandr --output eDP-1 --rotate normal
xinput set-prop <TouchscreenName> --type=float "Coordinate Transformation Matrix" 1 0 0 0 1 0 0 0 1
EOL

cat > /etc/local/bin/rotate-left <<EOL
#!/bin/bash
xrandr --output eDP-1 --rotate left
xinput set-prop <TouchscreenName> --type=float "Coordinate Transformation Matrix" 0 -1 1 1 0 0 0 0 1
EOL

cat > /etc/local/bin/rotate-right <<EOL
#!/bin/bash
xrandr --output eDP-1 --rotate right
xinput set-prop <TouchscreenName> --type=float "Coordinate Transformation Matrix" 0 1 0 -1 0 1 0 0 1
EOL

cat > /etc/local/bin/rotate-inverted <<EOL
#!/bin/bash
xrandr --output eDP-1 --rotate inverted
xinput set-prop <TouchscreenName> --type=float "Coordinate Transformation Matrix" -1 0 1 0 -1 1 0 0 1
EOL
```
