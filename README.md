# Non-Blocking Button Debounce & Edge Detection (C++)

This repository contains C++ firmware for an **ATmega328P** (Arduino Uno platform) that handles mechanical button inputs using non-blocking timing logic rather than blocking delay routines.

## Features
* **Non-blocking execution:** Uses `millis()` state checks so the microcontroller can run other tasks concurrently.
* **Debounce logic:** Filters out mechanical contact bounce / switch noise.
* **Edge detection:** Detects clean transition edges (button press events) to toggle output states reliably.
* **Circuit verification:** Simulated and validated in **Proteus 9**.

## Hardware & Tools
* **Language:** C++
* **Microcontroller:** ATmega328P / Arduino Uno
* **IDE / Toolchain:** Visual Studio Code (GCC/G++) / Arduino IDE
* **Simulation Software:** Proteus 9 Professional

## How It Works
Instead of halting execution using `delay(50)`, the algorithm records the timestamp when a pin change occurs. If the pin remains stable for longer than the debounce threshold (`50ms`), the program registers a valid state change and updates the output.

```cpp
if ((millis() - lastDebounceTime) > DEBOUNCE_DELAY) {
    if (reading != buttonState) {
        buttonState = reading;
        if (buttonState == LOW) { 
            digitalWrite(LED_PIN, !digitalRead(LED_PIN)); // Toggle LED
        }
    }
}
