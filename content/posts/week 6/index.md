---
title: "Week 6"
date: 2021-03-9T21:48:03-08:00
draft: false
---

## Week 6: Sensors

This week, I used an accelerometer to measure the XYZ location and the acceration of my breadboard!

#### Materials
I used the M0 Metro Circuit from Adafruit, and an Adafruit lis3dh accelerometer from the ps70 kit.

I followed along this [Adafruit Guide!](https://learn.adafruit.com/adafruit-lis3dh-triple-axis-accelerometer-breakout/arduino) at first in order to gain a better understanding of how this sensor works.

#### How It Works

The Adafruit LIS3DH triple-Axis Accelerometer Breakout has three axis sensing. The senor communicates both through l2C or SPI, for hardware and software control. l2C works with 2 wires, the Serial Clock (SCL) and Serial Data (SDA).

I connected Vin to the power supple of 5V, the ground pin to ground, the SCL (SCK) pin to Digital #13, the SDO pin to Digital #12, the SDA (SDI) to Digital pin #11, and the CS pin to Digital #10. 

The CS pin is the chip select pin, which is a command pin that connects the I/O pins on the accelerometer to the internal circuitry .. something to learn more about!

![Button](accelboard.jpg)

#### Code
I got the initial code from the Adafruit acceleration example! I had to download a few libraries in order to get there.

```cpp

// Basic demo for accelerometer readings from Adafruit LIS3DH

#include <Wire.h>
#include <SPI.h>
#include <Adafruit_LIS3DH.h>
#include <Adafruit_Sensor.h>

// Used for software SPI
#define LIS3DH_CLK 13
#define LIS3DH_MISO 12
#define LIS3DH_MOSI 11
// Used for hardware & software SPI
#define LIS3DH_CS 10

// software SPI
Adafruit_LIS3DH lis = Adafruit_LIS3DH(LIS3DH_CS, LIS3DH_MOSI, LIS3DH_MISO, LIS3DH_CLK);
// hardware SPI
//Adafruit_LIS3DH lis = Adafruit_LIS3DH(LIS3DH_CS);
// I2C
//Adafruit_LIS3DH lis = Adafruit_LIS3DH();

void setup(void) {
  Serial.begin(115200);
  while (!Serial) delay(10);     // will pause Zero, Leonardo, etc until serial console opens

  Serial.println("LIS3DH test!");

  if (! lis.begin(0x18)) {   // change this to 0x19 for alternative i2c address
    Serial.println("Couldnt start");
    while (1) yield();
  }
  Serial.println("LIS3DH found!");

  // lis.setRange(LIS3DH_RANGE_4_G);   // 2, 4, 8 or 16 G!

  Serial.print("Range = "); Serial.print(2 << lis.getRange());
  Serial.println("G");

  // lis.setDataRate(LIS3DH_DATARATE_50_HZ);
  Serial.print("Data rate set to: ");
  switch (lis.getDataRate()) {
    case LIS3DH_DATARATE_1_HZ: Serial.println("1 Hz"); break;
    case LIS3DH_DATARATE_10_HZ: Serial.println("10 Hz"); break;
    case LIS3DH_DATARATE_25_HZ: Serial.println("25 Hz"); break;
    case LIS3DH_DATARATE_50_HZ: Serial.println("50 Hz"); break;
    case LIS3DH_DATARATE_100_HZ: Serial.println("100 Hz"); break;
    case LIS3DH_DATARATE_200_HZ: Serial.println("200 Hz"); break;
    case LIS3DH_DATARATE_400_HZ: Serial.println("400 Hz"); break;

    case LIS3DH_DATARATE_POWERDOWN: Serial.println("Powered Down"); break;
    case LIS3DH_DATARATE_LOWPOWER_5KHZ: Serial.println("5 Khz Low Power"); break;
    case LIS3DH_DATARATE_LOWPOWER_1K6HZ: Serial.println("16 Khz Low Power"); break;
  }
}

void loop() {
  lis.read();      // get X Y and Z data at once
  // Then print out the raw data
  Serial.print("X:  "); Serial.print(lis.x);
  Serial.print("  \tY:  "); Serial.print(lis.y);
  Serial.print("  \tZ:  "); Serial.print(lis.z);

  /* Or....get a new sensor event, normalized */
  sensors_event_t event;
  lis.getEvent(&event);

  /* Display the results (acceleration is measured in m/s^2) */
  Serial.print("\t\tX: "); Serial.print(event.acceleration.x);
  Serial.print(" \tY: "); Serial.print(event.acceleration.y);
  Serial.print(" \tZ: "); Serial.print(event.acceleration.z);
  Serial.println(" m/s^2 ");

  Serial.println();

  delay(200);
}
```


#### Calibrating
I wasn't actually sure how to calibrate this accelerometer. I played around with the accelerometer to move it back and forth and different speeds. As I move it back and forth, I suspected that the faster I move it, the more acceleration there would be, especially during my "turning points" when I switch from moving it one direction to another.

<!-- ![Chart](moving.MOV) -->
{{< youtube id="Gh7k_WlOMco" title="Moving the accelerometer" >}}

However, I don't think this was the best way of testing, as I didn't get much of a takeaway result. It might be that the m/s^2 is too large of a unit.

Another issue I wondered about is why the acceleration was still around 9.8 m/s^s when sitting absolutely still on my desk. Is it possible that the LIS3DH is also measuring the gravitational pull of the Earth? Or is this just a coincidence? I might have to look more into how it works! At first I thought it might be in the code (as a default acceleration that it sets), but I couldn't parse something that seemed to indicate this.


Here's the original data:
<!-- ![Serial Monitor](serialmon.MOV) -->

![Chart](chart.png)

This is in the serial moniter, and the data shows us the XYZ data. As you can see, as the accelrmoter is still, these values are near 0.

And here's the graph:
![Graph](accelgph.png)

#### Capacitative sensor
A Mask! From class
![Mask](IMG_6443.jpg)

#### Graph
As the pressure increases (aka, as the sensors are closer together), the more output!
![Graph](mask.png)