## Context
This repository contains the hardware design files for the Memetrol project. This project can control three washing machines and one dryer. Users can authenticate themselves using an RFID badge. The system logs the usage of the machines. A webserver on the system serves these logs to the administrator.

## Hardware
The hardware consists of a Raspberry Pi zero W and a Waveshare RP2040-zero both mounted on the base PCB. This PCB also contains the power supply, the relay drivers and analog circuitry for the current sensors. The Raspberry Pi is connected to the Waveshare RP2040-zero with UART. The Waveshare RP2040-zero is connected to the relay drivers and the current measurement circuitry. The Raspberry Pi is connected to the rest of the peripherals using a 20 pin ribbon cable. This cable goes to the door PCB, at which point the connections to the buttons, the LCD and the RFID reader are broken out.

## Changes for the next revision
- Not enough mounting holes were placed on the main PCB. In the end I drilled out the 2.5 mm mounting holes for the Raspberry Pi to 3 mm and drilled an extra one here: [image](extra_hole_location.png). In a future revision the mounting holes should be placed in the correct locations.
- R25 was not needed. This is the resistor in series with the buzzer. The volume can be controlled by varying the duty cycle of the PWM signal. This resistor should be removed in the next revision.
- The buzzer is not loud enough, a different buzzer should be used.
- The connectors for the relays should be changed, currently it consists of two connectors, one for + and one for ground. It should be changed to four connectors, one for each relay, this makes the connections more clear. The current labeling on the PCB is also not correct, where it says Ground it should be 12 volt.
- The analog circuitry for the current measurement could have its own 3.3 volt, or even a 1.65 volt regulator, this might make the measurements more stable.
- The rp2040-zero should know if the override switches are pressed, this would make calibration easier, since the rp2040-zero can then know if it should be measuring zero current or not.
- The electrolytic capacitors in the analog circuitry could be a lot smaller, these were only used because I had them laying around.
- An input power capacitory should be added.
- Maybe an aditional button should be added to the main PCB, this could be used for resetting passwords.
- In the current design a solderbridge is used to select between 5 volts and 12 volts for the button led power, with 12 volts being the default. However, the button leds can only handle up to 6 volts. The door PCB should be changed so that the leds can only be powered from the 5 volt rail.
- During the building of the PCB several mosfets broke, the gate was at around one volt even though it was being pulled down. After replacing them it was improved, but I also added a 10k resistor in parallel with the button leds which improved the leds realy turning off when the gate was being pulled down. This situation should be investigated further.
- Maybe an RFID interupt pin can be added to the door PCB, this would make the system more responsive and use less cpu time.
- The RFID and the LCD are on the same LCD bus, but this makes the RFID reader misbehave. Therefore it needs to be reset every time it is used. This should be fixed in the next revision.