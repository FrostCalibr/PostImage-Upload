# postimg-upload

A lightweight screenshot-to-link tool. Take a screenshot, automatically upload it to postimages.org, and copy the direct link to your clipboard — all in one keybind.

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


## Note

-Headless mode is intentionally disabled — postimages.org blocks headless browsers. The browser runs on a separate workspace and closes automatically after upload.

-If you need more than copying direct link like Indirect link, markdown etc.. open an issue. 
## License

MIT
