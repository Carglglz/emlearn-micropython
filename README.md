
# emlearn-micropython

[Micropython](https://micropython.org) integration for the [emlearn](https://emlearn.org) Machine Learning library for microcontrollers.

The goal is to enable applications to run ML inference on the microcontroller,
without having to touch any C code.

## Status
**Proof of Concept**

- Can run RandomForest/DecisionTree
- Pre-built modules are available for the most common
- Has been tested on `armv6m` (RP2040) and `x64` (Unix port)

Or contribute yourself!

## Prerequisites

Minimally you will need

- Python 3.10+ on host
- MicroPython running onto your device

#### Download repository

Download the repository with examples etc
```
git clone https://github.com/emlearn/emlearn-micropython
```

## Installing from a release

#### Find architecture

Identify which CPU architecture your device uses.
You need to specify `ARCH` to install the correct module version.

| ARCH          | Description                       | Examples              |
|---------------|-----------------------------------|---------------------- |
| x64           | x86 64 bit                        | PC                    |
| x86           | x86 32 bit                        |                       |
| armv6m        | ARM Thumb (1)                     | Cortex-M0             |
| armv7m        | ARM Thumb 2                       | Cortex-M3             |
| armv7emsp     | ARM Thumb 2, single float         | Cortex-M4F, Cortex-M7 |
| armv7emdp     | ARM Thumb 2, double floats        | Cortex-M7             |
| xtensa        | non-windowed                      | ESP8266               |
| xtensawin     | windowed with window size 8       | ESP32                 |

#### Download release files

Download from [releases](https://github.com/emlearn/emlearn-micropython/releases).

#### Install on device

Copy the .mpy file for the correct `ARCH` to your device.
```
mpremote cp emltrees-$ARCH.mpy :emltrees.mpy
```

NOTE: If there is no ready-made build for your device/architecture,
then you will need to build the .mpy module yourself.

## Usage

NOTE: Make sure to install the module first.

Train a model with scikit-learn
```
pip install emlearn scikit-learn
python examples/xor_train.py
```

Copy model file to device

```
mpremote cp xor_model.csv :xor_model.csv
```

Run program that uses the model

```
mpremote run examples/xor_run.py
```


## Developing locally

#### Prerequisites
These come in addition to the prequisites described above.

Make sure you have the dependencies needed to build for your platform.
See [MicroPython: Building native modules](https://docs.micropython.org/en/latest/develop/natmod.html).

We assume that micropython is installed in the same place as this repository.
If using another location, adjust `MPY_DIR` accordingly.


#### Build

Build the .mpy native module
```
make -C eml_trees/ ARCH=x64 MPY_DIR=../../micropython
```

Install it on device
```
mpremote cp emltrees/emltrees.mpy :emltrees.mpy
```

#### Run tests

`TODO: implement and document`

