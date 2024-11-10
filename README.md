# Amiga Workbench 1.0 Style Look For Labwc

## labwc + waybar
![Screenshot](/labwc-screenshot.png "Title")

## Config

### labwc

- $HOME/.config/labwc/autostart
- Set Background Color
```
# Set background
swaybg -c '#0055AA' >/dev/null 2>&1 &
```

***

- $HOME/.config/labwc/rc.xml
- Disable Root Mouse Event
```
  <mouse>
    <default />
    <context name="Root">
      <mousebind button="Left" action="Press">
        <action name=" " />
      </mousebind>
      <mousebind button="Right" action="Press">
        <action name=" " />
      </mousebind>
      <mousebind button="Middle" action="Press">
        <action name=" " />
      </mousebind>
    </context>
  </mouse>
```

***

- $HOME/.config/labwc/themerc-override
- Look Color
```
window.active.border.color: #FFFFFF
window.inactive.border.color: #C0C0C0
window.active.title.bg.color: #FFFFFF
window.inactive.title.bg.color: #C0C0C0
window.button.width: 128
window.button.height: 128
window.button.spacing: 0
window.active.button.unpressed.image.color: #0055AA
window.inactive.button.unpressed.image.color: #0055AA
window.active.label.text.color: #0055AA
window.inactive.label.text.color: #0055AA
window.button.width: 32
window.button.height: 32
window.active.shadow.size: 80
window.inactive.shadow.size: 60
window.active.shadow.color: #0055AA40
window.inactive.shadow.color: #00000040
menu.items.bg.color: #FFFFFF
menu.items.text.color: #0055AA
menu.items.active.bg.color: #F08000
menu.items.active.text.color: #FFFFFF
menu.separator.color: #0055AA
menu.title.bg.color: #FFFFFF
menu.title.text.color: #0055AA
osd.bg.color: #FFFFFF
```

### waybar

- $HOME/.config/waybar/config
```
{
	   "layer": "top",
           "spacing": 5,
           "height": 40,
	   "modules-left": ["wlr/taskbar"],
           "modules-right": ["custom/pacman", "tray", "clock", "image#logout", "image#reboot", "image#poweroff"],
           "wlr/taskbar": {
                "format": "{icon} {title}",
                "icon-theme": "Adwaita",
                "icon-size": 16,
                "active-first": true,
                "on-click": "activate",
                "on-click-middle": "close",
           },
           "custom/pacman": {
                "format": "{} | ",
                "interval": "21600",
                "exec": "curl wttr.in/Busan?format=3",
                "on-click": "flatpak run org.gnome.Weather",
           },
           "tray": {
                "icon-size": 16,
                "spacing": 10,
           },
           "clock": {
		"interval": 60,
                "format": "<b>{:%H:%M}</b>",
                "tooltip-format": "{:%Y %m-%d %R (%a)}",
                "on-click": "flatpak run org.gnome.Calendar",
           },
           "image#logout": {
                "path": "/usr/share/icons/Adwaita/symbolic/actions/system-log-out-symbolic.svg",
                "size": 16,
                "on-click": "/usr/local/bin/system-power-control.sh logout",
           },
           "image#reboot": {
                "path": "/usr/share/icons/Adwaita/symbolic/actions/system-reboot-symbolic.svg",
                "size": 16,
                "on-click": "/usr/local/bin/system-power-control.sh reboot",
           },
           "image#poweroff": {
                "path": "/usr/share/icons/Adwaita/symbolic/actions/system-shutdown-symbolic.svg",
                "size": 16,
                "on-click": "/usr/local/bin//system-power-control.sh poweroff",
           }
}
```

***

- $HOME/.config/waybar/style.css
```
* {
    border: none;
    border-radius: 0;
    font-size: 16px;
    background: #FFFFFF;
    color: #0055AA;
}

#taskbar button {
    border-right: 1px solid #0055AA;
    font-weight: normal;
}

#taskbar button.active {
    border-bottom: 8px solid #F08000;
    font-weight: bold;
}
```

### Session Script

- /usr/local/bin/system-power-control.sh
```
#!/bin/sh

COMMAND=$1

[[ z$COMMAND == "z" ]] && echo "$0 [reboot|poweroff|logout]" && exit 0

if [[ $COMMAND == "reboot" ]]
then
	MASSSAGE='Would you like to restart the system??'
	RUN_CMD="sudo systemctl $COMMAND"
elif [[ $COMMAND == "poweroff" ]]
then
	MASSSAGE='Would you like to shut down the system?'
	RUN_CMD="sudo systemctl $COMMAND"
elif [[ $COMMAND == "logout" ]]
then
	MASSSAGE='Would you like to shut down the logout'
	[[ ${DESKTOP_SESSION} == "labwc" ]] && RUN_CMD="labwc -e"
else
	echo "$0 [reboot|poweroff]" && exit 0
fi

zenity --question --title= --text="${MASSSAGE}" --no-wrap --default-cancel && ${RUN_CMD}
```







