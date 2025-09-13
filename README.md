# Project_QRLock
Project supported by AI, Raspberry Pi, SQLite, Python

# QRLOCK Access Control System (Simulator Mode)

QRLOCK is a simulated QR code-based access control system designed for environments where physical GPIO hardware is unavailable. It mimics the behavior of a smart lock system using QR codes and a door button, with support for one-time passcodes (OTP) and administrative control.

---

## 🔧 Features

- ✅ Simulated GPIO interface for lock and button control
- 📦 SQLite database for storing QR codes and OTP flags
- 🔐 QR code validation with optional OTP mode
- 🧑‍💼 Admin menu for managing QR codes and system settings
- 🛠️ Button-triggered exit mechanism
- 📋 Viewable QR code database with timestamps

---

## 🧠 How It Works

1. **Startup**:
   - Initializes the SQLite database (`qr_access_demo.db`)
   - Sets up simulated GPIO pins for lock and exit button

2. **QR Code Scanning**:
   - Users input QR codes via terminal
   - Valid QR codes unlock the simulated lock for 5 seconds
   - OTP codes are deleted after use

3. **Exit Button**:
   - Simulated button press triggers lock release

4. **Admin Access**:
   - Scanning the special QR code `ADMIN123` opens the admin menu
   - Admins can add/delete/reset QR codes, toggle OTP mode, and view the database

---

## 🛠️ Admin Menu Options

| Option | Description |
|--------|-------------|
| 1      | Save a single QR code (with optional OTP flag) |
| 2      | Continuous QR code scan (until 'STOP') |
| 3      | Delete a specific QR code |
| 4      | Reset all QR codes |
| 5      | Toggle OTP mode on/off |
| 6      | View all QR codes in the database |
| 7      | Exit admin menu |

---

## 🗃️ Database Schema

```sql
CREATE TABLE qr_codes (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    qr_code TEXT UNIQUE,
    date_added TEXT,
    otp INTEGER DEFAULT 0
);
```

- `qr_code`: Unique identifier scanned by users
- `date_added`: Timestamp of QR code entry
- `otp`: Flag indicating if the code is one-time use (1) or reusable (0)

---

## 🚪 Lock Simulation

- Lock is controlled via `LOCK_PIN` (simulated GPIO pin 16)
- Unlocks for 5 seconds upon valid QR scan or button press
- Exit button is simulated via `BUTTON_PIN` (GPIO pin 15) 

## Raspberry Pi 4 GPIO Pinout (Pin 1 to Pin 40)

| Pin Number | Name            | Function / Description                         |
|--------------|-----------------|------------------------------------------------|
| 1            | 3.3V Power      | Power supply (3.3V)                            |
| 2            | 5V Power        | Power supply (5V)                              |
| 3            | GPIO 2 (SDA1)   | I2C Data (SDA)                                 |
| 4            | 5V Power        | Power supply (5V)                              |
| 5            | GPIO 3 (SCL1)   | I2C Clock (SCL)                                |
| 6            | GND             | Ground                                         |
| 7            | GPIO 4 (GPCLK0) | General Purpose I/O                            |
| 8            | GPIO 14 (TXD)   | UART Transmit                                |
| 9            | GND             | Ground                                         |
| 10           | GPIO 15 (RXD)   | UART Receive                                 |
| 11           | GPIO 17         | General Purpose I/O                            |
| 12           | GPIO 18         | General Purpose I/O / PWM                    |
| 13           | GPIO 27         | General Purpose I/O                            |
| 14           | GND             | Ground                                         |
| 15           | GPIO 22         | General Purpose I/O                            |
| 16           | GPIO 23         | General Purpose I/O                            |
| 17           | 3.3V Power      | Power supply (3.3V)                            |
| 18           | GPIO 24         | General Purpose I/O                            |
| 19           | GPIO 10 (MOSI)  | SPI Master Out Slave In                      |
| 20           | GND             | Ground                                         |
| 21           | GPIO 9 (MISO)   | SPI Master In Slave Out                        |
| 22           | GPIO 25         | General Purpose I/O                            |
| 23           | GPIO 11 (SCLK)  | SPI Clock                                    |
| 24           | GPIO 8 (CE0)    | SPI Chip Enable 0                            |
| 25           | GND             | Ground                                         |
| 26           | GPIO 7 (CE1)    | SPI Chip Enable 1                            |
| 27           | GPIO 0 (ID_SD)  | I2C ID EEPROM                                |
| 28           | GPIO 1 (ID_SC)  | I2C ID EEPROM                                |
| 29           | GPIO 5          | General Purpose I/O                            |
| 30           | GPIO 6          | General Purpose I/O                            |
| 31           | GPIO 12         | PWM / General Purpose I/O                   |
| 32           | GPIO 13         | PWM / General Purpose I/O                   |
| 33           | GPIO 19         | PCM / I2C / General Purpose I/O            |
| 34           | GND             | Ground                                         |
| 35           | GPIO 26         | General Purpose I/O                            |
| 36           | GPIO 16         | General Purpose I/O                            |
| 37           | GPIO 20         | General Purpose I/O                            |
| 38           | GPIO 21         | General Purpose I/O                            |
| 39           | GND             | Ground                                         |
| 40           | GPIO 21         | General Purpose I/O                            |

*Note:* Not all pins are suitable for all purposes; consult the Raspberry Pi 4 GPIO documentation for detailed use cases and limitations.
---

## 🧪 Simulator Mode

This implementation uses `MockGPIO` to simulate Raspberry Pi GPIO behavior in a terminal environment. All GPIO actions are printed to the console for visibility.

---

## 🏁 Getting Started

1. Run the script in a Python environment
2. Wait for QR code input or button press
3. Use `Example123` to access admin controls
4. Manage QR codes and test lock behavior

---

## 📌 Notes

- OTP codes are automatically deleted after successful use
- Admin QR code is hardcoded as `example123`
- All interactions are simulated via terminal prompts

---

## 📂 File Overview

- `qr_access_demo.db`: SQLite database file
- `MockGPIO`: Simulated GPIO class
- `admin_menu()`: Admin interface for QR code management
- `unlock_lock()`: Simulates unlocking mechanism
- `is_valid_qr_code()`: Validates QR codes with optional OTP logic

---

## 🧹 Cleanup

On exit (e.g., `Ctrl+C`), the system performs GPIO cleanup to simulate proper shutdown.

---

## 📞 Contact

For enhancements, integration with real hardware, or deployment support, feel free to reach out or fork this project.

```
