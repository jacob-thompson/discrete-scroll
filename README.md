# DiscreteScroll

<img src="https://github.com/emreyolcu/discrete-scroll/blob/icon/icon.png?raw=true" align="right" width="35%">

[![Downloads](https://img.shields.io/github/downloads/emreyolcu/discrete-scroll/total.svg)](https://github.com/emreyolcu/discrete-scroll/releases)

This small utility fixes macOS's unnecessary scroll wheel acceleration.
It runs in the background, allowing you to scroll
a constant number of lines with each notch of the wheel.

### Supported versions

As of November 2024, this application works on macOS versions 10.9–15.0.

### Installation

You may download the binary [here](https://github.com/emreyolcu/discrete-scroll/releases/download/v1.2.1/DiscreteScroll.zip).
DiscreteScroll requires access to accessibility features.
Upon startup, if it does not have access, it will prompt you and wait.
You do not need to restart the application
after you grant it access to accessibility features.

> [!CAUTION]
> You should not revoke accessibility access
> for DiscreteScroll while it is running.
> Otherwise, your mouse might become unresponsive, requiring a reboot to fix.

If you want the application to run automatically when you log in,
do the following:

1. On macOS 13.0 and later, go to `System Settings > General > Login Items`;
   otherwise, go to `System Preferences > Users & Groups > Login Items`.
2. Add `DiscreteScroll` to the list.

If you want to quit the application, either run `killall DiscreteScroll`
or do the following:

1. Launch `Activity Monitor`.
2. Search for `DiscreteScroll` and select it.
3. Click the stop button in the upper-left corner and choose Quit.

### Configuration

The default behavior is to scroll 3 lines with each notch of the wheel.
If you want to change this, run the following command,
replacing `LINES` with the number of lines to scroll with each notch.
This number may even be negative, which inverts scrolling direction.

```
defaults write com.emreyolcu.DiscreteScroll lines -int LINES
```

> [!WARNING]
> If you set `lines` to some value other than an integer,
> then the default value of 3 is used as a fallback.

You may configure exception applications if you do not want DiscreteScroll to run on every application. Running this command repeatedly will append its arguments to the existing list of exception applications. Replace `APPLICATION` with the name of the exception application you would like to configure, e.g. `Finder`.
```
defaults write com.emreyolcu.DiscreteScroll except -array-add "APPLICATION"
```

You should restart the application for changes in settings to take effect.

### Uninstallation

To uninstall DiscreteScroll, quit the application, move it to trash,
and remove it from the lists for accessibility access and login items.
You can remove any stored preferences by running the following:

```
defaults delete com.emreyolcu.DiscreteScroll
```

### Potential problems

Recent versions of macOS have made it difficult to run unsigned binaries.

If you experience issues launching the application, try the following:

- Remove the quarantine attribute by running the command
  `xattr -dr com.apple.quarantine /path/to/DiscreteScroll.app`,
  where the path points to the application bundle.
- Disable Gatekeeper by running the command
  `spctl --add /path/to/DiscreteScroll.app`,
  where the path points to the application bundle.

If on startup the application asks for accessibility permissions
even though you have previously granted it access, try the following:

1. On macOS 13.0 and later, go to `System Settings > Privacy & Security > Accessibility`;
   otherwise, go to `System Preferences > Security & Privacy > Privacy > Accessibility`.
2. Remove `DiscreteScroll` from the list and add it again.

### History

#### v1.2.1 (2024-06-05)

- **Fix:** Release event tap and run loop source after adding source.

#### v1.2.0 (2024-06-02)

- Remove accessibility observer once granted access.

#### v1.1.0 (2024-05-31)

- Observe changes in accessibility access continuously.

#### v1.0.1 (2024-05-28)

- **Fix:** Fall back to defaults if user preference is set to incorrect type.

#### v1.0.0 (2024-05-26)

- Handle errors and check for accessibility access.
- Allow configuring the number of lines scrolled per notch.

#### v0.1.1 (2016-10-29)

- **Fix:** Use point delta instead of line delta.

#### v0.1.0 (2016-10-25)

- Initial release.
