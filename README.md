# Digital Alarm Clock (AVR Microcontroller)

A robust **Digital Alarm Clock** system implemented using an **AVR Microcontroller** (ATmega series). This project features real-time clock functionality, a user-configurable alarm, and an LCD interface for visual feedback.

---

## 🕒 Project Overview

The system is designed to maintain accurate time using internal timers and interrupts. It provides a user-friendly interface to set both the current time and the alarm time via physical buttons. The alarm status and time are displayed on a 16x2 LCD.

### 🔑 Key Features

- **Real-Time Clock:** Accurate timekeeping (Hours:Minutes:Seconds) using Timer1 Compare Match Interrupt.
- **Configurable Alarm:** Set a specific time for the alarm to trigger.
- **LCD Interface:** 16x2 LCD display showing current time, alarm time, and alarm status (ON/OFF).
- **Dual Mode Configuration:** Toggle between "Time Set" and "Alarm Set" modes using a dedicated switch.
- **Visual/Audio Alert:** Triggers an output (Buzzer/LED) on `PINC7` when the alarm time matches the current time.

---

## 🏗️ System Architecture

The system follows a modular approach, separating hardware initialization, interrupt-driven timekeeping, and the main application loop.

![System Flow](https://private-us-east-1.manuscdn.com/sessionFile/6d6PodzvRjfNhM4gyqPamI/sandbox/OHu7gdRHFe7GRXsR77mEXL-images_1771619410249_na1fn_L2hvbWUvdWJ1bnR1L0RJR0lUQUxfQUxBUk1fQ0xPQ0svYWxhcm1fc3RydWN0dXJl.png?Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9wcml2YXRlLXVzLWVhc3QtMS5tYW51c2Nkbi5jb20vc2Vzc2lvbkZpbGUvNmQ2UG9kenZSamZOaE00Z3lxUGFtSS9zYW5kYm94L09IdTdnZFJIRmU3R1JYc1I3N21FWEwtaW1hZ2VzXzE3NzE2MTk0MTAyNDlfbmExZm5fTDJodmJXVXZkV0oxYm5SMUwwUkpSMGxVUVV4ZlFVeEJVazFmUTB4UFEwc3ZZV3hoY20xZmMzUnlkV04wZFhKbC5wbmciLCJDb25kaXRpb24iOnsiRGF0ZUxlc3NUaGFuIjp7IkFXUzpFcG9jaFRpbWUiOjE3OTg3NjE2MDB9fX1dfQ__&Key-Pair-Id=K2HSFNDJXOU9YS&Signature=uH4etBXzr7fmLNqBIA2fC60HcuUS11Jly9jllc440xyTLbiiFHB6nCgbuZ6caXUNSFxD5I~qqPRfhNrvZpQL4Vyc0vxV7l4vcq4vnZ7vfPJDIAaPZ9Tgg~39wYkFXnYHegsGPih8YHG9J9wNey40Exv-9Md7lVrQNINF15k-xUT-B5uFrgRoWwB45EQ~tjAOzE9prt~o68Po4CxTK-lP1L7l~eFjF9ZHIbHg64Es8nNEapX3jkqp6zGLCXf8jes8x-v~hJo8k2LOph7OKayM1S2RjlkpOj4iWMfHgrWk4500~XQE6XwXPI3BacZ5A2mPki2xH5qE~dM0HY3PidxVkA__)

### 📂 Hardware Connections (Typical)

| Component | Port/Pin | Description |
| :--- | :--- | :--- |
| **LCD Data** | `PORTC` | 8-bit Data Bus for LCD. |
| **LCD RS** | `PORTD6` | Register Select. |
| **LCD Enable** | `PORTD5` | Enable Signal. |
| **Buzzer/LED** | `PORTA7` | Alarm Output Indicator. |
| **Mode Switch** | `PINA4` | High: Set Time \| Low: Set Alarm. |
| **Alarm Toggle** | `PINA5` | High: Alarm ON \| Low: Alarm OFF. |
| **Buttons** | `PINA0-PINA3` | Increment/Decrement Hours and Minutes. |

---

## 💻 Technical Implementation

- **Timer/Counter1:** Configured in **CTC Mode** (Clear Timer on Compare Match) with a prescaler to generate a precise 1-second interval.
- **Interrupt Service Routine (ISR):** The `TIMER1_COMPA_vect` handles the incrementing of seconds, minutes, and hours to ensure timekeeping runs independently of the main loop.
- **LCD Driver:** Custom implementation for sending commands and characters to a standard 16x2 LCD.
- **Debouncing:** Basic software delays are implemented to handle button debouncing during time adjustment.

---

## 🚀 How to Build and Flash

1. **Prerequisites:**
   - AVR-GCC compiler.
   - AVR Libc.
   - A programmer (e.g., USBasp, AVRISP mkII).
   - `avrdude` for flashing.

2. **Compilation:**
   Navigate to the `DIGITAL_ALARM_CLOCK` directory and run:
   ```bash
   avr-gcc -g -Os -mmcu=atmega32 -c main.c
   avr-gcc -g -mmcu=atmega32 -o main.elf main.o
   avr-objcopy -j .text -j .data -O ihex main.elf main.hex
   ```

3. **Flashing:**
   ```bash
   avrdude -c <your_programmer> -p m32 -U flash:w:main.hex:i
   ```

---

## 👤 Author
**Mohamed**
- GitHub: [@Mohamed662172](https://github.com/Mohamed662172)
