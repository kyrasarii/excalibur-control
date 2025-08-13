#  **Casper Excalibur Control Panel** 

Welcome to the **ultimate TUI control panel** for your **Casper Excalibur** gaming laptop! This sophisticated terminal interface brings together **power management** and **advanced RGB keyboard control** in one beautiful, efficient package. Take full control of your hardware with style!

---

## 🚀 **Features**

This control panel seamlessly integrates with your **casper-wmi driver** and **power-profiles-daemon**, delivering a comprehensive hardware management experience:

### ⚡ **Power Profile Management**
- Switch between **performance**, **balanced**, and **power-saver** profiles instantly
- Real-time profile status monitoring
- Seamless integration with **power-profiles-daemon**

### 🌈 **Advanced RGB Keyboard Control**
- **8 Dynamic LED Modes**: Off, Static, Blinking, Breathing, Pulsing, Rainbow effects
- **Full RGB Color Palette**: 8 preset colors + custom hex color support
- **Multi-Region Control**: Configure 1-9 keyboard regions independently
- **3 Brightness Levels**: Fine-tune your backlight intensity

### 🎯 **Preset Effects Library**
- **Gaming Presets**: Optimized Red/Blue static modes for competitive gaming
- **Productivity Themes**: Subtle breathing and pulsing effects for work
- **Rainbow Modes**: Dynamic wave and pulsing effects for maximum flair
- **Cyber Aesthetics**: Purple breathing and green hacker modes

### 📊 **System Information**
- Real-time CPU and memory monitoring
- Driver status verification
- Current hardware settings display

---

## 🛠️ **Installation Guide**

Ready to unlock the full potential of your **Casper Excalibur**? Follow these steps to get your control panel up and running:

### Prerequisites
- **Casper Excalibur** laptop with compatible hardware
- **Linux** with kernel headers installed
- **Python 3.6+** with curses support
- **Root/sudo access** for hardware control

### Steps

1. **Install the casper-wmi driver**:
   ```bash
   git clone https://github.com/kyrasarii/casper-wmi.git
   cd casper-wmi
   make
   sudo insmod casper-wmi.ko
   ```

2. **Set up permanent driver loading**:
   ```bash
   # Install with compression
   sudo zstd casper-wmi.ko -o /lib/modules/$(uname -r)/kernel/drivers/platform/x86/casper-wmi.ko.zst
   
   # Update module dependencies
   sudo depmod -a
   
   # Enable auto-loading
   echo "casper-wmi" | sudo tee /etc/modules-load.d/casper-wmi.conf
   ```

3. **Install power-profiles-daemon** (if not already installed):
   ```bash
   # Arch Linux
   sudo pacman -S power-profiles-daemon
   
   # Ubuntu/Debian
   sudo apt install power-profiles-daemon
   
   # Enable the service
   sudo systemctl enable --now power-profiles-daemon
   ```

4. **Download and install the control panel**:
   ```bash
   wget https://raw.githubusercontent.com/your-repo/casper-control-panel.py
   chmod +x casper-control-panel.py
   ```

5. **Launch the control panel**:
   ```bash
   sudo python3 casper-control-panel.py
   ```

---

## 🎯 **Usage Guide**

### 🎮 **Navigation Controls**
- **Arrow Keys**: Navigate through menus
- **Enter/Space**: Select options
- **ESC**: Go back or exit
- **Q**: Quick exit from main menu

### 🌈 **Keyboard Backlight Controls**
| Key | Action |
|-----|--------|
| `m/M` | Cycle through LED modes (0-7) |
| `b/B` | Adjust brightness levels (0-2) |
| `r/R` | Change region count (1-9) |
| `c` | Enter color selection menu |
| `0` | Quick turn off |

