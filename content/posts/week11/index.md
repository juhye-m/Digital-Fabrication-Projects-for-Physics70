---
title: "Week 11"
date: 2021-12-9T21:48:03-08:00
draft: false
---

## Week 11

## Color Tracking Web cam!

This week, I decided to tackle working with the ESP32 Cam and colortrack with OpenCV.js. Important notes included engaging the reset button onboard while connecting, and disconnecting the ground and GPIO pins after uploading the code. Once I had the program and board set up and working, it was time to manipulate the OpenCV application! It was difficult at first to set a good mask to track my blue-colored object. I used part of a switch controller to track, because it was a bright blue. To help be figure out the settings for the RGB values, I used this [RGB Color Picker](https://www.rapidtables.com/web/color/RGB_Color.html). Though it took a while, ultimately, the colortracking worked! 

{{< youtube id="g9m6Zp3z3As" title="ESP32 Cam Color Tracking" >}}

Then, I wanted to customize this program so that it outputs a music note when the program detects that the object is in a certain location. There is a lot to build open this, such as changing pitch as the colored object moves across the screen. This could be a cool instrument achieved with just a glove! MIDI could be integrated as well.

I did more research for what I could explore with the ESP32 webcam, and came across this [Python program that plays music when it detects your face](https://pgaleone.eu/tensorflow/opencv/playerctl/2020/03/26/facectrl-control-media-player-face/).

Though not ESP32-specific, in general applications, I also found a [research paper](/research.pdf) on hand gesture recognition, which also logs differences in detection based on camera used, depth of field, and backgrounds. This would be a great place for people to learn more if they are interested in object tracking.

## Capacitive Touch Midi Controller

I wrote custom code to measure capacitive touch and turn that data into midi data to use in a DAW! 
First, I set up my circuit like so (this is something we went over in earlier weeks):

![Capacitive sensor](IMG_7223.jpg)

The idea was that when the sensor outputs beyond a certain threshold, a midi note would be sent as output. When the capacitive sensor is below a certain threshold, the midi note is no longer playing. The capacitive sensor has more flexibility and versatility than the button midi circuit I built last week. This is because copper tape capacitive sensoring is not a binary, but is a function of how much resistance I am putting on the tape! Because of this, I could control velocity of my midi output. (note: velocity in the context of MIDI is a synonym to loudness). I also accounted for this in my code. 127 represents the loudest a midi note can be tagged for. 0 is the smallest. My approach was to first test the range of numbers outputted by the capacitive sensor, and wrote in threshold values according to what was reasonable. For the current setup, I decided to use 40000 as the high threshold, 20000 as a medium threshold, and 1000 as a low threshold. These would in turn represent high, low, and medium velocities, respectfully. These numbers were set to variables so that the threshold values can be easily manipulated based on the sensor sensitivity.

``` cpp
#include <CapacitiveSensor.h>

CapacitiveSensor Sensor = CapacitiveSensor(7,5);  // 7 is charge pin.  5 is sense pin.
byte noteON = 144; //note on command

long currentState = 0;
long lastState = 0;

void setup(){
  Serial.begin(115200); //initialize Serial connection
}
void loop(){
  long sensorValue = Sensor.capacitiveSensor(1000);
  long high = 40000;
  long med = 20000;
  long low = 1000;
  currentState = sensorValue;
  if (currentState > high  && lastState < low){
    MIDImessage(noteON, 60, 127); //turn note 60 on with 127 velocity
    delay(200); // Debounce
  if (currentState > med  && (lastState < low){
    MIDImessage(noteON, 60, 80); //turn note 60 on with 127 velocity
    delay(200); // Debounce
  } else if(currentState <= high  && lastState >= low){
    MIDImessage(noteON, 60, 0); //turn note 60 off
    delay(20);
  }
  lastState = currentState;

//  Serial.println(sensorValue); // Debugging
 
}
//send MIDI message
void MIDImessage(byte command, byte data1, byte data2) {
  Serial.write(command);
  Serial.write(data1);
  Serial.write(data2);
}
```
The serial midi program I ran is the same code as last week's, as well as the IAC buses for input/output. You can find it [here, in week 10](https://juhye-m.github.io/ps70/posts/week-10/).

My circuit and baseline code works. I can test the output values by printing the sensor values to the serial monitor. I ran the serial to midi converter, and hooked it up to my Macbook audio input bus. I then opened my DAW, and it almost works!

{{< youtube id="wJ-ZqfLPNT8" title="Capacitive Touch MIDI Controller" >}}

However, for some reason, this midi data doesn't "save", nor does it produce sound. However, it is clearly detecting the midi notes. I have yet to debug this.

I also did further research on the overall technology I am implementing. IAC stands for Inter-Application Communitation. The IAC Driver is Apple's default MIDI device that you can use to communicate to Applications (such as Logic Pro X) that I use here. I must set up IAC drivers -- it doesn't set itself up automatically.

MIDI refers to a protocol for communication, digital interface, and electrical connectors  -- formally called Musical Instrument Digital Interface. It was developed in the 80s. The reason why MIDI devices do not produce audio on their own is because MIDI does not provide actual audio signals. It is simply data and information that does not include audio signals.

For my code, I used the MIDImessage Arduino function. It takes as parameters (noteON, pitch, velocity). These are decimal values, which are converted into binary. More info [here](https://www.instructables.com/What-is-MIDI/)!

## Miscellaneous

I wanted to make my terminal more visible when recording a demo video and was planning on switching to "dark mode". Turns out, you can customize the mac terminals even more! Here's my custom terminal inspired by an artist I like.

![Rosé terminal](rose.jpg)

You can also customize your terminal by going to preferences->profile, then selecting custom parameters!