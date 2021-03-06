# Pi VU Meter

## ALSA Plugin to display a VU meter on various Raspberry Pi add-ons

### Installing

Currently, you will need to compile the pivumeter lib from source.

You may use our automated setup to do so, specifying the output device the wish to use (see `options` below):

```
setup.sh blinkt
```

if you'd rather compile and set things up yourself, read on!

#### pre-requisite

```
sudo apt-get install build-essential autoconf automake libtool libasound2-dev libfftw3-dev wiringpi
```

#### clone repository

if you haven't done so already, git clone this repository and cd into it:

```
git clone https://github.com/pimoroni/pivumeter
cd pivumeter
```

#### compiling from source


from the top of the repository, run the following to generate the MakeFile:

```
aclocal && libtoolize
autoconf && automake --add-missing
```

then, to compile and install:

```
./configure && make
sudo make install
```

### Options

Pi VU Meter supports various options in your `/etc/asound.conf`, these include:

#### output_device

Specify which device to display the VU meter on.

Supported devices:

* default (18-segment VU driven by SN3218)
* blinkt - Simple amplitude meter through Green->Yellow->Red
* speaker-phat - Simple amplitude meter
* scroll-phat - displays 11-band FFT-based EQ

#### brightness

Specify the pixel brightness from 0 to 255

#### Example

```
pcm_scope.pivumeter {
        type pivumeter
        decay_ms 500
        peak_ms 400
        brightness 128
        output_device blinkt
}
```

a full example of a suitable `asound.conf` file can be found in the `dependencies` directory.