### 🎨 **Color Selection**
- **Arrow Keys**: Navigate preset colors
- **Enter**: Apply selected color
- **Custom Colors**: Use the RGB hex format (#RRGGBB)

### ⚡ **Quick Effects**
Access these instant preset effects:
- **Gaming Mode**: `Red Static` for competitive gaming
- **Work Mode**: `White Breathing` for productivity
- **Party Mode**: `Rainbow Wave` for maximum RGB goodness
- **Stealth Mode**: `Off` for silent operation

---

## 🔧 **Configuration**

### LED Control Format
The control panel uses the casper-wmi format: `[regions][mode][brightness][color]`

**Example**: `372ffffff`

#### 🔢 **Control String Breakdown**:
- **1st Digit (`3`)**: **Regions** - Defines which regions of the keyboard to control
- **2nd Digit (`7`)**: **Mode** - LED effect mode (0-7, where 0=off, 1-7=various effects)  
- **3rd Digit (`2`)**: **Brightness** - Intensity level (0=off, 1=dim, 2=bright)
- **Last 6 Digits (`ffffff`)**: **Color** - RGB hex code for static modes

#### 🎨 **Important Color Behavior**:
- **Static Mode (Mode 1)**: The hex color code determines the exact RGB color displayed
- **Dynamic Modes (Modes 2-7)**: The hex color code is **overridden** by the mode's built-in color patterns
- **Experimentation Tip**: For rainbow and breathing effects, the color value may influence the base hue, but results vary by mode

### Available LED Modes
| Mode | Effect | Description |
|------|--------|-------------|
| `0` | Off | Completely disabled |
| `1` | Static | Solid color |
| `2` | Blinking | Regular on/off pattern |
| `3` | Breathing | Smooth fade in/out |
| `4` | Pulsing | Quick pulse effect |
| `5` | Rainbow Pulsing | Color-shifting pulse |
| `6` | Rainbow Pulsing Alt | Alternative rainbow pulse |
| `7` | Rainbow Wave | Flowing rainbow effect |

---

## 🔍 **Troubleshooting**

### Driver Issues
```bash
# Check if driver is loaded
lsmod | grep casper

# Verify LED control path exists
ls -la /sys/class/leds/casper::kbd_backlight/

# Test manual control
echo "312ffffff" | sudo tee /sys/class/leds/casper::kbd_backlight/led_control
```

### Permission Issues
```bash
# Add user to appropriate groups
sudo usermod -a -G input $USER

# Or run with sudo (recommended)
sudo python3 casper-control-panel.py
```

### Power Profiles Issues
```bash
# Check power-profiles-daemon status
systemctl status power-profiles-daemon

# List available profiles
powerprofilesctl list
```

---

## 🎨 **Customization**

### Adding Custom Presets
Edit the `preset_colors` dictionary in the script:
```python
self.preset_colors = {
    "White": "ffffff",
    "Your Custom Color": "ff8000",  # Add your hex color here
    # ... more colors
}
```

### Creating Custom Effects
Add new presets to the `apply_preset_effect` method:
```python
presets = {
    "your_effect": (regions, mode, brightness, "hex_color"),
    # ... more presets
}
```

---

## 🙏 **Credits & Acknowledgements**

A huge thank you to the following projects and communities:

- **Casper-WMI Driver**: For enabling hardware control on Casper laptops
- **Power Profiles Daemon**: For system-wide power management
- **Python Curses**: For the terminal user interface framework
- **Linux Gaming Community**: For continuous support and feedback
- **RGB Enthusiasts**: For inspiring advanced lighting effects

---

## 📝 **License**

This project is licensed under the **MIT License** - see the LICENSE file for details.

---

## 🤝 **Contributing**

Want to improve the control panel? Contributions are welcome!

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📞 **Support**

Having issues or questions? Here's how to get help:

- **Open an Issue**: Report bugs or request features
- **Check the Wiki**: Detailed guides and troubleshooting
- **Community Discord**: Join other Casper users
- **Email Support**: contact@your-domain.com

---

**Enjoy your enhanced Casper Excalibur experience!** 🚀

*Transform your gaming setup with professional-grade hardware control. Game on!* 🎮✨
