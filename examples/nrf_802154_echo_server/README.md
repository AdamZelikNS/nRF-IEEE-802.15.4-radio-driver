# nrf_802154_echo_server

nrf_802154_echo_server listens for frames and responds to the sender with the same frame it
received.
This example application is designed to cooperate with nrf_802154_echo_client.

## Build

Assuming build files have been generated (see top level README).
Invoke build tool with the target name in your build directory, e.g. using `make`
 
 ```bash
make nrf_802154_echo_server
 ```

## Flash

To flash created `.hex` file invoke `nrfjprog` from `build` directory.
If there is only one nRF device use

```bash
nrfjprog -f NRF52 --program nrf_802154_echo_server/nrf_802154_echo_server.hex --chiperase --reset
```

Otherwise, use below command, replacing `<serial_number>` with target device serial number.

```bash
nrfjprog -f NRF52 --program nrf_802154_echo_server/nrf_802154_echo_server.hex --chiperase --reset --snr <serial_number>
```

## Test

LEDs: LED3 toggles when a frame is received.

Using sniffer: channel 11 is set, payload of every transmitted frame is the same as payload
of a received frame, source and destination addresses are swapped.
