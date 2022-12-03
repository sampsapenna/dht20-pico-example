# Aosong AHT20/DHT20 Sensor Raspberry Pi Pico SDK example
An example / demo of periodically fetching temperature and humidity values
from the sensor, and updating them on the standard output. The example code
uses the [dht20-pico library.](https://github.com/sampsapenna/dht20-pico)

> CAUTION: USE 3.3V RAIL FOR POWERING THE AHT20/DHT20 SENSOR, USING 5V
> FOR POWER CAN LEAD TO A BRICKED RP2040 DUE TO INCORRECT I2C BUS VOLTAGE

## Getting started
Repository contains `pico sdk` and `dht20-pico` as submodules. Before
compiling run
```bash
git submodule init && git submodule foreach "git submodule init && git submodule update"
```

## Usage
To build the software run following commands.
```bash
mkdir build
cd build
cmake ..
make
```

Copy the resulting `dht20_example.uf2` on your Pico. Be sure to connect the
correct i2c pins. Raspberry Pi Pico defaults are pins 6 and 7.
