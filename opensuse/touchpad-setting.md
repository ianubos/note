### Install libinput package
[libinput](https://software.opensuse.org/package/libinput) Read this document well!!!   
[good document](https://wiki.archlinux.org/index.php/Libinput#Touchpad_settings_not_taking_effect_in_KDE's_Touchpad_KCM)

### Create touchpad setting file
[source](https://howchoo.com/linux/the-perfect-almost-touchpad-settings-on-linux-2)
/usr/share/X11/xorg.conf.d/50-mtrack.conf
```
Section "InputClass"
        MatchIsTouchpad "on"
        Identifier      "Touchpads"
        Driver          "mtrack"
        Option          "Sensitivity" "0.60"
        Option          "FingerHigh" "5"
        Option          "FingerLow" "1"
        Option          "IgnoreThumb" "true"
        Option          "ThumbRatio" "70"
        Option          "ThumbSize" "25"
        Option          "IgnorePalm" "true"
        Option          "TapButton1" "0"
        Option          "TapButton2" "0"
        Option          "TapButton3" "0"
        Option          "TapButton4" "0"
        Option          "ClickFinger1" "3"
        Option          "ClickFinger2" "3"
        Option          "ClickFinger3" "3"
        Option          "ButtonMoveEmulate" "false"
        Option          "ButtonIntegrated" "true"
        Option          "ClickTime" "25"
        Option          "BottomEdge" "30"
        Option          "SwipeLeftButton" "8"
        Option          "SwipeRightButton" "9"
        Option          "SwipeUpButton" "0"
        Option          "SwipeDownButton" "0"
        Option          "SwipeDistance" "700"
        Option          "ScrollCoastDuration" "500"
        Option          "ScrollCoastEnableSpeed" ".3"
        Option          "ScrollUpButton" "5"
        Option          "ScrollDownButton" "4"
        Option          "ScrollLeftButton" "7"
        Option          "ScrollRightButton" "6"
        Option          "ScrollDistance" "350"
        Option          "ClickMeMethod" "clickfinger"   //I added!
EndSection
```
