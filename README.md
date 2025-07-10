# Center Console Controller For Fiat Brava

## Project Overview
My friend has a Fiat Brava and has been working to [replace the center console with a giant Tesla style screen](https://www.reddit.com/r/raspberry_pi/comments/1ilmfnt/car_infotainment_system/). He asked me to help create all of the electronics for this slightly silly project. The goal was to design a system so that all of the controls that were previously accessible through the mostly mechanical center console could now be accessed through the screen. Being a software engineer my friend had already developed a system to do this. 
<p align="center">
  <img src="https://github.com/user-attachments/assets/3dc93c34-eb3f-45c3-9522-2845a06fb923" alt="Description" width="300" >
</p>
It involved using a Raspberry Pi running Android OS for the GUI displayed on the screen which connected to another Raspberry Pi running a Debian Linux based OS over websockets. The second Raspberry Pi would control the Car's systems through its GPIO. It was necessary because Android OS does not support the GPIO on the Raspberry Pi. Android OS was required on the first Raspberry Pi as it offered the best touchscreen and USB GPS support.

## Initial Prototyping
I thought the electrical design would be best implemented as a PCB with various components. However, before a schematic and PCB is developed it is often wise to do some initial prototyping to figure out the requirements and specifications for the design.


## Electrical Design
![Brava High Level Electrical Diagram](https://github.com/user-attachments/assets/61b6c3db-63e3-4bed-8339-eeec780cbf65)
