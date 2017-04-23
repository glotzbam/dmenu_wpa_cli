# dmenu_wpa_cli

The name pretty much gives it away, doesn't it...

-------------------------------------------------

## About

This tool can be used to activate one of a list
of pre-configured WiFi networks, something
you'd usually do using wpa_cli.

It's thought for users who manage their wifi
connections with wpa_supplicant and netctl,
and like the sparsity of dmenu.
Probably also using some minimalist window
manager like i3, monad or awesome.

It's still pre-alpha, but since it is unable
to change anything in your system besides
the connection state of your wifi, it
should be harmless enough.

Just put it somewhere you'll find it again
and make it executable (+x). Maybe ~/bin.
Usually you'd bind it to some hotkey, which
makes using it much more convenient.

## Troubleshooting

I can, unfortunately, only describe
the process for Arch Linux using systemd.

__dmenu_wpa_cli__, as the name says,
utilizes __dmenu__ as well as __wpa_cli__,
so both of these should be installed in your
system. Furthermore, in order for this to 
work, wpa_cli must have write access to 
the socket used by wpa_supplicant.

To make this work, make sure you enable
__wpa_supplicant@.service__ instead of 
__wpa_supplicant.service__ for your adapter.
So if its udev name is wlan0 for instance,
you use

`systemctl enable wpa_supplicant@wlan0.service`

Aditionally your wpa_supplicant config file
should be named 

`/etc/wpa_supplicant/wpa_supplicant-wlan0.config`

again named after your adapter.

At last you need to pass the group which
has write access to the socket in your
config file. The first line should be
something in the way of

`ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=wifi`

If your user is member of the wifi group,
everything should work just fine.

## TODO

- [ ] command line arguments to configure output and scan timeout
- [ ] menu item to rescan available networks
