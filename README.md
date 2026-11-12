# black-wire-reference

A Hermes Agent skill that looks up **board pinouts, GPIO maps, wiring guides and
power profiles** in the [Black Wire Maker's Technical Reference
Guide](https://valleytech-black-wire-guide.pages.dev/) catalog — 2,700+ boards,
1,600+ physical pinout images, transcribed connector pin tables and 15
wiring/protocol guides.

It is a source index, not an electrical authority: every answer carries the
source URL, revision, review status and coverage gaps.

## Install into Hermes

```bash
hermes skills install \
  https://raw.githubusercontent.com/rahlquist/black-wire-reference/main/SKILL.md \
  --yes
```

Or clone and copy `SKILL.md` + `scripts/` into `~/.hermes/skills/black-wire-reference/`.

## What it does

- `search` — exact-model board lookup (`RAK-13002` and `RAK13002` resolve to the
  same record; numeric suffixes stay distinct).
- `show` — one board record: revision, coverage status, assets, documentation gaps.
- `pins` — transcribed connector pin tables (position, label, functions).
- `resolve` — raw/live URLs for every pinout asset, plus a `?board=<id>` deep link.
- `wiring` — the 15 RJ45 / UART / RS-485 / CAN / I2C / SPI / SWD / JTAG / RFID guides.
- `stats` — catalog edition and counts.

## Usage

```bash
python3 scripts/bwm.py search "ESP32-S3-DevKitC-1"
python3 scripts/bwm.py show <board-id>
python3 scripts/bwm.py pins <board-id> --connector "P1"
python3 scripts/bwm.py resolve <board-id>
python3 scripts/bwm.py wiring "RS-485"
```

`--catalog PATH` uses a local `library/catalog.json`; the default downloads and
caches the live catalog (about 16 MB). Python 3.10+, standard library only.

## Files

| File | Purpose |
|------|---------|
| `SKILL.md` | Skill definition (Hermes loads this) |
| `scripts/bwm.py` | Catalog lookup CLI |

## Credits

- Catalog data: the Black Wire Maker's Technical Reference Guide by Kal /
  Valleytech Solutions, and its `black-wire-pinouts` collection. Fetched live;
  no catalog data is redistributed here. Manufacturer artwork retains its own
  rights.
- Skill: Richard Ahlquist.
