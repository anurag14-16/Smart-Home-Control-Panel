# Smart Home Control Panel 🏠

A simulation-based smart home automation system built with ESP32 that combines
password-protected security with appliance control. Designed and tested on Wokwi.

---

##  Project Overview

This project simulates a central home control panel placed at the entrance of a home.
It allows the user to authenticate via a 4-digit password, control a light and fan,
and manage door lock status — all through a single keypad interface with real-time
LCD feedback.

---

##  Features

- Password-protected access (4-digit keypad entry)
- Automatic door lock/unlock via servo motor
- Light control via relay module
- Fan control via relay + stepper motor (A4988 driver)
- Real-time status display on 16x2 I2C LCD
- Buzzer alert on wrong password entry
- Three-state system: Locked / Unlocked / Inside mode

---

## Keypad Controls

| Key | Function |
|-----|----------|
| 0–9 | Enter password digits |
| # | Confirm password |
| * | Clear password input |
| A | Toggle light ON/OFF (when unlocked) |
| B | Toggle fan ON/OFF (when unlocked) |
| C | Lock door — stay inside mode |
| D | Full logout — turn off appliances, lock door, return to password screen |

---

##  Components Used

| Component | Quantity | Purpose |
|-----------|----------|---------|
| ESP32 | 1 | Main microcontroller |
| 4x4 Matrix Keypad | 1 | Password input and appliance control |
| 16x2 I2C LCD | 1 | Real-time status display |
| SG90 Servo Motor | 1 | Door lock mechanism |
| Relay Module | 2 | Control light and fan power |
| Bipolar Stepper Motor | 1 | Simulates fan rotation |
| A4988 Motor Driver | 1 | Drives stepper motor |
| LED | 1 | Simulates light bulb |
| Buzzer | 1 | Wrong password alert |
| Resistor 220Ω | 1 | Current limiting for LED |

---

##  Pin Configuration

| Component | ESP32 Pin |
|-----------|-----------|
| Keypad Row 1–4 | GPIO 13, 12, 14, 27 |
| Keypad Col 1–4 | GPIO 26, 25, 33, 32 |
| I2C LCD SDA | GPIO 21 |
| I2C LCD SCL | GPIO 22 |
| Servo Signal | GPIO 18 |
| Relay 1 (Light) | GPIO 19 |
| Relay 2 (Fan) | GPIO 23 |
| A4988 STEP | GPIO 16 |
| A4988 DIR | GPIO 17 |
| Buzzer | GPIO 5 |

---

##  A4988 Wiring

- **SLEEP and RESET** pins must be pulled HIGH (3.3V) for the driver to operate
- **ENABLE** pin connected to GND (always enabled)
- **MS1, MS2, MS3** connected to GND (full-step mode)
- **VMOT** controlled via Relay 2 — relay ON = fan running, relay OFF = fan stopped

---

##  System Flow

```
Boot → "Enter Password"
         ↓
    Enter 4-digit code + #
         ↓
   Correct? → Servo unlocks → Appliance control mode
   Wrong?   → Buzzer beeps 3x → "Access Denied" → Try again
         ↓
   Press A → Toggle Light
   Press B → Toggle Fan (stepper spins)
   Press C → Lock door, stay inside (appliances still work)
   Press D → Full logout, all off, back to password screen
```

---

##  Libraries Used

| Library | Author |
|---------|--------|
| Keypad | Mark Stanley |
| LiquidCrystal I2C | Frank de Brabander |
| ESP32Servo | Kevin Harrington |

---

##  Simulation

Run this project on Wokwi: https://wokwi.com/projects/466616824961855489

---

##  Author

**Anurag**

B.Sc. (Hons) Electronics — Deen Dayal Upadhyaya College, University of Delhi

---
