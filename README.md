# metavenom
Image EXIF metadata extractor - from devive to geolocation
# MetaVenom

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.8+-blue?style=for-the-badge&logo=python&logoColor=white">
  <img src="https://img.shields.io/badge/Platform-Linux%20%7C%20macOS%20%7C%20Windows-informational?style=for-the-badge">
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge">
  <img src="https://img.shields.io/badge/OSINT-Tool-red?style=for-the-badge">
</p>

```
  ███╗   ███╗███████╗████████╗ █████╗ ██╗   ██╗███████╗███╗   ██╗ ██████╗ ███╗   ███╗
  ████╗ ████║██╔════╝╚══██╔══╝██╔══██╗██║   ██║██╔════╝████╗  ██║██╔═══██╗████╗ ████║
  ██╔████╔██║█████╗     ██║   ███████║██║   ██║█████╗  ██╔██╗ ██║██║   ██║██╔████╔██║
  ██║╚██╔╝██║██╔══╝     ██║   ██╔══██║╚██╗ ██╔╝██╔══╝  ██║╚██╗██║██║   ██║██║╚██╔╝██║
  ██║ ╚═╝ ██║███████╗   ██║   ██║  ██║ ╚████╔╝ ███████╗██║ ╚████║╚██████╔╝██║ ╚═╝ ██║
  ╚═╝     ╚═╝╚══════╝   ╚═╝   ╚═╝  ╚═╝  ╚═══╝  ╚══════╝╚═╝  ╚═══╝ ╚═════╝ ╚═╝     ╚═╝
```

**Image metadata & EXIF extractor for OSINT and security research.**
Pull GPS coordinates, device fingerprints, timestamps, and author data from images — including remote URLs.

---

## What It Extracts

| Category | Data |
|----------|------|
| **GPS** | Latitude, longitude, altitude, bearing, speed — direct Google Maps & OpenStreetMap links |
| **Device** | Camera/phone make & model, software version, lens model, serial numbers |
| **Timestamps** | Date taken, date edited, GPS timestamp — cross-reference for timeline analysis |
| **Author** | Artist name, copyright, owner, embedded comments and descriptions |
| **Camera Settings** | Aperture, shutter speed, ISO, focal length, flash, exposure mode |
| **File Info** | Format, dimensions, color space, resolution |

---

## Install

```bash
git clone https://github.com/jakkxbt/metavenom
cd metavenom
pip install -r requirements.txt
```

Optional — install `exiftool` for deeper extraction:
```bash
# Debian/Kali/Ubuntu
sudo apt install libimage-exiftool-perl

# macOS
brew install exiftool
```

---

## Usage

```bash
# Single image
python3 metavenom.py --image photo.jpg

# Direct image URL
python3 metavenom.py --url https://example.com/image.jpg

# Bulk directory scan
python3 metavenom.py --dir ~/targets/images/

# Save markdown report
python3 metavenom.py --image photo.jpg --output report.md
python3 metavenom.py --dir ~/images/ --output bulk_report.md
```

### Global alias (optional)
```bash
echo "alias metavenom='python3 $(pwd)/metavenom.py'" >> ~/.zshrc
source ~/.zshrc
```

---

## Example Output

```
⚡ GPS DATA FOUND
┌──────────────────────┬────────────────────────────────────────────┐
│ Latitude             │ 43.4674483                                 │
│ Longitude            │ 11.8851267                                 │
│ Google Maps          │ https://maps.google.com/?q=43.4674,11.885  │
│ Gps Date             │ 2008:10:23                                 │
└──────────────────────┴────────────────────────────────────────────┘

📱 DEVICE FINGERPRINT
  Make        NIKON
  Model       COOLPIX P6000
  Software    Nikon Transfer 1.1 W

🕐 TIMESTAMPS
  DateTimeOriginal     2008:10:22 16:28:39
  ModifyDate           2008:11:01 21:15:07
```

---

## Use Cases

- **OSINT investigations** — locate where a photo was taken from a direct image URL
- **Bug bounty recon** — extract metadata from target employee photos, leaked documents, or app-served images
- **Forensics** — verify timestamp integrity, detect post-processing edits, identify device used
- **Catfish detection** — device fingerprint doesn't match claimed phone model
- **Evidence analysis** — author fields reveal real names or internal usernames

> **Note:** Most social platforms (Instagram, Twitter, Facebook) strip EXIF on upload.
> Direct file shares via Telegram (as file, not photo), Discord CDN, email attachments, and raw URLs usually **do not strip metadata**.

---

## Supported Formats

`jpg` `jpeg` `png` `tiff` `webp` `heic` `heif` `bmp` `gif` `cr2` `nef` `arw`

---

## Requirements

- Python 3.8+
- `Pillow` — core EXIF extraction
- `rich` — terminal UI
- `exiftool` (optional) — extended metadata extraction

---

## License

MIT — free to use, modify, and distribute.

---

*By [@jakkxbt](https://github.com/jakkxbt)*
