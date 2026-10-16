# Finalmouse udev rules

Welcome to the GitHub repository for the XPANEL / Finalmouse udev rules! This repository contains the essential udev rules needed to ensure compatibility and proper permissions for Finalmouse devices. These rules are particularly designed to work seamlessly with the XPANEL web application at [xpanel.finalmouse.com](https://xpanel.finalmouse.com).

## Overview

Udev is a device manager for the Linux kernel, which dynamically creates or removes device nodes in the `/dev` directory. For certain devices like the Finalmouse devices, specific udev rules are required to set the correct permissions, allowing applications like [XPANEL](https://xpanel.finalmouse.com) to interact with them without needing root privileges.

This repository provides the necessary udev rules to facilitate this interaction, ensuring a smooth and secure experience on Linux systems.

## Installation

### Prerequisites

- A Linux-based operating system, that supports udev (almost any modern distro will)
- A supported Finalmouse device (see [Supported devices](#supported-devices)).

### Supported devices

| Device | USB IDs (`361d:xxxx`) |
| --- | --- |
| ULX / Falcon module | `0100`–`0104`, `0111` |
| Centerpiece Pro | `0200`–`0203` (+ `1fc9:0021`) |
| StarlightX (SLX) dongle | `0300`, `0302` (bootloader) |
| StarlightX (SLX) mouse | `0310`, `0312` (bootloader) |

The SLX bootloaders show up as a USB serial (CDC-ACM) port rather than a HID device, so the rules also grant access to that serial port and tell ModemManager to leave it alone. No `dialout`/`uucp` group membership is needed.

### Steps

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/teamfinalmouse/xpanel-linux-permissions
   ```
   
2. **Navigate to the Repository:**
   ```bash
   cd xpanel-linux-permissions
   ```

3. **Copy the Udev Rule:**
   ```bash
   sudo cp 70-finalmouse.rules /etc/udev/rules.d/
   ```

4. **Reload Udev Rules (or reboot):**
   ```bash
   sudo udevadm control --reload-rules && sudo udevadm trigger
   ```
   Then unplug and replug your device (including the dongle).

5. **Verify Installation:**
   Connect your Finalmouse device and verify if it's detected correctly by the [XPANEL](https://xpanel.finalmouse.com) application.

## Usage

Once installed, the udev rules will automatically set the correct permissions for your Finalmouse devices.
This allows the [XPANEL](https://xpanel.finalmouse.com) web application to detect and interact with your device without requiring additional configurations.

If you installed an older version of this file, copy it again to pick up newly supported devices.

## Troubleshooting

- Make sure the file is named `70-finalmouse.rules` (or anything sorting before `73`). `TAG+="uaccess"` has no effect in files sorted later, such as `99-...`.
- Check that your user got access (look for a `user:<you>:rw-` line):
  ```bash
  getfacl /dev/hidraw*            # mouse / dongle
  getfacl /dev/ttyACM*            # SLX bootloader
  ```
- `uaccess` only applies to users with an active local session; it doesn't apply over SSH.

---

For more information or support, please visit [xpanel.finalmouse.com](https://xpanel.finalmouse.com) or open an issue in this repository.

