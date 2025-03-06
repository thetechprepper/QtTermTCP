# QtTermTCP for Mobian

This is a modified version of QtTermTCP designed to run on the PinePhone
under Mobian 12.

## Build & Runtime Dependencies

1. Install Qt5 development tools.

```
sudo apt install \
  qtbase5-dev \
  qtbase5-dev-tools \
  qt5-qmake \
  qtchooser \
  qtmultimedia5-dev \
  libqt5serialport5-dev \
  libfftw3-dev \
  qttools5-dev-tools \
  -y
```

2. Install `socat`.


```
sudo apt install socat -y
```

## Build Instructions

1. Run `qmake` to produce a suitable Makefile.

2. Run `make` to compile and produce `QtTermTCP`.


## Connecting to QtTermTCP

This integration is designed to work with a radio that supports a
Bluetooth TNC such as the BTECH UV Pro.

1. Pair your radio with the PinePhone. 

2. Associate the Bluetooth TNC to a device. Replace the MAC address
   accordingly.

```
sudo rfcomm connect /dev/rfcomm0 38:D2:00:00:ED:C8
```

3. Bind the a KISS TCP port to `/dev/rfcomm0`.

```
socat -d TCP-LISTEN:8100,reuseaddr,fork FILE:/dev/rfcomm0,raw
```

4. Open QtTermTCP and configure the KISS connection under _Setup_.

    1. Enable KISS Interface = checked
    2. MYCALL = set to your callsign
    3. Serial TNC > Select Device: `TCP`
    4. TCP Setup > Host: 127.0.0.1
    5. TCP Setup > Port: 8100

