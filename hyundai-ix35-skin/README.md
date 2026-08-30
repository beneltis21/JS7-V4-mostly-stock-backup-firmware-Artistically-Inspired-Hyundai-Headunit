# JS7 V4 Hyundai IX35 Android System Customisation

## Status: experimental / partially hardware-validated

This package is an exact-build-gated Hyundai IX35 Android interface, boot-asset and identity customisation for one JS7 V4 platform. It is **not stock firmware**, **not an official Hyundai release**, and **not a platform-independent JS7 update**.

![Frame from the included Hyundai 1024x600 boot video](../docs/images/hyundai-boot-11s.jpg)

*A frame extracted from the exact 13.52-second Hyundai boot video included in V1.2.*

The package is guarded for:

| Item | Required value |
| --- | --- |
| Product | `full_k80_bsp` |
| Device | `k80_bsp` |
| Build | `CMDAZX80-U1_R8010_S6.14` |
| Android | 8.1.0 / API 27 |
| Platform | MediaTek MT6580 family, ARMv7 32-bit |
| Mainboard reference | `JS-78-MB_V4.0`, dated `2026.01.09` |
| CPU-board reference | `MT80_MINI_P03_V1.0`, dated `2024.12.11` |

## Modification scope

- Hyundai dashboard V0.5.1 (`com.js7.hyundai`).
- Dashboard source code and build notes.
- Hyundai 1024×600 H.264 boot video.
- Black 1024×600 early-boot bitmap.
- Hyundai IX35 Bluetooth, hotspot and Android identity settings.
- Hyundai / Hyundai IX35 CarPlay make and model configuration.
- 12-hour clock and `Australia/Sydney` timezone.
- Backup, installation, verification and rollback scripts.
- A local Wi-Fi identity helper.
- Persistent USB ADB without computer-key authorisation.

The Hyundai dashboard does not request Android's `INTERNET` permission. This does not prevent Google Maps, CarPlay, Android Auto or existing factory applications from using their own network permissions.

## Critical ADB security characteristic

V1.2 intentionally changes `ro.adb.secure` from `1` to `0` and keeps the USB `adb` function enabled. Any computer with physical access to a working USB data port may obtain ADB access without the normal trusted-computer prompt.

This materially reduces host-authentication security. Deployment requires explicit acceptance of that risk. Backup and rollback scripts are included, but rollback remains dependent on a bootable Android userspace and functional privileged ADB transport.

## Physical validation result

The following was observed on the matching physical unit:

- The package passed its ZIP and SHA-256 integrity checks.
- The Hyundai dashboard APK installed successfully.
- The Hyundai boot video displayed during boot.
- The unit completed a later normal boot and was not bricked.

The recorded full V1.2 run did **not** reach its final verification message. The device-side installer was terminated with `Killed` after it began applying identity, clock and boot configuration. Some changes applied, but the complete automated V1.2 process was not proven end-to-end in that run.

Accordingly, the public classification is **experimental / partially hardware-validated**; end-to-end installer completion has not been demonstrated.

## Public sanitised package

```text
JS7_HYUNDAI_IX35_V4_SKIN_V1.2_PUBLIC_SANITISED.zip
SHA-256: b857b7be1f59d2ae2eba157428ac5468197b03e44021d46a310caf8e000a4f9f
```

The release package includes its own `README_FIRST.txt`, offline-validation record, privacy audit, asset hashes, installer, verifier and rollback scripts. Read those files before running anything.

The private source ZIP had SHA-256
`7ed1a9a4aec9198d128b116f992a7c85922ec64292b8af5cc4b40e06ba78b2f2`.
It is retained only as provenance and is not included publicly. The public
derivative removes the captured local IP, an old personal Wi-Fi name and all
owner-specific default ADB targets. It contains no raw device dump.

## Intended exclusion scope

The package is designed not to replace the preloader, LK/LK2, boot, recovery, vendor, NVRAM/NVDATA, MCU, CAN data, radio, amplifier configuration, touch configuration or vehicle services. It does write selected files and properties under Android's `/system`, installs the dashboard APK and invokes the unit's boot-logo updater.

## Deployment prerequisites

1. Confirm every required product/device/build value above.
2. Use stable, correctly fused 12 V power.
3. Verify root ADB access before beginning.
4. Keep the complete stock backup produced by the installer.
5. Do not interrupt power during system or boot-logo writes.
6. Treat a Wi-Fi ADB disconnect during reboot as expected, but treat an earlier `Killed` or error message as an incomplete installation.

Use is at your own risk. Similar model names, seller listings or processor labels are not sufficient compatibility evidence.

Hyundai names and marks belong to their respective owner. This independent package is not produced, endorsed or supported by Hyundai.
