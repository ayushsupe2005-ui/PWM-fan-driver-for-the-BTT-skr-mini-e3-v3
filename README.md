I accidentally fried one of the fan ports on my BTT skr mini e3 v3 board. 
I was in the middle of taking apart my 3D printer toolhead and a PWM controller board that I had connected to the fan port accidentally shorted due to a screw. 
This fried one of the transistors on the board, so that port become permanently always on. 
I had some electronic components laying around, so I made this circuit in multisim. 
Note that this is my first time designing something like this so I might have overlooked something. 

<img width="980" height="601" alt="image" src="https://github.com/user-attachments/assets/3bc0ea27-c29e-4a97-88f6-3efc9560f5b1" />

I used the following components: 
<ul>
  <li>
    1 1k resistor
  </li>
  <li>
    2 10k resistors
  </li>
  <li>
    1 1N5819 Schottky diode
  </li>
  <li>
    1 IRF520N N-Channel mosfet
  </li>
  <li>
    1 2n3904 NPN transistor
  </li>
</ul>

Couple things about this circuit: 
<ul>
  <li>
    This circuit allows a 3.3V GPIO pin to control a 24V fan
  </li>
  <li>
    I simulated this to work for a 24V 6.0W fan (This is the 96 ohm resistor in the circuit). I also set the PWM frequency to 25 kHz. 
  </li>
  <li>
    This circuit uses low-side switching, which is also what the BTT skr mini e3 v3 uses. This means that when the 3.3V GPIO pin is high, the fan is off. When the 3.3V GPIO is low, the fan is on. 
  </li>
  <li>
    This circuit uses a level shifter made from the 2N3904 transistor to shift the level of the digital high signal from 3.3V to 24V. 
  </li>
  <li>
    The 1N5819 Schottky diode is there to counteract any voltage spikes generated from the fan. 
  </li>
  <li>
    R3 is there to lower the Vgs Voltage. The max Vgs voltage for the IRF520N is ±20V. Without R3, the Vgs voltage would go up to 24V.  
  </li>
  <li>
    R1 is there to limit the current from the GPIO to the base of the transistor. Without this, the transistor will fry. 
  </li>
  <li>
    R2 is a pull-up resistor that allows the signal to be digital (either high or low)
  </li>
</ul>
