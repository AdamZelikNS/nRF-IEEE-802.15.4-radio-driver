# nRF 802.15.4 radio driver - examples

Example bare-metal applications for nRF IEEE 802.15.4 radio driver are provided to familiarize you
with the radio driver API and reduce amount of work required to create your own IEEE 802.15.4
compliant application.

## Required hardware

Provided examples are compatible with the nRF52840 DK.

## Toolchain

Tools required to build the examples and program the board are as follows.

**CMake** - version 3.13.1 or above - is required to generate the build scripts for a build tool of
choice. This manual uses `make`.

**ARMGCC** - version 9-2019-q4-major - is required to build the examples. Provided CMake files assume
the ARM Toolchain is included in the path.

**nRF5x Command Line Tools** - version 9.4.0 - are required as they provide `nrfjprog` utility used
to program the target device.

## Project structure

Assuming project tree as shown below, provided code snippets can be used directly.

```
project_directory
|--build
|--nRF-IEEE-802.15.4-radio-driver
   |--examples
   |  |--CMakeLists.txt    <- top level examples CMakeLists.txt
   |--...                  <- radio driver files
```

## Genrate build scripts

Invoke cmake with path to the deployed examples directory in the nRF-IEEE-802.15.4-radio-driver directory.

```bash
cd build
cmake ../nRF-IEEE-802.15.4-radio-driver/examples
```
&nbsp; <!--- Blank line -->

---

**NOTE**: Prepared build and flash commands are provided for every example in its `README.md` file.

---

&nbsp; <!--- Blank line -->

## Build

Invoke build tool with the target name in your build directory, e.g. using `make`.
Replace `<target_example_name>` with the example name being the example directory name.

 ```bash
make <target_example_name>
 ```

## Flash

To flash created `.hex` file invoke `nrfjprog` from `build` directory.

If there is only one nRF device use

```bash
nrfjprog -f NRF52 --program <target_example_name>/<target_example_name>.hex --chiperase --reset
```

Otherwise, use below command, replacing `<serial_number>` with target device serial number.

```bash
nrfjprog -f NRF52 --program <target_example_name>/<target_example_name>.hex --chiperase --reset --snr <serial_number>
```
Serial numbers of connected devices can be obtained by invoking

```bash
nrfjprog -i
```

## Test

For notes on testing the examples refer to `README.md` files in the example directory.

## Creating application out of tree

Project hierarchy is assumed to be as presented below.

```
nRF-IEEE-802.15.4-radio-driver
|--examples
|  |--common
|  |--CMake
|  |--...               <- example directories
|  |--CMakeLists.txt    <- top level examples CMakeLists.txt
|--external             <- externals used by radio driver and apps
|  |--nrfx
|  |  |--mdk            <- linker scripts are not exported
|  |  |--...            <- exported by radio driver
|  |--...               <- exported by radio driver
|--lib
|--CMakeLists.txt       <- radio driver CMakeLists.txt
|--...                  <- radio driver files
```
Provided example applications depend on radio driver and its externals. Therefore moving an
existing application or creating a new one requires changes in added subdirectories. If hierarchy
between radio driver and its externals is preserved, only radio driver directory must be added.

nRF MDK provides linker scripts, therefore a CMake variable USER_LINK_DIR pointing to a directory
containing required linker scripts (e.g. nRF MDK directory) must be provided.
