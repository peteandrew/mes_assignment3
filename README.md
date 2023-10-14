# Making Embedded Systems - Assignment 3
## Blinky
This is an STM32Cube project that will blink the LEDs on an STM32L1 Discovery Kit. Pressing the user button allows the LED blinking to be switched on or off.

The project makes use of a timer that sets a tick flag every 100th of a second. On every tick, if LED blinking is enabled, a counter is incremented and when `LED_TOGGLE_TICKS` are reached the LEDs are toggled. Also on every tick the state of the user button is polled. The button pressed state is debounced and is only set if the button is down for `DEBOUNCE_TICKS`.