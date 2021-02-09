# nrf_802154_delayed_echo_client

nrf_802154_delayed_echo_client sends a frame every two seconds and listens for a response
in a 10 millisecond reception window scheduled one second after a successful transmission.
This example application is designed to cooperate with nrf_802154_delayed_echo_server.  

## Build

Assuming build files have been generated (see top level README).
Invoke build tool with the target name in your build directory, e.g. using `make`
 
 ```bash
make nrf_802154_delayed_echo_client
 ```

## Flash

To flash created `.hex` file invoke `nrfjprog` from `build` directory.
If there is only one nRF device use

```bash
nrfjprog -f NRF52 --program nrf_802154_delayed_echo_client/nrf_802154_delayed_echo_client.hex --chiperase --reset
```

Otherwise, use below command, replacing `<serial_number>` with target device serial number.

```bash
nrfjprog -f NRF52 --program nrf_802154_delayed_echo_client/nrf_802154_delayed_echo_client.hex --chiperase --reset --snr <serial_number>
```

## Test

LEDs: LED1 toggles when a successful frame transmission is completed , LED2 toggles when a frame
is received.

Please note: transmitted frame is configured to require an acknowledgement.

Using sniffer: channel 11 is set, payload of every frame: "Nordic Semiconductor".
