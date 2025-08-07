# MELD

-------------------------------------------------------------------------------

## MacOS Homebrew

### Install

```
$ brew tap homebrew/cask
$ brew cask install meld
```

-------------------------------------------------------------------------------

## MacOS Macports

### Install

```
$ sudo port install meld
```

### Troubleshooting

- Broken characters and icons
    + Error message

        ```sh
        gi.repository.GLib.Error: gtk-icon-theme-error-quark: Icon 'folder' not present in theme Adwaita (0)
        ```

    + Install `adwaita-icon-theme`

        ```sh
        $ sudo port install adwaita-icon-theme
        ```

-------------------------------------------------------------------------------

## MacOS Meld

- [https://yousseb.github.io/meld/](https://yousseb.github.io/meld/)

### Shell Wrapper

```sh
#!/usr/bin/env sh

/Applications/Meld.app/Contents/MacOS/Meld "$@"
```

-------------------------------------------------------------------------------

## Install from Source

- [https://meldmerge.org/development.html](https://meldmerge.org/development.html)

### Clone

```sh
$ git clone https://gitlab.gnome.org/GNOME/meld.git
```

#### Git Clone error

If SSL verification errors occur behind some firewall configuration, try to disable `http.sslVerify=false`

```sh
$ git -c http.sslVerify=false clone https://gitlab.gnome.org/GNOME/meld.git
```

### Install

Run `setup.py` for install

```sh
$ python3 setup.py install --force --prefix /opt/local --record files.txt
```

### Uninstall

```sh
$ xargs rm -rf < files.txt
```

Note that this uninstall only removes the files, NOT the directories.

### Add site-packges path

Add user `site-packages` path to `usrlocal.pth` in the default `site-packges` path if necessary

```sh
$ echo /opt/local/lib/python3.8/site-packages >> /usr/lib/python3.8/site-packages/usrlocal.pth
```

### Troubleshooting

Missing icons due to unrecognized resource directory

#### Error example

```sh
gi.repository/GLib.Error: g-io-error-quark: Failed to load /usr/local/share/icons/hicolor/16x16/actions/meld-change-apply-right.png: Error opening file /usr/local/share/icons/hicolor/16x16/actions/meld-change-apply-right.png: No such file or directory (1)
```

#### Solution

Set `XDG_DATA_HOME` set `.bashrc` or `.profile`
([https://developer.gnome.org/gtk3/stable/ch32s03.html](https://developer.gnome.org/gtk3/stable/ch32s03.html))

```sh
export XDG_DATA_HOME=/opt/local/share
```

Remove old resource directories

```sh
rm -rf /usr/local/share/icons/*
```

#### Verification

Verification code `gtk_icon_search_path.py`

```python
#!/usr/bin/env python3

import gi

gi.require_version('Gtk', '3.0')

from gi.repository import Gtk
from pprint        import pprint

theme = Gtk.IconTheme.get_default()

# Verify search paths
pprint(Gtk.IconTheme.get_search_path(theme))

# Verify icon loading
pprint(theme.load_icon('meld-change-apply-right', 16, 0))
```

Example output

```sh
$./gtk_icon_search_path.py
dbus[32002]: Dynamic session lookup supported but failed: launchd did not provide a socket path, verify that org.freedesktop.dbus-session.plist is loaded!
['/Users/foo/.local/share/icons',
 '/Users/foo/.icons',
 '/opt/local/share/icons',
 '/usr/local/share/icons',
 '/usr/share/icons',
 '/opt/local/share/pixmaps',
 '/usr/local/share/pixmaps',
 '/usr/share/pixmaps']
```
