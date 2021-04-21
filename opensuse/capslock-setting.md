### Convert Capslock to language !
1. [Look for the key switch](https://tldp.org/HOWTO/Intkeyb/x772.html)  
2. [Make key swap file and add authority](https://ictsolved.github.io/remap-key-in-linux/)  
swap.desktop
```
[Desktop Entry]
Name=Swap
Exec=xmodmap -e "keycode 96 = Caps_Lock" && xmodmap -e "keycode 66 = F12"
Terminal=false
Type=Application 
```
