# CYD-MUNCH-MAN-pac_man-
# 🎮 CYD MUNCH MAN

A full-featured Munch Man clone for the **ESP32 Cheap Yellow Display (CYD)** board (ESP32-2432S028R).

![Version](https://img.shields.io/badge/version-1.2-blue)
![Platform](https://img.shields.io/badge/platform-ESP32--CYD-yellow)
![License](https://img.shields.io/badge/license-MIT-green)

```
┌────────────────────────────────────┐
│[≡] SCORE 1250  🟡🟡🟡  LV2  PWR 5s│
├────────────────────────────────────┤
│ ██████████████████████████████████ │
│ █○·····█      █      █·····○█     │
│ █·███·███████████████·███·██      │
│ █·····························█   │
│ █·██·██·🔴····🟡····🔵·██·██·█   │
│ █····██·····██·····██·····█       │
│ ████·████·  👻👻  ·████·██████    │
│     ·██·    🍒    ·██·            │
│ ████·██████████████·██·██████     │
│ █○·········🟠··············○█     │
│ ██████████████████████████████████ │
└────────────────────────────────────┘
```

## ✨ Features

### 🕹️ Gameplay
- **Classic Munch Man mechanics** - dots, power pellets, ghosts
- **3 levels** with increasing difficulty
- **5 fruit types** - Cherry, Strawberry, Orange, Apple, Melon (100-1000 pts)
- **Smart ghost AI** - each ghost has unique behavior
- **Power mode** with blinking ghosts warning

### 👻 Ghost AI (like original!)
| Ghost | Color | Behavior |
|-------|-------|----------|
| **Blinky** | 🔴 Red | Direct chase - always follows player |
| **Pinky** | 🩷 Pink | Ambush - targets 4 tiles ahead of player |
| **Inky** | 🔵 Cyan | Unpredictable - random movements |
| **Clyde** | 🟠 Orange | Shy - chases when far, flees when close |

### 🍒 Fruits
| Level | Fruit | Points |
|-------|-------|--------|
| 1 | 🍒 Cherry | 100 |
| 2 | 🍓 Strawberry | 300 |
| 3 | 🍊 Orange | 500 |
| 4 | 🍎 Apple | 700 |
| 5 | 🍈 Melon | 1000 |

### ⚙️ Settings (saved to SD card)
- **Sound** - ON/OFF toggle
- **Volume** - 0-100% (PWM duty cycle)
- **Touch Sensitivity** - Low/Medium/High
- **Difficulty** - Easy/Normal/Hard (ghost speed)
- **Player Speed** - 60-150ms

### 🛠️ Extras
- **Built-in map editor** - create your own levels!
- **Touchscreen controls** - swipe to change direction
- **Persistent settings** - saved to SD card
- **Level progression** - ghosts get 5% faster each level

## 📋 Requirements

### Hardware
- **ESP32-2432S028R** (Cheap Yellow Display / CYD)
- **MicroSD card** (for levels and settings)
- **Passive buzzer** on GPIO 4 (optional, requires removing RGB LED)

### Software
- Arduino IDE 1.8.x or 2.x
- ESP32 board package
- TFT_eSPI library

## 📦 Installation

### 1. Clone repository
```bash
git clone https://github.com/yourusername/cyd-munchman.git
```

### 2. Configure TFT_eSPI
Edit `User_Setup.h` in your TFT_eSPI library folder:

```cpp
#define ILI9341_DRIVER
#define TFT_WIDTH  240
#define TFT_HEIGHT 320

#define TFT_MISO 12
#define TFT_MOSI 13
#define TFT_SCLK 14
#define TFT_CS   15
#define TFT_DC    2
#define TFT_RST  -1
#define TFT_BL   21

#define TOUCH_CS 33

#define SPI_FREQUENCY  40000000
#define SPI_READ_FREQUENCY  20000000
#define SPI_TOUCH_FREQUENCY  2500000
```

### 3. Prepare SD Card
Create folder structure:
```
SD Card/
└── gry/
    └── munchman/
        ├── level1.txt
        ├── level2.txt
        └── level3.txt
```

Copy level files from `levels/` folder to SD card.

### 4. Upload
1. Open `src/cyd_munchman.ino` in Arduino IDE
2. Select board: **ESP32 Dev Module**
3. Upload!

## 🎮 Controls

### Main Menu
- **PLAY** - Start game
- **EDITOR** - Open map editor
- **SETUP** - Configure settings

### In Game
- **Swipe** anywhere to change direction
- **[≡] button** (top-left) - Return to menu

### Map Editor
- **Touch cell** - Place/remove element
- **[<] [>]** - Change brush type
- **[CLR]** - Clear map
- **[SAVE]** - Save to SD card
- **[TEST]** - Test play the map
- **[EXIT]** - Return to menu

## 📁 Project Structure

```
cyd-munchman/
├── README.md
├── LICENSE
├── src/
│   └── cyd_munchman.ino      # Main game code (1700+ lines)
├── levels/
│   ├── level1.txt          # Classic maze
│   ├── level2.txt          # More tunnels
│   └── level3.txt          # Challenge maze
└── docs/
    └── wiring.md           # Hardware connections
```

## 🗺️ Map Format

Maps are 26x17 text files with cell types:

| Code | Element |
|------|---------|
| 0 | Empty (tunnel) |
| 1 | Wall |
| 5 | Dot |
| 6 | Power pellet |
| 7 | Ghost spawn |
| 8 | Fruit spawn |
| 9 | Player start |

Example:
```
11111111111111111111111111
16555555555555555555555561
15111511111111111111151151
...
```

## 🔧 Hardware Mod (Optional)

To enable sound, remove the RGB LED and connect a passive buzzer:
- **GPIO 4** → Buzzer (+)
- **GND** → Buzzer (-)

After removing RGB LED, these pins become available:
- GPIO 4 (Red LED) → **Buzzer**
- GPIO 16 (Green LED) → Free
- GPIO 17 (Blue LED) → Free

## 📊 Technical Details

| Parameter | Value |
|-----------|-------|
| Display | 320x240 px, ILI9341 |
| Cell size | 12x12 px |
| Map size | 26x17 cells |
| Game area | 312x204 px |
| Ghosts | 4 |
| Max levels | Unlimited (SD card) |
| Code size | ~1700 lines |

## 🎯 Scoring

| Action | Points |
|--------|--------|
| Dot | 1 |
| Power pellet | 10 |
| Ghost (1st) | 200 |
| Ghost (2nd) | 400 |
| Ghost (3rd) | 800 |
| Ghost (4th) | 1600 |
| Fruit | 100-1000 |

## 📜 Version History

### v1.2 (Current)
- Added 5 fruit types with unique graphics
- Implemented smart ghost AI (Blinky, Pinky, Inky, Clyde)
- Added level system with 3 maps
- Ghosts blink when power mode ending
- Fruit spawns during gameplay
- Level indicator in UI

### v1.1
- Added volume control (PWM)
- Added MENU button in game
- Optimized UI refresh (only updates changes)
- Settings saved to SD card

### v1.0
- Initial release
- Basic Munch Man gameplay
- Map editor
- Touch controls

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Submit bug reports
- Create new levels
- Suggest features
- Submit pull requests

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Inspired by classic arcade maze games
- [TFT_eSPI](https://github.com/Bodmer/TFT_eSPI) library by Bodmer
- [ESP32 CYD Community](https://github.com/witnessmenow/ESP32-Cheap-Yellow-Display)

---

**Made with ❤️ for the ESP32 CYD community**
