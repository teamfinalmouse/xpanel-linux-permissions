# Finalmouse ULX udev rules

Welcome to the GitHub repository for the XPANEL / Finalmouse ULX udev rules! This repository contains the essential udev rules needed to ensure compatibility and proper permissions for Finalmouse ULX devices. These rules are particularly designed to work seamlessly with the XPANEL web application at [xpanel.finalmouse.com](https://xpanel.finalmouse.com).

## Overview

Udev is a device manager for the Linux kernel, which dynamically creates or removes device nodes in the `/dev` directory. For certain devices like the Finalmouse ULX, specific udev rules are required to set the correct permissions, allowing applications like [XPANEL](https://xpanel.finalmouse.com) to interact with them without needing root privileges.

This repository provides the necessary udev rules to facilitate this interaction, ensuring a smooth and secure experience for users of Finalmouse ULX devices on Linux systems.

## Installation

### Prerequisites

- A Linux-based operating system.
- A Finalmouse ULX device.

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
   sudo cp 99-finalmouse.rules /etc/udev/rules.d/
   ```

4. **Reload Udev Rules:**
   ```bash
   sudo udevadm control --reload-rules && sudo udevadm trigger
   ```

5. **Verify Installation:**
   Connect your Finalmouse ULX device and verify if it's detected correctly by the [XPANEL](https://xpanel.finalmouse.com) application.

## Usage

Once installed, the udev rules will automatically set the correct permissions for your Finalmouse ULX devices.
This allows the [XPANEL](https://xpanel.finalmouse.com) web application to detect and interact with your device without requiring additional configurations.

---

For more information or support, please visit [xpanel.finalmouse.com](https://xpanel.finalmouse.com) or open an issue in this repository.

