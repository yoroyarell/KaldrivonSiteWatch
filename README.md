# Kaldrivon SiteWatch

SiteWatch is a small network probe for remote sites, built on the M5Stack Atom Lite (ESP32). It sits on the site's Wi-Fi, measures the gateway, the internet and DNS, and reports to your monitoring tool over standard interfaces.

## What it does

- Measures gateway latency, jitter and packet loss, internet reachability, DNS lookup time and Wi-Fi signal.
- Raises alarms (gateway unreachable, internet unreachable, high packet loss, high latency, weak Wi-Fi) and clears them again.
- NETCONF over SSH (RFC 6241, 6242) with `ietf-alarms` notifications, Call Home (RFC 8071) for probes behind NAT, and optional VES push.
- Set up from a browser over USB, no tools to install.
- Signed over-the-air updates.

## Monitoring with Kaldrivon MiniSMO

A probe connects to Kaldrivon MiniSMO as an external network function:

- **Alarms** arrive as NETCONF notifications (`ietf-alarms`).
- **Measurements** (gateway latency, jitter and loss, internet latency, DNS lookup time, Wi-Fi signal and drops) are read from the probe's YANG model or pushed as VES `perf3gpp` reports.
- **Behind NAT or a firewall:** turn on Call Home. The probe opens the connection to MiniSMO, so no inbound port is needed at the site.
- **Setup:** MiniSMO can provision the probe's VES destination itself, over NETCONF.

Any other NETCONF client or VES collector can use the same interfaces.

## Status

The first production release is not published yet. Release files will appear under **Releases** when it is.

## Flashing a probe

The flasher page and the firmware image will be published here with the first release. It runs in Chrome or Edge on a PC and talks to the probe over USB.

## Licensing

A new probe starts with a 30-day trial. A purchased license is permanent and is tied to the probe's Device ID. It is added in your Kaldrivon account at https://portal.kaldrivon.com. Update coverage has an end date; a probe keeps working after that, it just does not receive newer firmware.

## Third-party software

The firmware uses libssh (LGPL-2.1), ESP-IDF and mbed TLS (Apache-2.0), Monocypher (CC0 / BSD-2-Clause) and IETF YANG modules (BSD-3-Clause). Each release includes the license texts and the libssh source with the steps to rebuild the firmware with a modified libssh.

## Contact

Kaldrivon, https://kaldrivon.com
