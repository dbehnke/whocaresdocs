# 📚 Complete Guide to Headless CachyOS (KDE Plasma/X11) Streaming

This document provides step-by-step instructions to configure a stable, headless **CachyOS** host for streaming via **Sunshine** and **Moonlight**, and guides the setup of the **Moonlight client** on macOS.

**NOTE:** Replace `youruserid` with your actual Linux username throughout this guide.

---

## Part 1: CachyOS Host Configuration (Headless Setup)

This section removes SDDM and sets up a reliable Xorg session using a Dummy Display Driver.

### I. Install Essential Software

Use the CachyOS package manager (`pacman`) to install the core utilities and the streaming host.

```bash
# 1. Install Xorg utilities, Dummy Driver, and Fish Shell (for compatibility)
sudo pacman -S xorg-xinit xorg-xhost xf86-video-dummy fish

# 2. Install Sunshine Streaming Host
# If using the official repo (preferred):
sudo pacman -S sunshine
# If using an AUR helper like yay:
# yay -S sunshine-git
```

### II. Configure the Headless Display (Dummy Driver)

This ensures the X server runs at a stable, scaled resolution (e.g., 1512x982 for a 14" MBP) to prevent the "tiny interface" HiDPI issue on the client.

1.  **Create the Xorg Configuration File:**

    ```bash
    sudo nano /etc/X11/xorg.conf.d/99-dummy-screen.conf
    ```

2.  **Add the Configuration:**

    ```ini
    Section "Screen"
        Identifier "Screen0"
        Device "DummyVideoCard"
        Monitor "DummyMonitor"
        DefaultDepth 24
        SubSection "Display"
            Depth 24
            Modes "1512x982" 
        EndSubSection
    EndSection

    Section "Monitor"
        Identifier "DummyMonitor"
    EndSection

    Section "Device"
        Identifier "DummyVideoCard"
        Driver "dummy"
        VideoRam 32000 
    EndSection

    Section "ServerLayout"
        Identifier "Layout0"
        Screen 0 "Screen0" 0 0
    EndSection
    ```

### III. Configure Boot & Auto-Start

1.  **Disable SDDM Service:**

    ```bash
    sudo systemctl disable sddm
    sudo systemctl stop sddm
    ```

2.  **Configure TTY Auto-Login (Universal Step):**
    This allows TTY1 to log in your user automatically at boot. **Replace `youruserid` with your actual username.**

    ```bash
    sudo systemctl edit getty@tty1.service
    ```

    Add this content:

    ```ini
    [Service]
    ExecStart=
    ExecStart=-/usr/bin/agetty --autologin youruserid --noclear %I $TERM
    ```

3.  **Configure Shell Auto-Start (`startx`):**
    Use the file for your shell.

      * **Bash (`~/.bash_profile`):**

        ```bash
        # --- Auto-start Xorg for Headless KDE Session ---
        if [ -z "$DISPLAY" ] && [ "$(tty)" = "/dev/tty1" ]; then
            exec startx
        fi
        ```

      * **Fish Shell (`~/.config/fish/config.fish`):**

        ```fish
        # --- Auto-start Xorg for Headless KDE Session ---
        if test (tty) = "/dev/tty1"
            if not set -q DISPLAY
                exec startx
            end
        end
        ```

### IV. Configure the Xorg Session (`.xinitrc`)

This script launches KDE Plasma and sets the authentication environment.

1.  **Create/Edit Xorg Startup Script (Universal):**
    ```bash
    nano ~/.xinitrc
    ```
    Add the following content:
    ```bash
    #!/bin/bash

    # Set display for the session
    export DISPLAY=:0

    # Grant local access to bypass MIT-MAGIC-COOKIE-1 key errors
    xhost +si:localuser:$(whoami)

    # Start the KWallet Daemon (required for NetworkManager and Wi-Fi)
    kwalletd6 &

    # Start the KDE Plasma X11 session
    exec startplasma-x11
    ```

### V. Final Host Setup and Service Activation

1.  **Fix KWallet Password Prompt:**

      * After the first reboot, log in via Moonlight.
      * Open KWallet Manager and set the password for your default wallet (`kdewallet`) to **blank (empty)**. Accept the security warning.

2.  **Fix Virtual Input Permissions:**
    To ensure Sunshine can send input, add your user to the input groups. **Replace `youruserid` with your actual username.**

    ```bash
    sudo usermod -aG input youruserid
    sudo usermod -aG uinput youruserid
    ```

    **You must REBOOT for these group changes to take effect.**

3.  **Configure Sunshine Systemd Service:**
    Ensure Sunshine runs as a user service and explicitly targets the correct display.

    ```bash
    mkdir -p ~/.config/systemd/user/sunshine.service.d
    nano ~/.config/systemd/user/sunshine.service.d/10-x11-env.conf
    ```

    Add the configuration:

    ```ini
    [Service]
    Environment="DISPLAY=:0"
    ```

4.  **Enable and Start Sunshine Service:**

    ```bash
    systemctl --user daemon-reload
    systemctl --user enable sunshine.service
    ```

5.  **Final Reboot:**

    ```bash
    sudo reboot
    ```

-----

## Part 2: Moonlight Client Setup (macOS)

### 1\. Install Moonlight and Connect

1.  **Install Moonlight:** Download and install the client for macOS from the official Moonlight Game Streaming website.
2.  **Launch Moonlight:** The application will search for hosts.
3.  **Add Host:** If not auto-detected, click **Add Host** and enter the hostname (e.g., `sunshinehost.local`) or the host's IP address.

### 2\. Pairing Devices (Using Web UI)

1.  **Initiate Pairing:** Click on the `sunshinehost.local` entry in the Moonlight client. A **4-digit PIN** will appear on your Mac's screen (e.g., 5678).
2.  **Access the Sunshine Web UI:** Open a web browser on your Mac and navigate to the Sunshine host's web interface:
    ```
    [https://sunshinehost.local:47990](https://sunshinehost.local:47990)
    ```
    *(Note: You must proceed through the security warning to access the page.)*
3.  **Enter the PIN:** In the **"Pairing"** dialogue box that appears on the web page, enter the **4-digit PIN** shown on your Moonlight client.
4.  **Verification:** Once paired, the PIN prompt on your Mac will disappear, and the Moonlight application will display the available desktop sessions.

### 3\. Start Streaming

1.  Click on the **"KDE Plasma"** desktop icon in Moonlight.
2.  The stream will begin, showing your headless CachyOS desktop.
