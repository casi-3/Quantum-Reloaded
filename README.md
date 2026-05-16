# Quantum Reloaded - Automatic qBittorrent Port Updater for ProtonVPN

This application monitors the Windows ProtonVPN client log files for port changes and passes them to qBittorrent through its WebUI.

## About this fork

Quantum Reloaded is a community continuation of **Quantum**, originally created by **UHAX**:
https://github.com/UHAXM1/Quantum

The original project is no longer maintained. This fork keeps it working with current qBittorrent versions and adds a couple of requested features. All credit for the original application goes to UHAX. It is released under the same licence (GPL-3.0) and the original copyright is kept.

## What is new in Reloaded

- Works with **qBittorrent 5.2+**, tested against a real qBittorrent 5.2 instance. The port is now updated with a single targeted call instead of rewriting every preference.
- **Single file**: one `Quantum.exe`, nothing else to install. The .NET runtime is included in the file.
- Updated to **.NET 10**.
- **Self-signed HTTPS support**: an option to ignore certificate errors, for a qBittorrent WebUI served over HTTPS with a self-signed certificate.
- **Post-update script**: run your own `.bat`, `.cmd`, `.ps1` or `.exe` after the port is updated. The new port is passed as the first argument and as the `QUANTUM_PORT` environment variable. The exit code is written to the log.
- Builds again from a clean checkout (the original was missing a reference and would not compile).

## Requirements

The single `Quantum.exe` needs nothing else, just run it on Windows. You still need the Windows ProtonVPN client (with port forwarding) and qBittorrent with the WebUI enabled.

To build from source you need .NET 10 and the qBittorrent-net-client submodule:
```
git clone --recurse-submodules https://github.com/casi-3/Quantum-Reloaded
```
Submodule used: https://github.com/fedarovich/qbittorrent-net-client

## How it works

Once you give it your qBittorrent connection details, Quantum finds the ProtonVPN log directory automatically and checks it once a minute. When the forwarded port changes it pushes the new port to qBittorrent.

## qBittorrent setup

1. Open qBittorrent, go to Tools > Options (or Alt + O).
2. Open the Web UI section and enable the Web User Interface (remote control).
3. Set a username and password, or enable "Bypass authentication for clients on localhost" (then you can leave them blank).
4. To reach it from other devices, set the IP address to 0.0.0.0 and check your firewall.
5. Optionally enable HTTPS with a certificate and key.
6. Apply, then OK. Check the WebUI works in a browser.

## Quantum setup

1. Launch Quantum. If it does not appear, check the system tray and double-click the icon.
2. Startup: enable or disable Quantum starting when you log in (per account).
3. Log file: leave automatic detection on. If you select it manually you have to redo it after every ProtonVPN update.
4. Host: `http://127.0.0.1:8080` by default. Change the IP/port for a remote instance. If you use HTTPS, change `http` to `https`.
5. Username and password: the ones from the qBittorrent setup above (blank if you use localhost bypass).
6. If your WebUI uses a self-signed HTTPS certificate, tick "Ignore certificate errors (self-signed HTTPS)".
7. Optionally set a post-update script.
8. The Test / Save / Update Port Now button is dynamic: it tests and saves the configuration, or forces an immediate port update.

Closing the window minimises Quantum to the system tray.

## Troubleshooting

**qBittorrent 5.x answers 401 / Unauthorized to everything (even the login page).** qBittorrent 5.x validates the Host header, including the port. If qBittorrent is behind a port mapping or a reverse proxy (the port you connect to is different from the port qBittorrent actually listens on), it rejects every request. Fix it on the qBittorrent side: connect on its real port, or set `WebUI\HostHeaderValidation=false` in the configuration file (Web UI options), or set the allowed server domains.

## Licence

GPL-3.0, same as the original. See LICENSE. Original project and author: https://github.com/UHAXM1/Quantum
