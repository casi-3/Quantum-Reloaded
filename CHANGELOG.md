# Changelog

## 1.6.1

### Fixed
- "No valid port information found in logs" when a previous ProtonVPN version directory was left next to the current one. Quantum now scans every `v*\ServiceData\Logs\service-logs.txt` under the install root and picks the most recent.
- Same error when the log file Quantum was pointed at no longer received port updates. Quantum now also reads the per-user client log at `%LocalAppData%\Proton\Proton VPN\Logs\client-logs.txt`, which carries the same port information.

### Changed
- The active log file path shown in the settings is updated to the one Quantum actually found a port in, so the UI matches reality.

## 1.6.0 - Quantum Reloaded

Community continuation of Quantum 1.5.0 by UHAX (https://github.com/UHAXM1/Quantum).

### Added
- Option to ignore certificate errors, for a qBittorrent WebUI served over HTTPS with a self-signed certificate.
- Post-update script: run a `.bat`, `.cmd`, `.ps1` or `.exe` after the port is updated. The new port is passed as the first argument and as the `QUANTUM_PORT` environment variable. The exit code is logged.

### Changed
- The port is updated with a single targeted WebUI call instead of rewriting all preferences (safer with qBittorrent 5.2+).
- Updated to .NET 10.
- Distributed as a single self-contained `Quantum.exe`, no .NET runtime to install.

### Fixed
- The project builds again from a clean checkout (removed an unused reference that was missing from the project).

### Notes
- Tested against qBittorrent 5.2.
- qBittorrent 5.x validates the Host header including the port. Behind a reverse proxy or a port mapping this returns 401; see the Troubleshooting section in the README.
