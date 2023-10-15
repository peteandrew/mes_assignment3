# Making Embedded Systems - Assignment 3
## Blinky
This is an STM32Cube project that will blink the LEDs on an STM32L1 Discovery Kit. Pressing the user button allows the LED blinking to be switched on or off.

The project makes use of a timer that sets a tick flag every 100th of a second. On every tick, if LED blinking is enabled, a counter is incremented and when `LED_TOGGLE_TICKS` are reached the LEDs are toggled. Also on every tick the state of the user button is polled. The button pressed state is debounced and is only set if the button is down for `DEBOUNCE_TICKS`.

## Questions
- What are the hardware registers that cause the LED to turn on and off? (From the processor manual, don’t worry about initialization.)

    The LEDs on the discovery board are connected to GPIO pins 6 and 7 of port B. The LEDs can be switched on and off by writing directly to the output data register (ODR) or by writing to the bit set/reset register (BSRR).

    For example to switch one LED on using the ODR the following expression can be run: `GPIOB->ODR |= 0x40`
    
    To switch the same LED off: `GPIOB->ODR &= ~0x40`

    To switch an LED on using the BSRR: `GPIOB->BSRR = 0x40`
    
    and off: `GPIOB->BSRR = 0x40 << 16`

- What are the registers that you read in order to find out the state of the button?

    The input data register (IDR) is used to read the input state of a GPIO pin. On this board the button is connected to pin 0 of port A.

    To read the current button state the following expression can be run: `GPIOA->IDR & 0x01`

- Can you read the register directly and see the button change in a debugger or by printing out the value of the memory at the register’s address?

    In CubeIDE, while debugging the project, adding `GPIOA->IDR & 0x01` to the expressions list allows the current button state to be displayed. Pressing the button and stepping in the debugger causes the button state value to change from 0 to 1.