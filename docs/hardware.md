## GarHAge Hardware

GarHAge can be built to support:
1. Up to two overhead garage doors (requiring a relay and reed/magnetic switch per door)
1. Up to two auxiliary doors (requiring a reed/magnetic switch per door)
1. Temperature and humidity readings (requiring a DHT11 or 22 sensor) 

### Bill of Materials

The following is a list of example parts required to build a feature-complete GarHAge unit:

| No. | Qty | Part | Link | Approx Price (ea) |
| --- | --- | ---- | ---- | ------------ |
| 1. | 1 | ESP8266-based microcontroller (e.g. NodeMCU) | [Link](https://www.amazon.com/ESP8266-NodeMcu-development-Internet-HONG111/dp/B06XBSV95D/ref=sr_1_6?ie=UTF8&qid=1504449670&sr=8-6&keywords=nodemcu) | $ 7.00 |
| 2. | 1 | Dual-relay module | [Link](http://www.robotshop.com/en/2-channel-5v-relay-module.html) | $ 4.00 |
| 3. | 4 | Reed/Magnetic door switches | [Link](http://a.co/bEomwwP) | $ 12.00 |
| 4. | 1 | DHT 11 sensor | [Link](http://a.co/aSYmtVi) | $ 7.00 |
| 4. | 1 | _OR_ DHT 22 sensor | [Link](http://a.co/fZQ35Ao) | $ 8.00 |
| 5. | 1 | 5v MicroUSB power supply | [Link](http://www.robotshop.com/en/wall-adapter-power-supply-5vdc-2a.html) | $ 6.00 |
| 6. | 1 | Mini solderless breadboard (170 tie-point) | [Link](http://www.robotshop.com/en/170-tie-point-mini-self-adhesive-solderless-breadboard-white.html) | $ 4.00 |
| 7. | | Bell/low voltage two-conductor wire | | |
| 8. | | Male-to-female breadboard jumper wires | | |
| 9. | | Project box or case | | |

**Approximate total cost for major components:** $ 80.00, buying most items from Amazon or Robotshop; much less if you source your components direct from China (e.g. AliExpress, BangGood, GearBest).

### Detailed Bill of Materials

#### 1. ESP8266-based microcontroller

I recommend the NodeMCU as GarHAge was developed and is tested on it. Its advantages are:
- it comes with header pins already soldered so that it can plug directly into a mini solderless breadboard;
- its VIN (or VU on the LoLin variant) port can power the 5v relay module;
- it can be powered and programmed via MicroUSB;
- it has Reset and Flash buttons, making programming easy.

Accordingly, this guide is written with the NodeMCU in mind.

But, Garhage should also work with the Adafruit HUZZAH, Wemos D1, or similar, though you may need to adjust the GPIO ports used in `config.h` to match the ESP8266 ports that your microcontroller makes available.

#### 2. Dual 5v relay module

A dual 5v relay module (as opposed to individual 5v relays) makes setup easy: just plug jumper wires from the module's VCC, CH1, CH2, and GND pins to the NodeMCU. These relay modules generally also include LEDs to ease troubleshooting.

Most importantly, because the relay module is powered by 5v, its inputs can be triggered by the NodeMCU's GPIOs.

GarHAge will work with relay modules that are active-high or active-low, defaulting to active-high relay support.

If using an active-low relay, be sure to set the relevant configuration parameter in `config.h`, and test thoroughly to be sure that your garage door opener(s) are not inadvertently triggered after a momentary power-loss.

#### 3. Reed/magnetic door switches

GarHAge will work with reed switches that are normally-open or normally-closed, defaulting to normally-open switch support. Many switches with screw terminals are available, making placement and wiring easy.

If using a normally-closed switch, be sure to set the relevant configuration parameter in `config.h`.

#### 4. DHT11 or 22 sensor

GarHAge can provide temperature and humidity readings from your garage via an attached DHT11 or 22, defaulting to DHT11 sensor support. 

However, the DHT22 is recommended as it is usually only slightly more expensive, is more accurate, and has a wider measurement range. If using a DHT22, be sure to set the relevant configuration parameter in `config.h`.

#### 5. 5v MicroUSB power supply

Power your NodeMCU via the same type of power supply used to charge Android phones or power a RaspberryPi. Powering the NodeMCU via MicroUSB is important since the relay module can then be powered via the NodeMCU VIN (or VU on the LoLin variant) port.

#### 6. Mini solderless breadboard (170 tie-point)

The NodeMCU mounts to this breadboard nicely, leaving one female port next to each NodeMCU port and making it easy to use male-to-female jumper wires to make connections from the NodeMCU to the relay module. The bell wire attached to the reed switches will also slide into the breadboard ports, making for a clean and solderless installation. Finally, these mini breadboards often also have an adhesive backing, making mounting in your project box easy.

#### 7. - 9. Miscellaneous parts

To install GarHAge, you will also require:
- Enough bell/low voltage two-conductor wire to make connections from each reed/magnetic switch at your garage doors to where GarHAge is mounted and to make connections from GarHAge to each garage door opener.
- Male-to-female breadboard jumper wires to make connections from the NodeMCU to the dual-relay module (4 jumper wires required).
- a project box to hold both the NodeMCU and dual-relay module.