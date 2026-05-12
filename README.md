# postimg-upload

A lightweight screenshot-to-link tool for Hyprland. Take a screenshot, automatically upload it to postimages.org, and copy the direct link to your clipboard — all in one keybind.

## How it works

1. `grimblast` captures a screen region and saves it
2. Playwright uploads it to postimages.org via a headless browser
3. The direct link is copied to your clipboard with `wl-copy`
4. Optionally, a desktop notification is shown

## Dependencies

- Python 3
- [grimblast](https://github.com/hyprwm/contrib/tree/main/grimblast)
- [wl-copy](https://github.com/bugaevc/wl-clipboard) (`wl-clipboard`)
- [Playwright for Python](https://playwright.dev/python/)

Install Python dependencies:

```bash
pip install playwright
playwright install chromium
```

## Setup

1. Clone the repo:

```bash
git clone https://github.com/yourusername/postimg-upload.git
cd postimg-upload
```

2. Edit the config section at the top of `postimg-upload.py`:

```python
SAVE_DIR = os.path.expanduser("~/Pictures/Screenshots")  # Where screenshots are saved
SCREENSHOT_CMD = "grimblast", "copysave", "area"         # Screenshot command
CLIPBOARD_CMD = "wl-copy"                                # Clipboard tool
NOTIFY = True                                            # Show notification after upload
```

3. Add a keybind in your `hyprland.conf`:

```
bind = SUPER SHIFT, S, exec, python /path/to/postimg-upload.py
```

4. Add a windowrule to keep the browser out of your way:

```
windowrule {
    name = postimg-browser
    match:title = ^(.*)Google Chrome for Testing(.*)$
    workspace = 7 silent
}
```

5. Optionally set the screenshots directory as default for all grimblast keybinds in `hyprland.conf`:

```
env = XDG_SCREENSHOTS_DIR,$HOME/Pictures/Screenshots
```

## Note

Headless mode is intentionally disabled — postimages.org blocks headless browsers. The browser runs on a separate workspace and closes automatically after upload.

## License

MIT
