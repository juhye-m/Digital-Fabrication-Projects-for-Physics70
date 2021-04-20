---
title: "Week 12"
date: 2021-04-19T10:35:42-07:00
draft: false
---

## Week 12

## Molding and Casting

This week was molding and casting week, so I looked around my room for something interesting to make a mold out of. After feeling like I didn't have something cool (I left my trinkets at home), I finally decided to make a mold of my perfume bottle cap. It looks like this! 

![Perfume cap](figure.jpg)
![Perfume cap side](figureside.jpg)

I liked how the bottom sat flat on the ground, and how the figure resembles a human. I thought it would be real fun to make popsicles in the shape! I found that the sunglasses especially would be special as it would be something difficult to reinvent without a mold.

I debated between doing a two-part mold versus just one part. eventually, I went with the one-part mold since it seemed like they would produce similar results if I cut the mold at the sunglasses to take the figure out later.

I put the figure in a cup and poured the mixed silicone in. Unfortunately, it didn't reach the top to completely engulf the figure. As a workaround, I simply slathered the top of the head with some silicone and hoped that it would still provide some structure (which it did as you'll see!). I held the figure in place with a stick, but then later just held the figure, as it kept rising and even pushing the stick upwards. I thought about putting rocks inside the figure as well, where I had taped the bottom, but it was too late for that. After I finished, I let the mold hardern for several hours.

It was extrememly difficult to get the mold out of the cup. I cut out the edges with a kinfe, but it took me longer than I expected.

![Mold](molded.jpg)
![Casting the mold with OJ](cast.jpg)

Finally, after getting the mold out of the cup, I cut the mold paralell to the ground where the figure's sunglasses were. By doing so, I was able to remove the figure while keeping the mold and its intracacies intact. Then, I filled the mold with orange juice and froze it to form a popsicle. Here is the finished product:

![My perfume cap popsicle!](popsicle.jpg)

If I were to do this again, I would 
- make sure there is enough silicon to fill the mold cup
- use a narrower cup to maximize the height
- use a paper or disposable plastic cup so that I can easily rip the cup off of the mold
- mold a figure that is easier to work with (but is still interesting)!

## Final Project work

This week, I compiled a [new page to document all my final project work and ideas](https://juhye-m.github.io/ps70/posts/wip-final-proj/). I then assembled my 3D printed model of my midi keyboard casing, and explored the speaker component, a new output device that was sent to me! 

## Speakers

With my mid-term kit, I received a speaker and an amplifier. I plan on exploring these components more, and did some research on what I could accomplish this week. There is a [simple audio player](https://www.arduino.cc/en/Tutorial/SimpleAudioPlayer) tutorial on the official Arduino website that I read through. To play .wav files, however, I need a Arduino shield with an SD card. I wanted to explore the Apple Music/Spotify APIs to see if I can use my keyboard as a speaker using internet access instead of local files on an SD card. Unfortunately, I couldn't find any information on how to start doing so, other than these blogs that said it wasn't possible for them. I did find this work-in-progress github repository that integrates the Spotify Web API with the Arduino libraries. It seems like I can use the wifi capabilities of my ESP32 to use this API. However, it does not produce sound. I want to look into this a little further for next week's assignment, which is to work on our final project more. However, this isn't my main priority, as my final project is a MIDI controller. Thus, I need the microcontroller and circuit to produce midi data that can be sent to DAWs, rather being the device that produces sound (a synthesizer). This would be cool to exlore as a second function, but for now I want to work more on getting the capacitive sensor midi to work properly, and then recreate this with multiple keys. Finally, as final touches or extra functions, to integrate potentiometer knobs to control parameters, and make a simple TCP display of notes.

## 3D model

For my final project, I wanted to case my midi controller in a mini piano-keyboard. Since a huge goal of my final project was to create a portable instrument, it was important to keep the casing minimal! I got the original files from thingiverse. I then edited (with the help of Professor Melenbrink) the top and bottom files to smooth out the logos and to cut out a space for the TCP display. Here are the [STL files](). 

![Assembled 3D model](midi.jpg)
![Side view](midiside.jpg)