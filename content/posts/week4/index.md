---
title: "Week 4"
date: 2021-02-22T21:48:03-08:00
draft: false
---

## Week 4: Microcontroller Programming

This week, I created a simple button-controlled music player!

#### Materials
I used the M0 Metro Circuit from Adafruit, a piezo speaker, a button, and the breadboard from the PS 70 kit to start. 

I first used the button circuit from class as inspiration. I attached a button and a resistor from ground to one of its legs. Then I connected this leg to digital input 8 so that I can program the button's functionality. Finally I ran 5 volts to the other leg of the button. 

![Button](button.jpg)

Then, I hooked up the piezo speaker! I connected the - leg to ground and the + leg to digital pin 9 to upload instructions to the piezo.

![Circuit](circuit.jpg)

#### Code
I got the initial code for the music from this [Adafruit Guide!](https://learn.adafruit.com/experimenters-guide-for-metro/circ06-code)



#### And... TADA!
{{< youtube id="B8eITQbo8LA" title="Music button" >}}
