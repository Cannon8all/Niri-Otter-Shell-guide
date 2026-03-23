__**This is for Otter-Shell on Niri**__

Install otter-shell
-------------------
```
pikman i otter-shell
pikman i wtype
(wtype is needed to make toggling and the osd work on niri)
Disable and mask the hypridle service
```
Disable the Hypridle sevice
---------------------------
```
killall hypridle
sudo systemctl disable --now hypridle.service
systemctl --user mask hypridle.service
```
Copy your current (noctalia) config.kdl and back it up
------------------------------------------------------
﻿
Remove or comment like below:
-----------------------------
//start-at-startup noctalia-shell/pikabar 
//spawn-at-startup "swww-notifications"
//spawn-at-startup "swww-daemon"
//spawn-at-startup "/usr/bin/mate-polkit"
//spawn-at-startup "systemctl" "--user" "enable" "--now" "hypridle"
also remove the keybind that launches the noctalia/walker launcher

Add
---
spawn-at-startup "otter-bar"
spawn-at-startup "otter-wallpaper"
spawn-at-startup "otter-osd"
spawn-at-startup "otter-notifications"
spawn-at-startup "otter-polkit"
spawn-at-startup "otter-idle"

Keybinds for Otter-OSD: capslock,numlock, volume and brightness
----------------------------------------------------------------
Caps_Lock            allow-when-locked=true { spawn "sh" "-c" "otter-osd caps-lock && wtype -k Caps_Lock"; }
Num_Lock             allow-when-locked=true { spawn "sh" "-c" "otter-osd num-lock && wtype -k Num_Lock"; }
XF86AudioRaiseVolume allow-when-locked=true { spawn "otter-osd" "volume-up" "5"; }
XF86AudioLowerVolume allow-when-locked=true { spawn "otter-osd" "volume-down" "5"; }
XF86AudioMute        allow-when-locked=true { spawn "otter-osd" "volume-mute-toggle"; }
XF86MonBrightnessUp  allow-when-locked=true { spawn "sh" "-c" "brightnessctl set +5% && otter-osd brightness-up"; }
XF86MonBrightnessDown allow-when-locked=true { spawn "sh" "-c" "brightnessctl set 5%- && otter-osd brightness-down"; }
Keybinds for Otter-launcher and Otter-Logout (adjust to your choice)

Various keybinds for otter-launcher,otter-logout
------------------------------------------------
//Spawn and toggle otter-launcher
    Mod+Space { spawn "sh" "-c" "pkill otter-launcher || otter-launcher"; }
//Shutdown-Logout
    Ctrl+Alt+Delete { spawn "otter-logout"; }

Add this as a layer to have the overview blur working correctly
---------------------------------------------------------------
layer-rule {
    match namespace="^otter-wallpaper-overview$"
    place-within-backdrop true
}
