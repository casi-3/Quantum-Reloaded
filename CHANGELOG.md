# Changelog

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
