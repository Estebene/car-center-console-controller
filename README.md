# Center Console Controller For Fiat Brava

## Project Overview
My friend has a Fiat Brava and has been working to [replace the center console with a giant Tesla style screen](https://www.reddit.com/r/raspberry_pi/comments/1ilmfnt/car_infotainment_system/). He asked me to help create all of the electronics for this ~~silly~~ revolutionary project. The goal was to design a system so that all of the controls that were previously accessible through the mostly mechanical center console could now be accessed through the screen. Being a software engineer my friend had already developed a system to do this. 
<p align="center">
  <img src="https://github.com/user-attachments/assets/3dc93c34-eb3f-45c3-9522-2845a06fb923" alt="Screen hastily attached to the front of a destroyed center console" width="300" >
</p>
It involved using a Raspberry Pi running Android OS for the GUI displayed on the screen which connected to another Raspberry Pi running a Debian Linux based OS over websockets. The second Raspberry Pi would control the Car's systems through its GPIO. It was necessary because Android OS does not support the GPIO on the Raspberry Pi. Android OS was required on the first Raspberry Pi as it offered the best touchscreen and USB GPS support.

## Initial Prototyping
I thought the electrical design would be best implemented as a PCB with various components. However, before a schematic and PCB is developed it is often wise to do some initial prototyping to figure out the requirements and specifications for the design. Cheap Aliexpress boards such as the IBT-2 and an 8 channel relay board and a Raspberry Pi 4 were used to test all of the functionality of the car. We referred to the car's electrical wiring diagrams available in the manual. ChatGPT was used to develop much of the code as this allowed for rapid prototyping.

<p align="center">
  <img src="https://github.com/user-attachments/assets/86268ebf-3019-4b79-bd91-45b7eca3a683" alt="Description" width="300" >
</p>

A difficult problem we ran into was that when controlling the fan through PWM it made audible noises. At low PWM frequencies the fan would make a variable whoosing sound and at higher frequencies (~1000Hz) a whining sound could be heard. The previous fan controller used selectable position resistor ladder to determine the power to the fan and thus the speed so I became worried that the motor was not suitable for controlling with PWM. We tried placing a capacitor across the fan to smooth out the switched voltage but this did not help. To help diagnose the problem I used an oscilloscope to measure the voltage across the fan, this showed than even though the PWM frequency might be set at 50kHz in software only 1kHz might be generated on the output of the Raspberry Pi. This is because the PWM was implemented in software using function calls to turn the GPIO on and off quickly. Eventually through online research we found that the PWM frequency can be increased significantly by using the Raspberry Pi's built-in hardware PWM. Implementing this fixed the issue and the fan no longer made unexpected noises.

## Electrical Design
![Brava High Level Electrical Diagram](https://github.com/user-attachments/assets/61b6c3db-63e3-4bed-8339-eeec780cbf65)
