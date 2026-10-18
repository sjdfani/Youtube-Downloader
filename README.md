# YouTube Downloader

A desktop application for downloading YouTube videos, built with **Python**, **PyQt5** and **pytube**.

> **Status:** work in progress. The core flow (fetch video info → pick a resolution → download) works, but some
> parts of the UI are not wired up yet. See [Known limitations](#known-limitations).

## Features

- Frameless, draggable window with a custom dark gradient theme
- Internet connection check before starting
- Fetches video details from a YouTube link:
  - Title
  - Duration
  - View count
  - Rating
- Lists the available MP4 resolutions for the video (1080p, 720p, 480p, 360p, 144p) and shows the file size of
  the selected one
- Lets you choose the destination folder
- Downloads in a background thread so the UI stays responsive

## How it works

The app has three steps, shown as tabs at the top of the window:

1. **YouTube URL** – paste a video link and press submit. The video's title, duration, views and rating appear.
   Press **Next** to continue.
2. **Setting** – choose a resolution from the list (the download size is shown) and pick a destination folder
   with **Browse**. Press **Download** and confirm.
3. **Download** – the video is saved as an MP4 file to the chosen folder.

## Project structure

```
Youtube-downloader/
├── Source/
│   ├── main.py        # Entry point and application logic
│   ├── homePage.py    # Generated UI for the welcome screen
│   └── youtube.py     # Generated UI for the URL / Setting / Download pages
├── photo/             # Icons and images used by the UI
├── requrments.txt     # Python dependencies
└── README.md
```

`homePage.py` and `youtube.py` are generated from Qt Designer `.ui` files with `pyuic5`.

## Requirements

- Python 3.7 or newer
- The packages listed in `requrments.txt`
- [`pytube`](https://pypi.org/project/pytube/) (used for downloading, but not listed in `requrments.txt`)

## Installation

```bash
git clone https://github.com/sjdfani/Youtube-downloader.git
cd Youtube-downloader

# Optional: create a virtual environment
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate

pip install -r requrments.txt
pip install pytube
```

## Usage

Run the app from the **repository root**, because the UI loads its images from the relative `photo/` folder:

```bash
python Source/main.py
```

## Known limitations

- The download progress bar is not connected yet; progress is only printed to the console.
- The **Back**, **First page**, **Home page**, **Open** and **Go file location** buttons have no actions yet.
- The window icon path uses a Windows-style separator (`photo\youtube.png`), so the icon may not show on macOS
  or Linux.
- Only progressive MP4 streams (video and audio in one file) are offered, so higher resolutions may not be
  available for some videos.
- YouTube changes its site often, which can break `pytube`. If fetching a video fails, upgrade it with
  `pip install --upgrade pytube`.

## Author

**Sajjad Fani** – [@sjdfani](https://github.com/sjdfani)
