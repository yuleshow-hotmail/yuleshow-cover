# yuleshow-cover

![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)
![Pillow](https://img.shields.io/badge/Pillow-PIL-8C4A2F?logo=python&logoColor=white)
![OpenCC](https://img.shields.io/badge/OpenCC-繁→簡-FF6600)
![Premiere Pro](https://img.shields.io/badge/Premiere%20Pro-MOGRT-9999FF?logo=adobepremierepro&logoColor=white)
![YouTube](https://img.shields.io/badge/YouTube-Thumbnails-FF0000?logo=youtube&logoColor=white)

YouTube thumbnail generator for **梅璽閣菜話** (Yule Show's Gourmet Chatting).

## Files

| File | Description |
|------|-------------|
| `yuleshow-cover.py` | Interactive cover generator — prompts for episode number, series code, Chinese/English titles, finds a JPG in the current directory, and renders 3 variants (16:9 繁體, 16:9 簡體, 4:3 簡體) using PIL. Includes OpenCC traditional→simplified conversion. |
| `mogrt-cover.py` | Reads text controls from `Untitled.mogrt`, optionally edits them, and renders covers using the same data. Can also write updated values back into the MOGRT. |
| `doog` | Standalone single-episode cover script with hardcoded values. |
| `Untitled.mogrt` | Premiere Pro Motion Graphics Template (MOGRT) — a ZIP containing `definition.json` (7 editable text controls), `project.prgraphic` (binary layout), and preview thumbnails. |

## MOGRT Structure

The `.mogrt` file is a ZIP archive with 4 internal files:

```
Untitled.mogrt
├── definition.json      # Editable text controls + metadata
├── project.prgraphic    # Binary project (Adobe-proprietary)
├── thumb.png            # Static preview (1422×800)
└── thumb.mp4            # Video preview
```

### Editable Controls (from `definition.json`)

| ID | Role | Default Value | Fill | Stroke | Font | Size |
|----|------|---------------|------|--------|------|------|
| 9 | Episode | 總第309集 | ![](https://img.shields.io/badge/-%20-000000) Black | ![](https://img.shields.io/badge/-%20-FFFFFF) White 3px | NotoSans**-Bold | 50 |
| 6 | Slogan | Yule Show's Gourmet Chatting | ![](https://img.shields.io/badge/-%20-000000) Black | ![](https://img.shields.io/badge/-%20-FFFFFF) White 2px | HermanzTitling | 61 |
| 8 | Series name | 上海老風味之一百廿七 | ![](https://img.shields.io/badge/-%20-FFFF00) Yellow | ![](https://img.shields.io/badge/-%20-000000) Black 10px | NotoSerif**-Black | dynamic |
| 7 | Chinese title | 夜開花塞肉 | ![](https://img.shields.io/badge/-%20-FF0000) Red | ![](https://img.shields.io/badge/-%20-FFFFFF) White 8px | NotoSans**-Black | dynamic |
| 3 | English title | Stuffed Bottle Gourd with Pork | ![](https://img.shields.io/badge/-%20-000000) Black | ![](https://img.shields.io/badge/-%20-FFFFFF) White 3px | Sanchez | dynamic |
| 4 | TM symbol | ™ | ![](https://img.shields.io/badge/-%20-00FF00) Green | ![](https://img.shields.io/badge/-%20-000000) Black 4px | Arial Bold | 47 |
| 5 | Brand (vertical) | 梅璽閣菜話 | ![](https://img.shields.io/badge/-%20-00FF00) Green | ![](https://img.shields.io/badge/-%20-000000) Black 6px | SentyWen (文徵明體) | 133 |

> Canvas border: ![](https://img.shields.io/badge/-%20-00CC00) `#00CC00` (60px inset)

### Fonts Referenced

| PostScript Name | Font File | Used For |
|----------------|-----------|----------|
| `Arial-BoldMT` | Arial Bold.ttf | TM symbol |
| `HermanzTitling-Regular` | HermanzTitling Regular.otf | English slogan |
| `NotoSansCJKTC-Bold` | NotoSansTC-Bold.ttf | Episode number |
| `NotoSerifCJKTC-Black` | NotoSerifTC-Black.ttf | Series name |
| `Sanchez-Regular` | Sanchez Regular.otf | English title |
| `SentyWen` | 漢儀新蒂文徵明體.ttf | Brand 梅璽閣菜話 |

### Limitations

The visual layout (positions, font sizes, colors, strokes, layer hierarchy) is encoded in the binary `project.prgraphic` and can only be rendered by Adobe Premiere Pro or After Effects. The JSON only exposes text values and font names — not styling or positioning.

## Dependencies

```
pip install Pillow opencc-python-reimplemented
```

Fonts must be installed locally (see paths in the scripts).

## Usage

```bash
# Interactive mode — prompts for episode info
python3 yuleshow-cover.py

# From MOGRT data
python3 mogrt-cover.py
```

Place a `.jpg` photo in the same directory before running. Outputs are saved as `OUT_*.png`.
