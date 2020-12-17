# ![safecerthax logo](https://safecerthax.rocks/assets/images/cover.png)
This is a [mitmproxy](https://mitmproxy.org) script for [safecerthax](https://github.com/MrNbaYoh/safecerthax). You can use it to spoof official 3DS NUS servers and exploit safecerthax _**only**_ on O3DS/2DS SAFE_FIRM to run [SafeB9SInstaller](https://github.com/d0k3/SafeB9SInstaller). 

For more information on safecerthax, please visit the [safecerthax website](https://safecerthax.rocks).

*Note:* this repository only contains the python script for mitmproxy, please check out the [safecerthax repository](https://github.com/MrNbaYoh/safecerthax) for the actual exploit code.

## How to use?

### Computer-side

##### Requirements
- [Python 3](https://python.org)
- [mitmproxy](https://mitmproxy.org)

##### Running
To start the proxy server, run the following command:
```
mitmproxy -s safecerthax.py
  --set certs=\*=<fake_certificate>
  --set client_certs=<client_certificate>
  --ssl-insecure
  --set relax_http_form_validation
  --set certhax_payload=<safecerthax_binary>
  --set arm9_payload=<kernelhaxcode_3ds_binary>
```

With:
- `fake_certificate`: the path to your fake certificate (in PEM format) created with [SSLoth](https://github.com/MrNbaYoh/3ds-ssloth) that mimics the certificate for `*.c.shop.nintendowifi.net` domains.
-  `client_certificate`: the path to the ClCertA `ctr-common-1-cert` (in PEM format).
- `safecerthax_binary`: the path to the `safecerthax.bin` binary file.
- `kernelhaxcode_3ds_binary`: the path to the `kernelhaxcode_3ds.bin` binary file.

This will start the safecerthax proxy on port 8080.

### 3DS-side
Follow these steps:

1. Put the `SafeB9SInstaller.bin` at the root of your SD card.
2. In the system settings, edit your network configuration to add the proxy server (IP of your computer + port 8080).
3. Reboot in recovery mode (press L+R+Up+A at startup).
4. Confirm you want to update.
5. An error message should pop up. Close it.
6. The exploit should run and launch SafeB9SInstaller.
