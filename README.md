# Capacitive Touch Sensor Using LM358

## Why I built this?

I wanted to build a real touch sensor without relying on an Arduino or any digital shortcut. I also wanted to force myself to understand how an op amp behaves in practice and use only analog components to make something functional.

## What I ended up building

I built a high impedance capacitive touch sensor using LM358 acting as a comparator.
A coin works as the sensing plate. When you touch it, the voltage on that node shifts slightly. The op amp compares that tiny change of voltage to a reference voltage determined by the voltage divider configuration, and turns on the LED when the input crosses that threshold.

Sounds simple on paper right? In reality, everything depends on noise, impedance and how carefully you tune the reference.

## Circuit Overview

1) Comparator: LM358 on a single supply
2) Touch plate: Metal coin
3) Voltage reference divider: 1.5MΩ and 100kΩ
4) Pull down resistor: 1MΩ
5) Output: White LED with a current limiting 150Ω resistor

The coin acts like a small capacitor when it's touched. Your finger shifts the input node by a few tens of millivolts. The LM358 compares this change with the reference voltage and switches the output.

## Circuit

This section includes the full circuit used for the touch sensor.

![2794746D-0FB5-46A2-A6D4-5CE785659E62_1_105_c](https://github.com/user-attachments/assets/3c56d287-293c-4dcd-984f-b8bedaf4f5ab)

## What actually happened

### Prototype 1: The Transistor Failure
Before I learnt about op amps, I tried using an NPN transistor as the sensing element.
The LED barely lit. The sensitivity was horrible.
The circuit felt like I was forcing the wrong component to do a job it wasn't meant for 

Once I learnt what a comparator does, I realized immediately that the LM358 was the right tool for the job.

### Prototype 2: LM358 and the noise issue
The first LM358 attempt was way too sensitive to ambient noise. The LED flickered and the threshold drifted. The fix came from increasing the reference voltage slightly so that the comparator would ignore random fluctuations in noise.

### Prototype 3: Resistors mattered more than I expected
I started with a 7MΩ pull down. It was too sensitive and triggered without touching the plate.
Dropping it to 1MΩ made the response nice and stable.

The surprising part was how major resistor values changed the behavior of the entire sensor. A small adjustment completely changed sensitivity, stability and trigger accuracy.

## Results
1) Clean and consistent touch detection.
2) Zero microcontroller involvement
3) Very low power usage (5V and draws 0.001A only when touched so max power = 0.005W)
4) No random flickering once tuned correctly

## Future improvements
1) Add a Schmitt trigger stage to harden the threshold.
2) Build a PCB version for a more compact and stable design.

## Actual circuit build 
This is the final working implementation of the touch sensor on a breadboard.

![8A0BB05B-3D51-4EF0-ABE5-6EB50F3D76B1_1_105_c](https://github.com/user-attachments/assets/d985b8ab-895c-4b41-8368-2d22362c5faa)

## Demo

**Click here to watch the video demo**  
[ Watch on Google Drive](https://drive.google.com/file/d/142fAchAKle-YS19PesCG8SXIbo68Vkxt/view?usp=sharing)

## Author
Mahmod Kirresh



