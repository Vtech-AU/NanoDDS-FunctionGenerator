DDS Waveform Generator on Arduino Nano
A fully functional 8-bit direct digital synthesis (DDS) waveform generator using an Arduino Nano, 128×64 OLED, buttons, and timer interrupts—all implemented in pure C++. It outputs digital waveforms via 8 digital pins (D2–D9) with optional smoothing via RC.

🚀 Features
Waveforms: Sine, triangle, square (with adjustable duty), sawtooth, inverted sawtooth, and noise
Frequency range: ~2 Hz up to ~40 kHz (software-limited by table size and timer resolution)
Dynamic table sizing: Automatically adjusts table size (128 → 4 samples) based on frequency for optimal performance
Fast single-pin control: Uses direct PORTD writes to update 8-bit DAC in one operation, maximizing speed 
User interface: OLED display shows waveform type, frequency, amplitude, duty cycle, and computed RMS voltage
Button controls: Four buttons for mode, selection, up/down adjustments, and RUN toggling
Pin-change interrupt for RUN: Allows instantaneous start/stop of waveform output
RMS % display: Estimates waveform RMS (0–5 V range) and shows it as a percentage

🧠 Innovation Highlights
Automatic table-size adaptation
Calculates table length based on frequency, trading resolution for speed—crucial for high-frequency accuracy.

Efficient DAC output
All 8 data bits change in one PORTD = ...; call. This simple but powerful technique drastically boosts maximum achievable frequency .

Interrupt-driven control
Both waveform output (Timer1 CTC) and RUN button (Pin Change Interrupt) are interrupt-driven for low-latency and reliable operation.

RMS estimation in real-time
Computes waveform RMS across the buffer (based on 0–5 V scale) and displays it with 0.1% precision—no external measurement needed.

📋 Example Display Layout
makefile
Copy
Edit
WAVE: Sine
FREQ: 10000 Hz
AMPL: 75%
DUTY: 50%
RMS: 70.7%

[  waveform preview scrolls live ]

📦 Repository Contents
DDS_function_generator.ino – Full Arduino sketch

README.md – This documentation

(Optional) Wiring diagrams, Fritzing files, and hardware details

🔧 Requirements
Hardware:

Arduino Nano (ATmega328P)
128×64 OLED via I²C
4 momentary buttons (with pull-ups)
Optional RC filter on output lines

Software:
Adafruit_SSD1306 and Adafruit_GFX libraries
Arduino IDE (recommended version ≥1.8.x)

📥 Installation & Usage
Clone or download this repo to your Arduino sketch folder.

Install necessary libraries (via Library Manager): Adafruit SSD1306, Adafruit GFX.

Open the .ino in Arduino IDE, configure pins if needed.

Build and upload to your Nano.

Wire OLED, buttons, and output pins as per code comments.

Press MODE to cycle waveform, UP/DOWN to adjust settings, and RUN to start/stop output.

📈 Performance
Table Size	Max Output Frequency
128	~490 Hz
64	~1 kHz
32	~2 kHz
16	~4 kHz
8	~8 kHz
4	~16 kHz

Above ~10 kHz, table size reaches minimum of 4 to maintain timing.

🛠️ Contribution & Licensing
Feel free to fork, modify, or adapt this project under the MIT license.
Feedback, fixes, and feature requests are welcome!
