# Kaldrivon SiteWatch

SiteWatch is a small network probe for remote sites, built on the M5Stack Atom Lite (ESP32). It sits on the site's Wi-Fi, measures the gateway, the internet and DNS, and reports to your monitoring tool over standard interfaces.

## What it does

- Measures gateway latency, jitter and packet loss, internet reachability, DNS lookup time and Wi-Fi signal.
- Raises alarms (gateway unreachable, internet unreachable, high packet loss, high latency, weak Wi-Fi, trial or update coverage ending) and clears them again.
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

Current release: **0.6.0-beta.7** (pre-release). Download it from **Releases**. It is a beta: one NETCONF session is served at a time.

## Flashing a probe

You need a PC with Chrome or Edge and a USB cable.

1. From the latest release, download `kaldrivon-probe-flasher.html` and `atom-probe-<version>-merged.bin`.
2. Open the flasher page in Chrome or Edge, connect the probe, pick the `.bin` file and click Flash.
3. Use the Manage tab to set the Wi-Fi and the NETCONF login. The probe restarts and joins your Wi-Fi.

`SHA256SUMS` in the release lets you check the files. GitHub carries the baseline build. Newer builds (fixes and features) come to licensed probes over the air, and are also available to download in your account at https://portal.kaldrivon.com while the license's update period covers them; the flasher page can install those over USB too and keeps the probe's settings.

## Licensing

A new probe starts with a 30-day trial. After the trial (plus 3 days) a probe without a license stops its NETCONF, Call Home and VES interfaces until a license is added; Wi-Fi, USB setup and the Manage page keep working so it can be activated. A purchased license is permanent and is tied to the probe's Device ID. It is added in your Kaldrivon account at https://portal.kaldrivon.com. Update coverage has an end date; a probe keeps working after that, it just does not receive newer firmware. The probe raises minor, major and critical alarms as the end of the trial (14, 7 and 2 days) or of the update coverage (60, 30 and 7 days) approaches, and shows the days left on the Manage tab.

## Third-party software

The firmware uses libssh (LGPL-2.1), ESP-IDF and mbed TLS (Apache-2.0), Monocypher (CC0 / BSD-2-Clause) and IETF YANG modules (BSD-3-Clause). Each release includes the license texts and the libssh source with the steps to rebuild the firmware with a modified libssh.

## Contact

Kaldrivon, https://kaldrivon.com
